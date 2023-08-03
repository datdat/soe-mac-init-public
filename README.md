#  Terminal and HomeBrew
* Grant Terminals full disk access
* Change screen resolution
* HomeBrew
```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/kong/.zprofile
source /Users/kong/.zprofile
```


# Grab ssh keys
```
open "smb://media@ebox/media"
```
```
ssh_keys_out_dir=~/keys
mkdir "$ssh_keys_out_dir"
cd /Volumes/media/downloads/backup/ssh_keys
echo 'PASSWORD HINT: My first cat name'
for i in *.enc; do openssl enc -d -md md5 -aes-256-cbc -in "$i" -out "$ssh_keys_out_dir/${i//.enc}" ;done
chmod -R 0600 $ssh_keys_out_dir/*
cd - 
```

# Load the keys
    ssh-add --apple-use-keychain ~/keys/*.key    
    
# Ansible
```
brew install ansible firefox
```
```
ansible-galaxy collection install community.general
```
```
mkdir -p ~/code/personal
cd ~/code/personal
git clone 'git@github.com:datdat/soe-mac.git'
cd soe-mac/ansible
```
```
./run-playbook.sh
```
```
./run-playbook.sh run-once.yml
```
Reboot
```
./run-playbook.sh macos-post.yml
```

#  MANUAL
* Setup Profile Me profile
*     /Applications/Firefox.app/Contents/MacOS/firefox -P "me" &
* Setup SYNC
* Appstore app:
    * RDP
* Setup Dropbox (me [@] n........im)
* Download greenlock keyfile from Google Drive and:
*     mv ~/Downloads/greenlock.keyx ~/keys/.
* Setup Profile Work profile (work [@] n......im)
*     /Applications/Firefox.app/Contents/MacOS/firefox -P "work" &
* Visual Code
    * Sign-in with github (d-a-t-[d]at) - 
    * Check if Auto Save is automatically sync
* Sign out from iMessages
* Disable handoff
* LockScreen, require password after 8 hours 

