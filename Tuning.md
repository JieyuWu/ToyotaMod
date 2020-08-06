![Tuning](https://user-images.githubusercontent.com/37757984/83087550-658b3c00-a046-11ea-9744-8f1e51fa8009.png)

[◄ Home](https://github.com/commaai/openpilot/wiki)

# Lateral Tuning

### INDI tuning strategy
 - Vary one parameter at a time, by less than 10%, finding lower and upper edges of stability.
 - Use a road you travel often and know well, with straights and curves, and excellent lane markings on both sides.
 - Start with moderate values for outer (angle error) and inner (rate error) loops,  like the Prius's outer 3, inner 4.
 - Avoid instability: wobble, sloppy lane keeping, entering or exiting corners poorly, oscillating or jerky steering.

1. CRITICAL: Tune actuator delay first. Enter and exit curves dead center, no wobble on straights.
2. Tune actuator effectiveness. Lowest value without oversteering. May vary with speed.
3. Tune time constant. Lowest value with smooth actuation.
4. Tune inner loop (steer rate error gain). Highest value with smooth corrections on curves.
5. Tune outer loop (steer error gain). Highest value with smooth corrections on straights.

### Notes on INDI tuning parameters
* steerActuatorDelay
  * Plan(now + steerActuatorDelay) -> Vehicle Model -> Desired Steer Output
  * Emits controls ahead on plan
  * Crude
    * If turning too early, decrease steerActuatorDelay
    * If turning too late, increase steerActuatorDelay
    * On straight section, vary in small steps away from best guess until the plan wobbles left and right.
  * Fine
    * Steer torque, pose yaw are proportional
    * Normalize torque and yaw signals
    * Find median phase delay in frequency domain?
    * Find maximum correlation of varying time delay?
* lateralTuning.indi.actuatorEffectiveness
  * As effectiveness increases, actuation strength decreases
  * Too high: weak, sloppy lane centering, slow oscillation, can't follow high curvature, high steering error causes snappy corrections
  * Too low: overpower, saturation, jerky, fast oscillation
  * Just right: just above fast oscillation
* lateralTuning.indi.timeConstant
  * Extend exponential decay of prior output steer
  * Too high: sloppy lane centering
  * Too low: noisy actuation, responds to every bump
  * Just right: just above noisy actuation and lane centering instability
* lateralTuning.indi.innerLoopGain
  * Steer rate error gain
  * Too high: jerky oscillation in high curvature
  * Too low: sloppy, cannot accomplish desired steer angle
  * Just right: brief snap on entering high curvature
* lateralTuning.indi.outerLoopGain
  * Steer error gain
  * Too high: twitchy hyper lane centering
  * Too low: sloppy, all over lane
  * Just right: crisp lane centering

# Longitudinal Tuning
[Skip to tuning](#Tuning-the-longitudinal-PI-controller)
## Introduction

### Understanding how openpilot decides what speed to travel
*This will change when comma.ai moves to using the driving model for full longitudinal control*.

openpilot uses your car's radar (which returns up to 16 to 18 detected objects) and the driving model to select a radar point using the camera. openpilot runs the selected radar point (called a lead) through a kalman filter to get a more accurate acceleration and speed of the lead. The lead's speed, acceleration, and distance is sent to a longitudinal [MPC](https://en.wikipedia.org/wiki/Model_predictive_control) which after some complex math returns a desired speed to travel (along with desired acceleration) to [long_mpc.py](/commaai/openpilot/blob/master/selfdrive/controls/lib/long_mpc.py). This speed (which we'll mostly focus on) is then used by [longcontrol.py](/commaai/openpilot/blob/master/selfdrive/controls/lib/longcontrol.py) and a PI loop (not PID) which controls the gas and brakes.

**In short, all you need to know is the lead's speed, acceleration, and distance is the input and a desired speed to travel is the output of the longitudinal MPC (along with a few extra values like future desired speed, acceleration, etc).**

### Your vehicle's interface file
Now that you have some background on how openpilot's `LongitudinalMpc` works (it's not necessary to understand everything) we can move on to understanding how the PI loop controls your vehicle's gas and brakes and subsequently actually tuning your vehicle. Here are some of the parameters that `longcontrol`'s PI loop uses to output a gas signal sent to the car (from Toyota's [interface file](/commaai/openpilot/blob/master/selfdrive/car/toyota/interface.py#L288)):

![](https://i.imgur.com/e3w1kUM.png)

### How the breakpoint and value lists work
When you see `xBP` and `xV`, that means that the speeds defined in the breakpoint list (`xBP`) correspond to the values in the value (`xV`) list.

So for example let's say `xBP = [0., 5., 35.]` (in m/s) and `xV = [1.0, 1.5, 2.0]`

When you are traveling 5 m/s `1.5` is the value that openpilot uses, for 35 m/s `2.0` is the corresponding value. Speeds in between the defined speeds in `xBP` are linearly interpolated, so if you're halfway between 5 and 35 m/s the output will be halfway between `1.5` and `2.0`. How this works in code: `np.interp(20, [0., 5., 35.], [1.0, 1.5, 2.0]) = 1.75`

## Understanding the PI controller
* Proportional (`kpBP` and `kpV`):
  - Again, `kpBP` is the breakpoint list and `kpV` is the values list that the PI loop uses in operation. `kpV` or `kp` stands for proportional gain, and it's the simplest part of the PI controller. If you just had a P controller the output would simply be defined as `(desired speed - current speed) * proportional gain`. The first section is also known as the *error*. In code (from `pid.py`), this would look like: `error * self.k_p`. That proportional gain we're multiplying here changes based on your speed.

    Once you get the output, you would simply return the value and use it as the gas/brake value to send to the car.

* Integral (`kiBP` and `kiV`):
  - `kiV` or `ki` stands for integral gain. You can think of integral as the error (again, `desired speed - current speed`) that builds up over time. For a simple example, let's say that the error is `1` for one iteration (desired speed is 1 mph faster than our current speed). Then in the next iteration let's say we're still traveling at the same speed and we still want to go 1 mph faster.

    We now take the previous error and the current error, which both are `1` and sum them. Now our integral value is `2` (not gain, that's what is multiplied by `2` here to get the final output). This continues forever, so if the error is too small from proportional to bring us to our desired speed (think something like 50 mph - 49.5 mph), integral would build up over time and help us apply more gas to reach the desired speed.

    In a more concrete example, let's say we're approaching a steep hill and we want to maintain our speed of 50 mph. Of course the hill makes us lose some speed initially as the incline starts to increase, so proportional would kick in as our error increases. However, once we get close enough to the desired speed again, the output of proportional would fall to near 0, causing us to lose speed again. Here's where integral steps in. It can see the sum of the past errors, so integral would build up the longer we're lower than 50 mph, causing a higher gas output.

    In pseudo code, this looks like `self.i = self.i + (error * integral gain)`. You can see the two things that increase the output of the integral factor are error and time. If the error is large, integral increases. And if any error exists for some amount of time, integral increases.

* `gasMaxBP` and `gasMaxV`:
  - `gasMaxV` represents the maximum percentage of gas (0 being no gas and 1 being 100% gas) allowed to be output by the PI loop. Since `gasMaxBP = [0.]` and `gasMaxV = [0.5]`, the maximum gas allowed by the PI loop is 50% which is used at all speeds.

**The output of the PI loop (excluding feedforward) is essentially the sum of the output of the proportional factor and integral factor. `control = self.p + self.i`**

## Tuning the longitudinal PI controller
The two main factors you can tune to get a different response out of the long PI loop are of course proportional and integral. *To make the tuning process less complex, it's said to set the integral gain to all 0's so the only thing that's interacting with the output is proportional at first.*

- When to increase proportional:
  1. If your car doesn't give enough gas or brake to reach the set cruise speed in a timely manner.
  2. If your car doesn't brake enough when you approach a stopped lead.
- When to decrease proportional:
  1. If your car applies so much gas or brake trying to reach the desired speed that it doesn't feel smooth.
  2. If it doesn't feel smooth when reacting to a change in desired speed.

After you have it tuned so that it feels smooth enough either cruising without a lead, or with a lead that is always changing its speed, it's time to start tuning integral.

- When to increase integral:
  1. If when the lead is decelerating/accelerating over a few seconds and the car doesn't give enough gas or brake to maintain a safe/reasonable distance
  2. If you're traveling up or down a hill and the car doesn't give enough gas or brake to maintain your desired speed.
- When to decrease integral:
  1. If you start to experience overshoot (most easily identifiable on hills); ex. once you reach the crest of a hill and your car continues to apply gas when it should start to ease off.