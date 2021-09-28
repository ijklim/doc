# Git Commands

```sh
# Create a new branch and check out the new branch
git checkout -b <branch_name>

# Rename a local branch
# • Option 1
git checkout <old_name>
git branch -m <new_name>
# • Option 2
git branch -m <old_name> <new_name>

# Delete a local branch
git branch -d <old_name>

# Delete a remote branch
git push origin --delete <old_name>

# Initialize git with default branch <branch_name>
git init -b <branch_name>

# Display git configurations
git config -l
git config --global -l

# Credentials
git config --global --unset-all credential.helper
git config --global --unset credential.helper
## 3600 = 60 * 60 = 1 hour
git config --global credential.helper "cache --timeout=3600"
```

# Git Setup

## Global .gitignore

```sh
git config --global core.excludesfile ~/.gitignore

# Create or edit ~/.gitginore accordingly
```