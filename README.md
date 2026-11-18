# Git Commands Cheat Sheet

## 1. Setup & Config

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git config --global init.defaultBranch main
git config --global core.editor "nano"
git config --list                      # show all config
```

## 2. Create / Clone a Repo

```bash
git init                               # start a new repo in current folder
git clone <url>                        # clone a remote repo
git clone <url> <folder-name>          # clone into a custom folder
```

## 3. Basic Workflow

```bash
git status                             # see changed/staged files
git add <file>                         # stage a file
git add .                              # stage everything
git commit -m "message"                # commit staged changes
git commit -am "message"               # stage tracked files + commit
git commit --amend                     # edit the last commit
```

## 4. View History & Changes

```bash
git log                                # full history
git log --oneline                      # compact history
git log --oneline --graph --all        # branch graph
git diff                               # unstaged changes
git diff --staged                      # staged changes
git show <commit>                      # details of a commit
git blame <file>                       # who changed each line
```

## 5. Branching

```bash
git branch                             # list local branches
git branch -a                          # list all (incl. remote)
git branch <name>                      # create branch
git switch <name>                      # switch branch
git switch -c <name>                   # create + switch
git checkout <name>                    # older way to switch
git branch -d <name>                   # delete (merged) branch
git branch -D <name>                   # force delete
git branch -m <new-name>               # rename current branch
```

## 6. Merging & Rebasing

```bash
git merge <branch>                     # merge branch into current
git merge --abort                      # cancel a conflicted merge
git rebase <branch>                    # replay commits on top of branch
git rebase --continue                  # after fixing conflicts
git rebase --abort                     # cancel rebase
git cherry-pick <commit>               # apply a single commit
```

## 7. Remote Repositories

```bash
git remote -v                          # list remotes
git remote add origin <url>            # add a remote
git remote set-url origin <url>        # change remote URL
git remote remove origin               # remove remote
git fetch                              # download changes (no merge)
git pull                               # fetch + merge
git pull --rebase                      # fetch + rebase
git push                               # push to remote
git push -u origin <branch>            # push + set upstream
git push origin --delete <branch>      # delete remote branch
```

## 8. Undoing Things

```bash
git restore <file>                     # discard unstaged changes
git restore --staged <file>            # unstage a file
git reset --soft HEAD~1                # undo last commit, keep changes staged
git reset --mixed HEAD~1               # undo last commit, keep changes unstaged
git reset --hard HEAD~1                # undo last commit, DELETE changes
git revert <commit>                    # new commit that undoes a commit
git clean -fd                          # remove untracked files/folders
```

> ⚠️ `reset --hard` and `clean -fd` permanently delete work. Use with care.

## 9. Stashing

```bash
git stash                              # save changes temporarily
git stash -u                           # include untracked files
git stash list                         # list stashes
git stash pop                          # apply + remove latest stash
git stash apply                        # apply, keep stash
git stash drop                         # delete latest stash
git stash clear                        # delete all stashes
```

## 10. Tags

```bash
git tag                                # list tags
git tag v1.0                           # lightweight tag
git tag -a v1.0 -m "Release 1.0"       # annotated tag
git push origin v1.0                   # push one tag
git push origin --tags                 # push all tags
git tag -d v1.0                        # delete local tag
```

## 11. .gitignore & Cleanup

```bash
echo "node_modules/" >> .gitignore     # ignore a folder
git rm --cached <file>                 # stop tracking a file (keep locally)
git rm <file>                          # delete + stage deletion
git mv <old> <new>                     # rename/move a file
```

## 12. SSH Key for GitHub

```bash
ssh-keygen -t ed25519 -C "you@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
cat ~/.ssh/id_ed25519.pub              # copy into GitHub → Settings → SSH keys
ssh -T git@github.com                  # test connection
```

## 13. Useful Extras

```bash
git reflog                             # history of HEAD moves (recover lost commits)
git shortlog -sn                       # commits per author
git config --global alias.st status    # create alias: git st
git archive --format=zip HEAD -o out.zip   # export repo as zip
```

## Common Workflow Example

```bash
git clone <url>
git switch -c feature/login
# ...edit files...
git add .
git commit -m "Add login feature"
git push -u origin feature/login
# open a Pull Request on GitHub, then:
git switch main
git pull
git branch -d feature/login
```
