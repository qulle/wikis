# .bashrc
A living document containing my .bashrc config.

## Note
This used to be a private repo but i changed it to be public because of ease of access for me. Use it as a reference if you like it but `i am not accountable for what happens when you execute commands in your environment`, use with causion and Google commands that you don't know.

## .bashrc config
```
# Default start location for new shell
cd C:\\Users\\daniel\\Documents\\dev

# Aliases
#-----------------------------------------------------------------------------------------------------------
## General
alias cls='clear'
alias commands='printf "
    == GENERAL
       commands : Prints this list
       cls      : Clear screen

    == PROGRAM
       e : Start Explorer in current directory
       c : Start VSCode in current directory

    == BASH
       rbash : Reloads bash config in current shell
       ebash : VSCode editing this file

    == DIRECTORY SHORTCUTS
       h   : Home location
       dev : Root directory for all dev projects

    == NPM
       npmgc : Prints global installed npm packages
       npmgl : Prints global linked packages
       npmgs : Prints global symlinks

    == C++
       w++17 : g++ compiler with cpp version 17 and flags [ -Wall -Wextra -Wpedantic ]
"'

alias gitcommands='printf "
    == COMMIT
       git add .
       git commit -m \"Message of the commit\"
       git commit --amend --no-edit

    == PUSH
       git push
       git push -f

    == MERGE
       git merge origin/main
       git add .
       git commit -m \"Resolved merge conflict\"
       git merge --abort

    == RESET
       git reset
       git reset --soft HEAD~1
       git reset --hard HEAD~1
       git reset --hard HEAD@{1}

    == LOG
       git log
       git log --raw
       git log --pretty=oneline
       git log --graph --oneline --all
"'

## Program
alias e='explorer .'
alias c='code .'
alias vsc17='"C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\Professional\\Common7\\IDE\\devenv.exe" &'
alias vsc19='"C:\\Program Files (x86)\\Microsoft Visual Studio\\2019\\Professional\\Common7\\IDE\\devenv.exe" &'
alias vsc22='"C:\\Program Files\\Microsoft Visual Studio\\2022\\Professional\\Common7\\IDE\\devenv.exe" &'

## Bash
alias rbash='source ~/.bashrc'
alias ebash='code ~/.bashrc'

## Directory shortcuts
alias h='cd'
alias dev='cd ~/Documents/dev'

## NPM
alias npmgc='npm list -global --depth=0'
alias npmgl='npm ls -g --depth=0 --link=true'
alias npmgs='ls -al $(npm root -g) | grep "\->"'

## GIT
alias rowcount='git ls-files | xargs wc -l'

## C++
alias w++17='g++ -std=c++17 -Wall -Wextra -Wpedantic'

# Load Angular CLI autocompletion
#-----------------------------------------------------------------------------------------------------------
source <(ng completion script)
```
