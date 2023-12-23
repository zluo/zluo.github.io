---
layout: default
title: Command Line Editing
nav_order: 3 
parent: Linux Command 
---
## Bash Command Line Editing

### Readline Init File Location

- global
    
    /etc/inputrc

- local
  
   ~/.inputrc

### Moving

| ShortCut | Description |
|-----|--|
|Ctrl + a (Home)|Move to the start of the line|
|Ctrl + e (End)|More to the end of the line|
|Ctrl + f|Move forward a character|
|Ctrl + b|Move back a character|
|Alt + b |Back(Left) one word|
|Alt + Ctrl + b |Back(Left) one word|
|Alt + Ctrl +  f |Forward (right) one word|

### History Operations
| ShortCut | Description |
|-----|--|
|Ctrl + p (Up arrow)|Previous command|
|Ctrl + n (Down arrow)|Next command|
|Ctrl + g|Escape from history searching mode|
|Ctrl + o|Execute the command found via Ctrl + r or Ctrl + s|
|Ctrl + c|Interrupt/Kill whatever you are running (SIGINT)|

### Case Sensitive
| ShortCut | Description |
|-----|--|
|Alt + c | Capitalize the character under the cursor and move to the end of the word|
|Alt + l | Lower the case of every character from the cursor to the end of the current word|
|Alt + u | Upper the case (capitalize) of every character from the cursor to the end of the current word.|

### Copy paste
| ShortCut | Description |
|-----|--|
|Ctrl + k|Cut the line after the cursor to the clipboard|
|Ctrl + w|Cut the word before the cursor to the clipboard|
|Ctrl + u|Cut/delete the line|
|Ctrl + y (yank)|Past the last thing to be cut|
|Ctrl + h (backspace)|Delete character before the cursor|
|Ctrl + d|Delete character under the cursor|
|Alt  + d|Delete the word after the cursor|
|Alt + Del|Delete the word before the cursor|
|Alt + r | Cancel the changes and put back the line as it was in the history (revert)|

### Screen Operations

| ShortCut | Description |
|-----|--|
|Ctrl + s|Pause terminal output|
|Ctrl + q|Release paused output|
|Ctrl + L|Clear the screen|


| ShortCut | Description |
|-----|--|
|Ctrl + r|Recall the last command including the specified characters(s)|
|^abc^def|Run previous command, replacing abc with def|
|Ctrl + D|Send an EOF marker, unless disable by an option, this will close the current shell (EXIT)|
|Ctrl + z|Send the signal SIGTSTP to the current task, which suspends it|
|Ctrl + s|Stop output to the screen (for long running vervose commands)|
|Alt + t|Swap current word with previous|
|Ctrl + t|Swap the last two characters before the cursor|
|Esc + t|Swap the last two words before the cursor|
|Tab|Tab completion for file/directory names|
|Ctrl + xx| Toggle between the start of line and current cursor position|
|Ctrl + _| Undo |

## Running Commands
| ShortCut | Description |
|-----|--|
|!*  | All arguments of previous command |
!^   | first argument from previous command|
|!$  |Last argument of previous command|
|!:n-m  |The Nth-Mth argument of previous command|
|!!:n |where n is the 0-based position of the argument you want.|
|!n | command number n from history |
|!pattern | most recent command matching pattern |
|!!:s/find/replace | last command, substitute find with replace|
|!!|Repeat the last command|
|!abc:p|Print last command starting with abc|
|!abc|Run the last command starting with abc|

1.  All arguments of previous command (!*)

```bash
$ mkdir one two three
$ chmod 700 !*
```
---
### References
[Documentation](https://www.gnu.org/software/bash/manual/bash.html#Command-Line-Editing)