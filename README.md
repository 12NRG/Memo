# How to Save past GNU screen output to a file

```
One way to do it is to use copy mode to copy the entire scrollback history, then dump it into a file. (There is likely a better way.)

With default keybindings, this would be something like:
```
- Ctrl-A to send screen a command
- [ to enter copy mode
- g to go to the top
- Space bar to mark the beginning of the scrollback buffer (where you are) as the start of the text to be copied
- G to go to the end
- Enter to mark the end of the text to be copied, and copy it.
- Then open up vim, run :set paste to avoid issues with e.g. auto-indentation, and then use Ctrl-A ] to paste.
