---
layout: default
title: Bash Terminal Shortcuts Keys
nav_order: 3 
parent: Linux Command 
---
## Bash Terminal Shortcuts Keys

1.  All arguments of previous command

    !*
```bash
$ mkdir one two three
$ chmod 700 !*
```


| ShortCut | Description |
|-----|--|
| !*  | All arguments of previous command |
|Alt +b |Back(Left) one word|
|Ctrl + q|Allow output to the screen (if previously stopped)|
|Alt + r |Cancel the changes and put back the line as it was in the history (revert)|
|Alt + c|Capitalize the character under the cursor and move to the end of the word|
|Ctrl + L|Clear the screen|
|Ctrl + k|Cut the line after the cursor to the clipboard|
|Ctrl + w|Cut the word before the cursor to the clipboard|
|Ctrl + u|Cut/delete the line|
|Ctrl + h (backspace)|Delete character before the cursor|
|Ctrl + d|Delete character under the cursor|
|Alt + d|Delete the word after the cursor|
|Alt + Del|Delete the word before the cursor|
|Ctrl + g|Escape from history searching mode|
|Ctrl + o|Execute the command found via Ctrl + r or Ctrl + s|
|Alt + f|Forward (right) one word|
|Ctrl + f|Forward one character|
|Ctrl + s|Go back to the next most recent command|
|Ctrl + a (Home)|Go to the beginning of the line|
|Ctrl + e (End)|Go to the end of the line|
|Ctrl + c|Interrupt/Kill whatever you are running (SIGINT)|
|!$|Last argument of previous command|
|Alt + l|Lower the case of every character from the cursor to the end of the current word|
|Ctrl + n (Down arrow)|Next command|
|Ctrl + y (yank)|Past the last thing to be cut|
|Ctrl + p (Up arrow)|Previous command|
|!abc:p|Print last command starting with abc|
|Ctrl + r|Recall the last command including the specified characters(s)|
|!!|Repeat the last command|
|^abc^def|Run previous command, replacing abc with def|
|!abc|Run the last command starting with abc|
|Ctrl + D|Send an EOF marker, unless disable by an option, this will close the current shell (EXIT)|
|Ctrl + z|Send the signal SIGTSTP to the current task, which suspends it|
|Ctrl + s|Stop output to the screen (for long running vervose commands)|
|Alt + t|Swap current word with previous|
|Ctrl + t|Swap the last two characters before the cursor|
|Esc + t|Swap the last two words before the cursor|
|Tab|Tab completion for file/directory names|
|Ctrl + xx|Toggle between the start of line and current cursor position|
|Ctrl + _|Undo|
|Alt + u|Upper the case (capitalize) of every character from the cursor to the end of the current word.|
|||
