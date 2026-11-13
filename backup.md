# Pre ReInstall tasks
## Git
* Check for any uncommit changes
```bash
cd ~/code
git-check-commit-status.sh
```

# Applications data
* Export RDP setting
* FoxyProxy setting

## Files Backup
* Manually cleanup first
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