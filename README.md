# Backup your existing enviroment
[backup instruction here](backup.md)


# Reset / Erase existing MacOS
* Go to System Settings, General, Transfer or Reset

## NOTE: Alternative option:
Wait for the Mac to shut down completely, then press and hold the power button until the system volume and the Options button appear.
This will download the OS

#  Terminal and HomeBrew
* Grant Terminals full disk access
* Change screen resolution
* HomeBrew
```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
```bash
(echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> ~/.zprofile
source ~/.zprofile
```



# Grab ssh keys
```bash
open "smb://media@ebox/media"
```
```bash
ssh_keys_out_dir=~/keys
mkdir "$ssh_keys_out_dir"
cd /Volumes/media/downloads/backup/keys
echo 'PASSWORD HINT: My cat first name'
read -s PASS
for f in *.enc; do
    openssl enc -d -md sha256 -aes-256-cbc -pbkdf2 -in "$f" -out "$ssh_keys_out_dir/${f%.enc}" -k "$PASS"
done

chmod -R 0600 $ssh_keys_out_dir/*
cd - 
ls -lah "$ssh_keys_out_dir"
```

# Load the keys
    ssh-add --apple-use-keychain ~/keys/*.key    
    
# Ansible
```bash
brew install ansible
```
```bash
mkdir -p ~/code/personal
cd ~/code/personal
GIT_SSH_COMMAND="ssh -o StrictHostKeyChecking=accept-new" git clone 'git@github.com:datdat/soe-mac.git'
cd soe-mac/ansible
```
```bash
./run-playbook.sh
```
```bash
./run-playbook.sh run-once.yml
```
Reboot
```bash
ssh-load-apple-keychain-key.sh
```
```bash
./run-playbook.sh macos-post.yml
```
#  MANUAL
* Setup Profile Me profile
*     /Applications/Firefox.app/Contents/MacOS/firefox -P "me" &
* Setup Firefox SYNC
* Restore RDP settings
* Setup Dropbox (me [@] n........im)
* Download greenlock keyfile from Google Drive and:
*     mv ~/Downloads/greenlock.keyx ~/keys/.
* Setup Profile Work profile (work [@] n......im)
*     /Applications/Firefox.app/Contents/MacOS/firefox -P "work" &
* Visual Code
    * Sign-in with github (d-a-t-[d]at) - 
* If signed into Apple ID:
    * Sign out from iMessages
    * Disable handoff
* LockScreen, require password after 8 hours 
