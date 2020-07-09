[◄ Home](../wiki)

# Overview
Updating openpilot for most users is intended to be an automatic process, when it comes to official releases (i.e. versions that are listed here: https://github.com/commaai/openpilot/releases). As of this writing, June 3rd, the current latest official release is v0.7.5 (`git checkout release2`)

By switching away from the default `release2` branch of Openpilot, you will lose the benefit of Comma's rigorous test and review process.  All other branches can and likely do have bugs, some of which may cause undesirable behavior, **you switch branches at your own risk.**

## Git Branches
See the [Pro Git Book](https://git-scm.com/book/en/v2) and specifically the chapter on [Git Branches](https://git-scm.com/book/en/v2/Git-Branching-Branches-in-a-Nutshell) for an explanation of what a branch is. See the [Openpilot Development Flow](https://medium.com/@comma_ai/a-2020-theme-externalization-13b33326d8b3#9f7b:~:text=openpilot%20development%20flow) discussion on George's Medium post on Externalization for an explanation of the various Openpilot branches.

## Why Would a User Switch Branches?
Switching branches is primarily the realm of developers.  However, there are two reasons why a general user may want to switch to the `master-ci` branch of Openpilot:
* Gaining access to a bug fix
* Gaining access to newly fingerprinted vehicles

## How to Switch to `master-ci` (Non-Developers)
1. You will first need to gain access to your device using SSH, see the [SSH instructions](https://github.com/commaai/openpilot/wiki/SSH). 
2. Then you need to run the following command:
 
This command will replace whatever version of openpilot you are currently running with the `master-ci` branch. **Caution:** this command will blow away the openpilot directory, so if you are a developer who has made changes to openpilot, this command is not for you.

`cd /data && rm -rf openpilot && git clone -b master-ci https://github.com/commaai/openpilot && reboot`

## For Developers

However, if you want to test out newer, unreleased version like 0.8.0, the easiest way is to `git clone` openpilot directly onto your CommaTwo/EON and `git checkout` the master branch (could potentially be unstable since changes are made daily). The steps below show how to ensure you are on the git branch that has the latest code changes. 

The latest openpilot revisions come from the main repository: https://github.com/commaai/openpilot . \
If you want to test out your own modified code, create a fork of the main repo and clone that one (branches should still be the same)

### 1. [SSH](../wiki/SSH) into your comma2/EON
`cd /data/`\
`mv openpilot/ openpilot.backup`\
`git clone https://github.com/commaai/openpilot.git`\
`cd openpilot`

### 2. Checkout your desired branch
* `release2` - latest official release with compiled binary. Does not need to be built on the device
  * `git checkout release2`
* `master` - latest openpilot changes. The master branch has submodules, which need to be updated/initialized, otherwise once you reboot your build will fail. Needs to be built on the device.
  * `git checkout master`
  * `git submodule update --init --recursive`
  * `reboot` to start build
* `master-ci` - latest openpilot changes, with submodules already integrated. Needs to be built on the device.
  * `git checkout master-ci`
  * `reboot` to start build
* `devel`
* `devel-staging`

### 3. (Optional) Monitor build process after reboot
For branches that need to be built, you can monitoring the building process by SSH'ing into your comma right after reboot and typing `tmux a`

### Developer Notes

When switching between branches, if the version of cereal or some other submodule has changed between the branches, you may encounter errors including the "communication between processes" issue.  To reinitialize the submodules after you checkout a new branch run the following commands:

```
git submodule deinit --all -f 
git submodule init
git submodule update
```