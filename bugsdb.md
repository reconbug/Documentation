# Bugs list

## Tmux

### Backspace not working

### Solution

After giving up the first time, I've tried again. The problem did not have to do with zsh:

The solution was putting

set -g default-terminal "xterm-256color"
in my tmux.conf