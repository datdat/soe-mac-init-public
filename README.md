# Pre ReInstall tasks
## Git
* Check for any uncommit changes
```bash
cd ~/code
#!/bin/bash

# Find all directories with a .git folder
find . -type d -name ".git" | while read -r git_dir; do
    # Get the repository directory (parent of .git)
    repo_dir=$(dirname "$git_dir")
    echo "Checking repository: $repo_dir"
    
    # Change into the repository directory
    cd "$repo_dir" || continue
    
    # Check for uncommitted changes
    if ! git diff --quiet || ! git diff --cached --quiet; then
        echo "  - Has uncommitted changes"
    fi
    
    # Check for unpushed commits to origin
    if git log origin/$(git rev-parse --abbrev-ref HEAD)..HEAD 2>/dev/null | grep -q '.'; then
        echo "  - Has unpushed commits"
    fi
    
    # Return to the original directory
    cd - > /dev/null
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
./run-playbook.sh macos-post.yml
```
```bash
./ssh-load-apple-keychain-key.sh
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

