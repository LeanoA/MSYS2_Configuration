# MSYS2_Configuration
My MSYS2 configuration. Installation, Proxy configuration. Useful commands.

MSYS2 is a minimalist linux/unix shell environment for Windows.

## Install

Do all the steps listed here: http://msys2.github.io/  
(troubleshooting guide here: https://github.com/msys2/msys2/wiki/MSYS2-installation )

## Set-up Proxy

Most corporate networks require [proxy authentication] before connecting to the Net. 
You can probably skip this section on your home PC.

### Edit .bash_profile
Go to your MSYS `$HOME` directory; in my case it's `C:\msys32\home\alexander`. 
Using a text editor, modify `.bash_profile` file as described below. 
Save it and then restart MSYS2 to apply the new settings.

```bash
#
# .bash_profile example
#
# Example proxy:
# export http_proxy=http://$USERNAME:$PASSWORD@proxy-server-name:1234
# Simpler example without username/password:
export http_proxy=http://proxy.cab.cnea.gov.ar:3128

export https_proxy=$http_proxy
export HTTP_PROXY=$http_proxy
export HTTPS_PROXY=$http_proxy
export ftp_proxy=$http_proxy
export rsync_proxy=$http_proxy
export no_proxy="localhost,127.0.0.1,localaddress,.*.cnea.gob.ar,*redmine.ctrad.control*,*cnea.gov.ar,.local"

# Oracle, Java, other apps
# export TNS_ADMIN="X:\Support"
# PATH="$PATH:/c/ProgramData/Oracle/Java/javapath"
# PATH="$PATH:/mingw32/bin:~/bin"
# PATH="$PATH:/d/apps/gnuplot/bin"  
# PATH="$PATH:/c/Program Files/Docker/Docker/Resources/bin"
# PATH="$PATH:/c/Users/$USER/AppData/Roaming/npm"
# PATH="$PATH:/c/Users/$USER/AppData/Roaming/cabal/bin"
# PATH="$PATH:/c/Program Files/Amazon/AWSCLI"   # and so on...
# export PATH

# git status on PS1 prompt
git_branch() {
     git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
export PS1="\[\e]0;\w\a\]\[\e[32m\]${HOSTNAME,,}:\[\e[33m\]\w\[\e[0m\]\[\033[35m\]\$(git_branch)\[\033[96m\]$\[\033[0m\] "

# more tweaks
LS_COLORS=$LS_COLORS:'di=0;37:' ; export LS_COLORS
alias az=autozip   #a handy script i keep in /opt/bin
#alias vi=vim
alias ls='ls -p'
alias ll='ls -l'
alias lt='ls -lptr|tail'
alias my='cd "/c/Users/alexander/Documents"'
alias h=history
#set -o vi
shopt -s checkwinsize
uname -a
cd $HOME
#screenfetch -E
```

## Install gcc y dgb

```bash
pacman -Syu mingw-w64-x86_64-gcc
pacman -Syu mingw-w64-x86_64-gdb
```

test if it is installed

```bash
g++ --version
gdb --version
```
## Using g++ and gdb with VScode

Select g++ compliler.
- Check or modify `miDebuggerPath` line in `lauch.json` file: `"miDebuggerPath": "C:\\msys64\\mingw64\\bin\\gdb.exe".`
- Check or modify `command` line in `task.json` file: `"command": "C:\\msys64\\mingw64\\bin\\g++.exe"`

For more information, visit https://code.visualstudio.com/docs/languages/cpp.


## Disclaimer

This document is provided for information only, no guarantees. I have no association with MSYS2 or related projects.
