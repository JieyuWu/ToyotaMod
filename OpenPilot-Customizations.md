# Tweaks

Serves to document various small Openpilot (OP) customizations that others have implemented for themselves in the code base.  With each tweak, commands to apply the tweaks have been provided. Applying these tweaks will likely break the self-updating process, either necessitating a reinstall of the openpilot software or manual intervention.

The commands are to be run while SSH'd into the Comma device.

## Stop and Go Hack (Toyota)

https://github.com/ErichMoraga/openpilot/commit/4759891494b3f291e8f94093b98703e70937cc7b

```
cd /data/openpilot
git remote add erich https://github.com/ErichMoraga/openpilot.git
git fetch erich
git cherry-pick 4759891494b3f291e8f94093b98703e70937cc7b
```

Comments out 2 lines in the `carcontroller.py` to enable stop and go on Toyota's customized with a SmartDSU.

## Easing up Internet Requirements

https://github.com/ErichMoraga/openpilot/commit/29497f1d086e2ae0bee7ff24ba26adefc78c2dc9

Change the day counter values for `DAYS_NO_CONNECTIVITY_MAX` and `DAYS_NO_CONNECTIVITY_PROMPT` from the default of 7 & 4 days to 30 and 26 days.

```
cd /data/openpilot
git remote add erich https://github.com/ErichMoraga/openpilot.git
git fetch erich
git cherry-pick 29497f1d086e2ae0bee7ff24ba26adefc78c2dc9
```

## Minimize custom fork warning

https://github.com/ErichMoraga/openpilot/commit/ef8051484cd24b958bd4d13d7fbfa18fe6743cad

```
cd /data/openpilot
git remote add erich https://github.com/ErichMoraga/openpilot.git
git fetch erich
git cherry-pick ef8051484cd24b958bd4d13d7fbfa18fe6743cad
```

## Powering off after X hours

https://github.com/ErichMoraga/openpilot/commit/6717ce7db6cd930cb53fc1dadcc49a479ee192eb

define `MAX_TIME_OFFROAD_S` in seconds.  3600 seconds is an hour, so `30 * 3600` represents 30 hours.  This commit customizes the time down to shut off after 3 hours.

```
cd /data/openpilot
git remote add erich https://github.com/ErichMoraga/openpilot.git
git fetch erich
git cherry-pick 6717ce7db6cd930cb53fc1dadcc49a479ee192eb
```

## Acceleration Tweak (Toyota Only)

https://github.com/ErichMoraga/openpilot/commit/d72f6be5ff4ba4b377228328d5abf25157005755

Appears to dynamically set acceleration parameters to maximize acceleration below 13mph, while gradually reducing acceleration in a linear fashion as miles per hour goes up.

```
cd /data/openpilot
git remote add erich https://github.com/ErichMoraga/openpilot.git
git fetch erich
git cherry-pick d72f6be5ff4ba4b377228328d5abf25157005755
```

## Disabling Updates

```
echo -en "1" > /data/params/d/DisableUpdates
```