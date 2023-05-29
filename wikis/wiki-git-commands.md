# Git commands
A living document with useful git commands, not intended as a complete git reference.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`. Use with causion and Google commands that you don't know.

### Configurations
```
$ git config --global user.name "John Doe"
$ git config --global user.email "john.doe@domain.com"
```

## Init
### Start empty local git repo
```
$ git init
$ git clone <url>
```

### Three ways to track remote branch 
```
$ git push -u origin/<branch-name> <locale-branch-name>
$ git branch -u origin/<branch-name>
$ git branch --set-upstream-to origin/<branch-name>
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
$ git commit --amend --no-edit                 # Note, this will create a new commit hash and re-write history needing git push -f
$ git commit --amend --no-edit --date=now      # Update last commit with new timestamp, also creates new commit hash
$ git commit --amend --author="John Doe <john.doe@domain.com>" --no-edit  # Update author of the last commit

$ git checkout -- <filename>                   # Undo changes that not have been commited (-- is to target files, if branch have same name)
$ git restore <filename>                       # Undo changes that not have been staged
$ git restore --staged <filename>              # Remove files that have been changed and staged

$ git clean -n                                 # List files that will be deleted
$ git clean -f                                 # Delete untracked files
$ git clean -fd                                # Delete untracked files and directories
$ git clean -fX                                # Delete ignored files
$ git clean -fx                                # Delete ignored and untracked files

$ git reset                                    # Unstage files that have been added but not commited
$ git reset --soft HEAD~1                      # Undo the last commit and preserve changes that were made as unstaged files
$ git reset --hard HEAD~1                      # Undo the last commit and don't preserve changes
$ git reset --hard HEAD@{1}                    # Undo the previous reset --hard HEAD~1
$ git reflog                                   # Show log och git ref history
$ git reset --hard <commit-hash>               # Undo any reset --hard

$ git rm --cached <filename>                   # To stop tracking a file, it must be removed from the index
$ git rm -r --cached <folder-name>             # To stop tracking a folder, it must be removed from the index

$ git mv --force src/ts/file.ts src/ts/File.ts # Rename file that already is tracked
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
$ git push origin --delete gh-pages

b) Checkout the main branch locally
$ git checkout main
$ git pull

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
$ git fetch                                                  # Check if any new changes have been made in remote
$ git merge <branch-name-to-merge-into-current>              # Insert changes from one branch into the current branch
$ git pull                                                   # Try download any changes from remote, alias for git fetch and git merge
```

## Branching
```
$ git branch                                                 # Show all local branches
$ git branch -r                                              # Show remote branches
$ git branch -vv                                             # Show what remote branches the local branches are tracking, if any
$ git branch -d <branch-name>                                # Delete local branch 
$ git branch -D <branch-name>                                # Force delete local branch that have uncommitted changes
$ git push origin --delete <branch-name>                     # Delete branch from remote

$ git checkout -b <branch-name>                              # Create new local branch based on the current branch
$ git checkout -b <branch-name> origin/<branch-name>         # Create new local branch and set up to track remote
$ git checkout -b tag-v1.0.0 tags/v1.0.0                     # Create new local branch and set up to track specific remote-tag

$ git branch -m <branch-name>                                # Renames current branch
$ git branch -m <branch-name-old> <branch-name-new>          # Renames any branch

$ git fetch --prune origin                                   # Clean delete branch at remote and also fetch
$ git remote prune origin                                    # Clean delete branch at remote
$ git config --global fetch.prune true                       # Configure to prune remote every time a pull is executed
```

## Working with history
```
$ git rebase -i <commit-hash>                                # Enables commands to be made on historical commits, like squashing history into one commit
$ git rebase --abort                                         # Abort ongoing rebase (main|REBASE)
$ git merge --abort                                          # Abort ongoing merge (main|MERGING)
```

## Logging
```
$ git log
$ git log --pretty=oneline
$ git log --graph --oneline --all
$ git show <commit-hash>                                     # Show information about specific commit 

$ git ls-tree -r master --name-only                          # List all files that are tracked by Git from current directory and down
$ git ls-files                                               # Alias for the command above
$ git ls-tree --full-tree --name-only -r HEAD                # Show all files that are tracked by Git
```

## Tagging
```
$ git tag                                                    # List available tags
$ git tag v1.4.0.                                            # Basic lightweight tag
$ git tag -a v1.4.0 -m "Release version 1.4.0"               # Annotated tag
$ git tag -a v1.2.0 -m "Release version 1.2.0" 9fceb02       # Tagging later by specifying commit hash
$ git tag -d v1.4.0                                          # Delete tag

$ git push origin v1.4.0                                     # Push specific tag to remote
$ git push origin --tags                                     # Push all tags to remote
$ git push origin --tags --force                             # Force push all tags to remote
```

## Stashing
```
$ git stash save --keep-index --include-untracked            # Make stash of all files
$ git stash list                                             # List all stashes
$ git stash show                                             # Show contents of latest stash
$ git stash show stash@{index}                               # Show contents of specific stash
$ git stash apply                                            # Get latest stashed changes back, without removing the stash from the history
$ git stash apply stash@{index}                              # Get specific stashed changes back, without removing the stash from the history
$ git stash pop                                              # Get latest stashed changes and remove from history
$ git stash pop stash@{index}                                # Get specific stashed changes and remove from history
```

## Special Git files
```
.gitignore                                                   # Used to disregard some files and folders from being tracked
.gitkeep                                                     # Non standard file, used to track empty folders, git only track files
.gitattributes                                               # Non standard file, used to ignore language-detection
```

### .gitignore example
```
/node_modules
/.cache
/.parcel-cache
/dist
```

### .gitattributes example
```
*.html linguist-detectable=false
*.css linguist-detectable=false
*.js linguist-detectable=true
```
