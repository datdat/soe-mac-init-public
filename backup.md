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