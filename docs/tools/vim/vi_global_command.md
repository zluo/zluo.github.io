---
layout: default
title: navigating
nav_order: 999
parent: vim
grand_parent: tools
---

the :glocal command allows us to run an ex command on each line that matches a pattern

    :[range]global[!]/{pattern}/[cmd]

{pattern} integrate with search history

### Find all occurrences of current word
    g*
    g#

### change all to uppercase
    gU{motion}     //Upper Case
    g~{motion}     //Swap Case
    gu{moion}     //Lower Case
    gUgn          //UpperCase find pattern

### Normal Mode
normal mode equivelent to a loop

    [range]normal A;

### Previous Selection in Virtual Mode

    gv

### Switch between Tabs
    gt
    gT

### Copy all lines matching a pattern to register 'a'

    qaq:g/pattern/y A

NOTE: qaq clean register a, A (append to register a)

### Display 5 lines for all occurences of a pattern


    %s/aaa/bbb/g




