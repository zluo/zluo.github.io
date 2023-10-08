---
layout: default
title: Navigating
nav_order: 1 
parent: Vim
grand_parent: Tools
---

#### Basic Move

    h   move left
    l   move right
    j   move down
    k   move up

    gj/gh/gk/gl when lines wrap

    - upward
    +  (CTRL + M) downward
    

#### Move between words
    w   move to beginning of next word (ctrl + right)
    b   move to previous beginning of word
    e   move to end of word
    W   move to beginning of next word after a whitespace
    B   move to beginning of previous word before a whitespace
    E   move to end of word before a whitespace
    ge  backward to the end of word.

{: .note }
movements can be preceded by a count. e.g. `4j` moves down 4 lines.


#### Move to begin | end of the line
    0   move to beginning of line
    $   move to end of line

#### Move to begin | end of file

    gg  move to first line
    G   move to last line
    ngg / nG move to n'th line of file (n is a number; 12gg moves to line 12)


#### Move Cursor

    H   move to top of screen
    M   move to middle of screen
    L   move to bottom of screen

    z<CR> move cursor to top of screen
    zz  scroll the line with the cursor to the center of the screen
    zt  scroll the line with the cursor to the top of the screen
    zb  scroll the line with the cursor to the bottom



    Ctrl-D  move half-page down
    Ctrl-U  move half-page up
    Ctrl-B  page up
    Ctrl-F  page dow
    Ctrl-O  jump to last (older) cursor position
    Ctrl-I  jump to next cursor position (after Ctrl-O)
    Ctrl-Y  move view pane up
    Ctrl-E  move view pane down

#### Search Navigating

    n   next matching search pattern
    N   previous matching search pattern
    *   next whole word under cursor
    =   previous whole word under cursor
    g*  next matching search (not whole word) pattern under cursor
    g=  previous matching search (not whole word) pattern under cursor
    gd  go to definition/first occurrence of the word under cursor
    
    fX  to next 'X' after cursor, in the same line (X is any character)
    FX  to previous 'X' before cursor (f and F put the cursor on X)
    tX  til next 'X' (similar to above, but cursor is before X)
    TX  til previous 'X'
    ;   repeat above, in same direction
    ,   repeat above, in reverse direction

#### Jumps

    %   jump to matching bracket { } [ ] ( )
    ()  move between sentences.
    {}  move between paragraphs.

    ]]  forward to the next '}' in the first column.
    ][  forward to the next '{' in the first column.
    [[  backward to the next '{' in the first column.
    []  backward to the next '}' in the first column.

### switch between tabs
    g t
    g T
    n g t