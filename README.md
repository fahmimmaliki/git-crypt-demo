# git-crypt-demo
This repository demonstrates the use of [git-crypt](https://github.com/AGWA/git-crypt), a tool that provides transparent encryption of files in a Git repository.

## Using Git-Crypt
- Lock the repository: `git-crypt lock`
- Unlock the repository: `git-crypt unlock ~/git-crypt-key-file`
- Check the status of encrypted files: `git-crypt status`
## Files
- `file.txt`: A sample file used for demonstration plain file
- `.env.development`: An environment file used for demonstration encrypted file
- `.gitattributes`: The configuration file for Git-Crypt

## Step to produce this repo
```bash
git init
# Create file.txt
echo "This is some text" > file.txt
git add file.txt
git commit -m "Initial Commit"
git-crypt init
# Export git-crypt key
git-crypt export-key ~/git-crypt-demo-key
# Config to encrypt all .env.* in current dir
echo ".env.* filter=git-crypt diff=git-crypt" > .gitattributes
git add .gitattributes
git commit -m "Tell git-crypt to encrypt .env.*"
echo "dummy value" > .env.development
git-crypt status
git add .env.development
git commit -m "Added env dev file"
git-crypt lock
cat .env.development
git-crypt unlock ~/git-crypt-demo-key
git remote -v
git remote add origin git@github.com:fahmimmaliki/git-crypt-demo.git
git status
git push --set-upstream origin main
```
