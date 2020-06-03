# Overview
Updating openpilot for most users is intended to be an automatic process, when it comes to official releases (i.e. versions that are listed here: https://github.com/commaai/openpilot/releases). As of this writing, June 3rd, the current latest official release is v0.7.5 (`git checkout release2`)

However, if you want to test out newer, unreleased version like 0.8.0, the easiest way is to `git clone` openpilot directly onto your CommaTwo/EON and `git checkout` the master branch (could potentially be unstable since changes are made daily). The steps below show how to ensure you are on the git branch that has the latest code changes. 

The latest openpilot revisions come from the main repository: https://github.com/commaai/openpilot . \
If you want to test out your own modified code, create a fork of the main repo and clone that one (branches should still be the same)

### 1. SSH into your comma2/EON
`cd /data/`\
`mv openpilot/ openpilot.backup`\
`git clone https://github.com/commaai/openpilot.git`\

### 2. Checkout your desired branch
* `release2` - latest official release with compiled binary. Does not need to be built on the device
  * `git checkout release2`
* `master` - latest openpilot changes. The master branch has submodules, which need to be updated/initialized, otherwise once you reboot your build will fail. Needs to be built on the device.
  * `git checkout master`
  * `git submodule update --init --recursive`
  * `reboot` to start build
* `master-ci` - latest openpilot changes, with submodules already integrated. Needs to be built on the device.
  * `git checkout master-cli`
  * `reboot` to start build
* `devel`
* `devel-cli`

### 3. (Optional) Monitor build process after reboot
For branches that need to be built, you can monitoring the building process by SSH'ing into your comma right after reboot and typing `tmux a`