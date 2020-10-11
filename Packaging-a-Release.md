

# Introduction

The normal development flow within the Comma.ai repository is that the master branch is the actively developed branch. The master-ci, develop and Release2 branches are created through a CI deployment process. This process is not documented.

The easiest and safest way to perform the build and package process is to use an EON or a Comma2 - in fact there are scripts within the repo to perform a build remotely without using SSH or Workbench. If you are developing on Windows, however, you will need to run the scripts directly on the device.

I am going to assume you know how to SSH into your EON / Comma2. For the purpose of this document I will refer to your device as an EON - but it also applies to the Comma2.


# Preparing your EON

1. Generate RSA key pair as /tmp/deploy_key
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
Do not password protect it; change the email to the email associated with your account
When prompted for a location, enter "/tmp/deploy_key"
this will generate two files - deploy_key and deploy_key.pub. Please backup these files (I sftp into a server of mine and uploaded them for safe keeping)
2. Add deploy key to your Github account
On the EON, run cat /tmp/deploy_key.pub. Copy the block of text that is outputted. (It should begin with ssh-rsa and end with your email in quotes)
Open your Github profile settings, and select keys: [https://github.com/settings/keys](https://github.com/settings/keys)
Click New SSH Key, enter any name you wish, and paste the public key text. Save







