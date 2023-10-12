---
layout: default
title: navigating
nav_order: 10
parent: Vim
grand_parent: Tools
---

### 3 Vim Tips

#### repeat last


#### repeat last operation

    .

#### repeat last selection

    gv

#### repeat last replacement

    %s/aaa/~

#### Return to previous cursor position**

    ''

#### Increment/Decrement a number

    Ctrl + a , Ctrl + x

#### Switch Cases

    Make The First Letter Of Every Word From Line 18 To 43 Uppercase

    : :18,43s/\<./\u&/g

#### Insert characters repeatly

    Esc 80i- Esc

#### Comment multiple lines

    Ctrl + v
    Shift + i  (I)
    #
    Esc

#### Insert Result Of An External Command

    : read !date

#### Insert A Calculation

    Ctrl + r = 2+2

#### Windows Layout and Navigation (:help ^w)

    Ctrl + w    windows command

#### Rotate windows

    Ctrl + w + r

#### Rotate cursor between windows

    Ctrl + w + w


#### Switch Vim to Command Line

   Ctrl + z
   fg      //come back to vim

#### Move current cursor to

  ''     previous cursor position

  Ctrl-O  jump to last (older) cursor position

  z + z // middle of screen

  z + t top of screen

  z + b bottom of screen


#### Foldering

  z + c //close foldering
  z + a //toggle foldering
  z + o // open foldering
  z + r // reduce more level
  z + m // foldering more level


#### Batch Delete Lines

    :g//d


