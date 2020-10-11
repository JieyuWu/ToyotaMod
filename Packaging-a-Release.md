

# Introduction

The normal development flow within the Comma.ai repository is that the master branch is the actively developed branch. The master-ci, develop and Release2 branches are created through a CI deployment process. This process is not documented.

The easiest and safest way to perform the build and package process is to use an EON or a Comma2 - in fact there are scripts within the repo to perform a build remotely without using SSH or Workbench. If you are developing on Windows, however, you will need to run the scripts directly on the device.

I am going to assume you know how to SSH into your EON / Comma2. For the purpose of this document I will refer to your device as an EON - but it also applies to the Comma2.

# Required code modifications

## selfdrive/common/version.h
Edit this to be specific to your fork / branch.
I suggest appending a short ID and a secondary version for your release
ex: 0.7.4-GM-0.1
Your version should be incremented with each release to ensure the update can be identified

If you updated Panda code, you should also update
panda/VERSION
I am using the same format as the OP version. It is even more important to update this, as OP uses it to decide if it should flash the Panda.


## release/build_devel.sh
Search for "commaai" and replace it with your github username. there should be 4 instances.
As of this writing, they are lines 10, 17, 20 and 40

Find this block and update the publisher info to match you
starts at line 29
`export GIT_COMMITTER_NAME="<Name>"
export GIT_COMMITTER_EMAIL="<email>"
export GIT_AUTHOR_NAME="<name>"
export GIT_AUTHOR_EMAIL="<email>"`

Around line 60, the submodules are added. If you are using a different branch than master, update the branch name
`add_subtree "cereal" "cereal" master
add_subtree "panda" "panda" master
add_subtree "opendbc" "opendbc" master
add_subtree "openpilot-pyextra" "pyextra" master`


## installer/installer.c

Around line 34
Update the repository url
`#define GIT_CLONE_COMMAND "git clone https://github.com/jasonjshuler/openpilot.git"`


## installer/Makefile
Around line 95, update the target branch name. I think it defaults to master2
This should match the branch you intend people to use. I recommend devel.
`					-DBRANCH=devel \`



## Commit and push all your changes. Make sure your submodules are updated as well












# Deployment Steps

## (Only need to do this once) 1. Generate RSA key pair as /tmp/deploy_key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Do not password protect it; change the email to the email associated with your account
When prompted for a location, enter "/tmp/deploy_key"
this will generate two files - deploy_key and deploy_key.pub. **Please backup these files** (I sftp into a server of mine and uploaded them for safe keeping)

**If you have already generated the key pair, simply upload them to the eon and place them in /tmp**
They will stay there until you do a factory reset.

## 2. Add deploy key to your Github account
On the EON, run cat /tmp/deploy_key.pub. Copy the block of text that is outputted. (It should begin with ssh-rsa and end with your email in quotes)
Open your Github profile settings, and select keys: [https://github.com/settings/keys](https://github.com/settings/keys)
Click New SSH Key, enter any name you wish, and paste the public key text. Save

## 3. Prepare the working directories
`cd /data
rm -r openpilot
rm -r openpilot_source
git clone https://github.com/JasonJShuler/openpilot.git openpilot_source`
In the clone line, replace the url with your repository and the branch name with your desired source branch. (note that this branch needs to match your deployment script and installer code

## Optional Step - compile installers (Only needs to be done once after you change the installer files)
If you customized the installer, you need to rebuild the binaries and check them in.
Replace <branch_name> with the name of your branch. this should be the same branch you have configured in the scripts.
`cd /data/openpilot_source
git checkout <branch_name>
git fetch
git pull
cd /data/openpilot_source/installer
make
cd installers
cd updater
make
cd /data/openpilot_source
git add .
git commit -m "updating installers"
git push`


## Run prep commands
These can just be pasted into the terminal. Be sure to press enter after the last line
Note: replace the master branch name with your source branch name.
`cd /data/openpilot_source
git reset --hard
git fetch origin
git checkout master
git clean -xdf
git submodule update --init
git submodule foreach --recursive git reset --hard
git submodule foreach --recursive git clean -xdf
`
## Perform the Build / Deploy

Note: replace "devel" with your target branch. Typical values are "master-ci" or "devel"
Note: if you have made any hotfixes the push will fail - **TODO: steps to resolve**
`PUSH=devel /data/openpilot_source/release/build_devel.sh`

If you did everything right, and your code is good, it will package and deploy. Your users' devices will auto-update on the next reboot

## OPTIONAL - Host your installer binary
The file /data/openpilot_source/installer/installers/install_openpilot should be uploaded to a webserver - you can name it whatever you want. The url to this file will allow people to install your fork from the EON without using SSH or Workbench. Note that newer cert issued by Comodo - which has been renamed to Sectigo - are not trusted and will not work. Use a digicert, or even a free ssl cert.

Finally, I recommend you uninstall OP and test your install url.






