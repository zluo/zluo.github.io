---
layout: default
title: tmux
nav_order: 4
has_children: true
permalink: /docs/tools/tmux
parent: Tools
---
## Tmux note


1. Session
--------------------------------------------------------------------------------
The advantage of session is that it will span multiple command terminal. 

  **1.1 Create Session**

      tmux new -s <name>

  **1.2 List Session**

      Prefix s
      
      tmux ls

  **1.3 Detach Session**

  **1.4 Attach Session**

      tmux a -t <name>

  **1.5 Delete Session**

      tmux kill-session -t <name>
  
  **1.6 Rename Session**
  
      Prefix $
  **1.7 Switch Sessions**
  
      Prefix ( previous session
      Prefix ) next session
      Prefix L 'last' session
      Prefix s select a session

2. Window
--------------------------------------------------------------------------------
windows is the shells within a session

  **2.1 Create window**

      Prefix c

  **2.2 List windows**

      Prepl.itrepl.itrefix w

  **2.4 navigate windows**

      Prefix <window number>

      Prefix p (previous window)

  **2.5 close windows**

   <pre> Prefix &</pre>

  **2.6 find windows**

      Prefix f

  **2.7 rename window**

      Prefix ,

3. Pane

  **3.1 splite windows**

      Prefix %
      Prefix "

  **3.2 navigate panes**

      Prefix <Arrow>
      Prefix o

  **3.3 pane layout**

      Prefix p

  **3.4 full screen**

      Prefix z

  **3.5 resize pane**

      Prefix CTRL <ARROW>

  **3.5 close pane**

      exit

  **3.6 swap pane**

      Prefix {

  **3.7 merge two windows into pane**

      join-pane -s 2 -t 1 -h

  **3.8 move current pane to a new window**

      Prefix !

  **3.9 rearrange**
  
      Prefix <space>
