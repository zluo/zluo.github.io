---
layout: default
title: Copy and Paste
nav_order: 2
parent: Vim
grand_parent: Tools
---

## Copy(Yank) and Paste

### Paste from clipboard 

- Paste from clipboard

    `"``+``p`

**Register To Buffer**

    "ay

**Paste from Buffer**

    "ap

**Pasting into Command-Line Mode**
    
    "ayw
    CTRL + R, a
    
    yw
    CTRL + R , 0  // YANK Register
    
    CTRL + R , "  // Unnamed Register

**Copy Current word to Command Line**

    CTRL + R, CTRL + W

**Paste in a new Line**

    o<Alt + p>

**List paste buffers**

    :reg


### Macro

    #start macro
    qa

    #stop macro
    q

    #apply macro
    @a

Also see [vim registers](../vi_03_registers)

