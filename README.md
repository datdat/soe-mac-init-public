# HomeBrew
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

# Clone soe-mac
    git@github.com:datdat/soe-mac.git



    

--------------------
# Old

# Finder
## Connect to Server
smb://media@ebox.nguyen.im


```
cp -a /Volumes/media/mm/keys ~/.
ssh-add --apple-use-keychain ~/keys/ssh_pn_personal_rsa.key
ssh-add --apple-use-keychain ~/keys/ssh_pn_wtg_rsa.key

```


# Software installation
# brew install dropbox firefox keepassxc
