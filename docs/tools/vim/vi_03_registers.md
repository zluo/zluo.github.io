---
layout: default
title: Vim Registers
nav_order: 3
parent: Vim
grand_parent: Tools
---

### List Register History


#### Show Registers
    :reg

#### Yank Registers
    "0

#### Unnamed Register
    ""

#### Named Register
    "[a-z]

#### BlackHome Register
    "_

#### Clipboard Register
    "+ / "*

#### Paste In Command Line
    CTRL + R {register}

#### Paste in Insert Mode
    CTRL + R {register}

#### Copy a Register
    :let @a=@""

#### The Expression Regist "=

    :%s/word/\=@a/g

#### More Registers
    "%  Name of the current file
    "#  Name of the alternate file
    ".  Last insert text
    ":  Last Ex command
    "/  Last Search pattern




































































