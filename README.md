# Pre ReInstall tasks
## Git
* Check for any uncommit changes
```bash
for dir in */; do
    # Check if it's a directory and has a .git folder
    if [ -d "$dir" ] && [ -d "$dir/.git" ]; then
        echo "Checking $dir..."
        cd "$dir" || continue
        
        # Check if there are uncommitted changes
        if ! git diff --quiet || ! git diff --cached --quiet; then
            echo "  Uncommitted changes found in $dir"
            git status -s  # Show short status of changes
        else
            echo "  No uncommitted changes in $dir"
        fi
        
        cd .. # Return to parent directory
    fi
done
```

## Backup
* Export RDP setting
* FoxyProxy setting
* tar gzip home directory
```bash
backupDate=$(date "+%Y-%m-%d")
backupTarget="/Volumes/media/downloads/backup/mm/$backupDate"
backupFilename="mm-home-dir.tgz"
mkdir $backupTarget

cd ~
tar --exclude '.git/' --exclude '.venv/' --exclude 'Dropbox' --exclude './Library' --exclude './.cache' --exclude './.docker' --exclude './Music' --exclude './go' --exclude './Pictures' --exclude './.kube' --exclude './.Trash' --exclude './.npm' --exclude './.vscode' --exclude './noBackup' --exclude './.ollama' \
--one-file-system -zcvf $backupFilename .

mv $backupFilename $backupTarget/.
```

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
cd /Volumes/media/downloads/backup/ssh_keys
echo 'PASSWORD HINT: My first cat name'
for i in *.enc; do openssl enc -d -md md5 -aes-256-cbc -in "$i" -out "$ssh_keys_out_dir/${i//.enc}" ;done
chmod -R 0600 $ssh_keys_out_dir/*
cd - 
```

# Load the keys
    ssh-add --apple-use-keychain ~/keys/*.key    
    
# Ansible
```bash
brew install ansible firefox
```
```bash
ansible-galaxy collection install community.general
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

