---
layout: default
title: Vim Mode
nav_order: 4
parent: Vim
grand_parent: Tools
---

### Normal Mode
normal mode equivelent to a loop

    [range]normal A;

### Insert Mode
    C-h     Delete back one character(backspace)
    C-w     Delete back one word.
    C-u     Delete back to start of line
    C-r0    Paste without leave insert mode.
    C-p     Complete word typed before.

    C-a     paste previous insert
    C-@     paste previous insert, exit insert mode
    


### Visual Mode
Visual Mode allow us define a selection and then operate upon it.

    v       //character wise
    V       //line wise
    C-v     //block wise
    gv      //previous selction
    o       //go to other end of highlighted text