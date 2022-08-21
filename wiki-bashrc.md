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
alias commands='printf "
    == GENERAL
        commands : Prints this list
        cls      : Clear screen

    == PROGRAM
        e : Start Explorer in current directory
        c : Start VSCode in current directory

    == BASH
        reloadbash : Reloads bash config in current shell
        editbash   : VSCode editing this file

    == DIRECTORY SHORTCUTS
        h   : Home location
        dev : Root directory for all dev projects

    == NPM
        npmcomponents : Prints globally installed npm packages

    == C++
        w++17 : g++ compiler with cpp version 17 and flags [ -Wall -Wextra -Wpedantic ]
"'
alias cls='clear'

## Program
alias e='explorer .'
alias c='code .'

## Bash
alias reloadbash='source ~/.bashrc'
alias editbash='code ~/.bashrc'

## Directory shortcuts
alias h='cd'
alias dev='cd ~/Documents/dev'

## NPM
alias npmcomponents='npm list -global --depth 0'

## C++
alias w++17='g++ -std=c++17 -Wall -Wextra -Wpedantic'

# Load Angular CLI autocompletion
#-----------------------------------------------------------------------------------------------------------
source <(ng completion script)
```
