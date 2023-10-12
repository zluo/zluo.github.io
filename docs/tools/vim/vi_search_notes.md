---
layout: default
title: search
nav_order: 5
parent: Vim
grand_parent: Tools
---

## Vim Notes - Searching


## Matching Patterns
### Setting Case Sensitivity per Search
    \c      ignore case.
    \C      force case sensitivity.

### Smarter Default Case Sensitivity
    if the pattern are all lowercase, is case insensitive
    if the pattern include upper case letters, is case sensitive.

### Use the \v Pattern Switch for Regex Searches


### Find character in current line
    f 
    F backward
     
    t a character before what you search
    T backward
    
    Repeat ; (forward), (backword)
    
### Search current word
    * (forward)
    # (backward)
    g* find all occurrences of current word

### Search using buffer value

    / ctrl + r + register name

### Disable Search Highlight
    :noh (no highlight)

### Global Search
    :g/pattern
    :g/vpattern     no escaping needed
    :g//            list search result
