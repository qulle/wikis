# Git commands
A living document with useful git commands, not intended as a complete git reference.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`, use with causion and Google commands that you don't know.

## Init
### Start empty local git repo
```
$ git init
$ git clone <URL>
```

### Three ways to track remote branch 
```
$ git push -u <origin/BRANCH-NAME> <LOCAL-BRANCH-NAME>
$ git branch -u <origin/BRANCH-NAME>
$ git branch --set-upstream-to <origin/BRANCH-NAME>
```

## Commit and push/pull
### Staging files before commit 
```
$ git add .      # Stage new and modified files only
$ git add *      # Same as above except that this does not add files beginning with .
$ git add -A     # Stage all new files, new, modified and deleted
$ git add -u     # Stage modified and deleted files only
```

### Check status of staged and non staged files
```
$ git status
```

### Commit
```
$ git commit -m "Commit message"
$ git commit --amend --no-edit                # Note, this will create a new commit hash and re-write history needing git push -f
$ git commit --amend --no-edit --date=now     # Update last commit with new timestamp, also creates new commit hash

$ git checkout -- <FILE>                      # Undo changes that not have been commited (-- is to target files, if branch have same name)
$ git restore <FILE>                          # Undo changes that not have been staged
$ git restore --staged <FILE>                 # Remove files that have been changed and staged

$ git clean -n                                # List files that will be deleted
$ git clean -f                                # Delete untracked files
$ git clean -fd                               # Delete untracked files and directories
$ git clean -fX                               # Delete ignored files
$ git clean -fx                               # Delete ignored and untracked files

$ git reset                                   # Unstage files that have been added but not commited
$ git reset --soft HEAD~1                     # Undo the last commit and preserve changes that were made as unstaged files
$ git reset --hard HEAD~1                     # Undo the last commit and don't preserve changes
$ git reset --hard HEAD@{1}                   # Undo the previous reset --hard HEAD~1
$ git reflog                                  # Show log och git ref history
$ git reset --hard <COMMIT HASH>              # Undo any reset --hard
```

### Push
```
$ git push 
$ git push -f     # Force push files ex. when history has diverged, use with caution
```

### Push /dist folder as subtree to gh-page at github
```
1. Github
a) Remove the gh-pages branch from github
b) Checkout the main branch locally

2. Add dist folder to the staged area
$ git add dist -f

3. Commit the dist folder
$ git commit -m "gh-pages demo"

4. Push the commit as a subtree to the gh-pages branch
$ git subtree push --prefix dist origin gh-pages

5. Undo the last commit from the main branch
$ git reset --hard HEAD~1
```

### Pull
```
$ git fetch                                         # Check if any new changes have been made in remote
$ git merge <BRANCH-NAME-TO-MERGE-INTO-CURRENT>     # Insert changes from one branch into the current branch
$ git pull                                          # Try download any changes from remote, alias for git fetch and git merge
```

## Branching
```
$ git branch                                                 # Show all local branches
$ git branch -r                                              # Show remote branches
$ git branch -vv                                             # Show what remote branches the local branches are tracking, if any
$ git branch -d <BRANCH-NAME>                                # Delete local branch 
$ git branch -D <BRANCH-NAME>                                # Force delete local branch that have uncommitted changes

$ git checkout -b <NEW-BRANCH-NAME>                          # Create new local branch based on the current branch
$ git checkout -b <NEW-BRANCH-NAME> origin/<BRANCH-NAME>     # Create new local branch and set up to track remote

$ git branch -m <NEW-BRANCH-NAME>                            # Renames current branch
$ git branch -m <OLD-BRANCH-NAME> <NEW-BRANCH-NAME>          # Renames any branch

$ git fetch --prune origin                                   # Clean delete branch at remote and also fetch
$ git remote prune origin                                    # Clean delete branch at remote
$ git config --global fetch.prune true                       # Configure to prune remote every time a pull is executed
```

## Working with history
```
$ git rebase -i <COMMIT-HASH>     # Enables powerful commands to be made on historical commits, like squashing history into one commit
```

## Logging
```
$ git log
$ git log --pretty=oneline
$ git log --graph --oneline --all
```

## Tagging
```
$ git tag                                                      # List available tags
$ git tag v1.4.0.0                                             # Basic lightweight tag
$ git tag -a v1.4.0.0 -m "Release version 1.4.0.0"             # Annotated tag
$ git tag -a v1.2.0.0 -m "Release version 1.2.0.0" 9fceb02     # Tagging later by specifying commit hash
$ git tag -d v1.4.0.0                                          # Delete tag

$ git push origin v1.4.0.0                                     # Push specific tag to remote
$ git push origin --tags                                       # Push all tags to remote
```

## Stashing
```
$ git stash save --keep-index --include-untracked
```

## Special git files
```
.gitignore     # Used to disregards some files and folders from being tracked
.gitkeep       # Non standard file, used by the community to track empty folders, git only track files
```
