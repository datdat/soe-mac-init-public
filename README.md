# Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
- Run these two commands in your terminal to add Homebrew to your PATH:
    (echo; echo 'eval "$(/opt/homebrew/bin/brew shellenv)"') >> /Users/kong/.zprofile
    eval "$(/opt/homebrew/bin/brew shellenv)"

# Software installation
brew install dropbox firefox keepassxc

# Finder
## Connect to Server
smb://media@ebox.nguyen.im



# 
open "smb://media@ebox/media"
cp -a /Volumes/media/mm/keys ~/.
ssh-add --apple-use-keychain ~/keys/ssh_pn_personal_rsa.key
ssh-add --apple-use-keychain ~/keys/ssh_pn_wtg_rsa.key
