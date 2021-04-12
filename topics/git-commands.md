# Git Commands

```sh
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
```