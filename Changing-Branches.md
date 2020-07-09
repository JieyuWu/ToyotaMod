[◄ Home](../wiki)

By switching away from the default `release2` branch of Openpilot, you will lose the benefit of Comma's rigorous test and review process.  All other branches can and likely do have bugs, some of which may cause undesirable behavior, **you switch branches at your own risk.**

# Introduction
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

## Notes on Switching Branches for Developers
When switching between branches, if the version of cereal or some other submodule has changed between the branches, you may encounter errors including the "communication between processes" issue.  To reinitialize the submodules after you checkout a new branch run the following commands:

```
git submodule deinit --all -f 
git submodule init
git submodule update
```