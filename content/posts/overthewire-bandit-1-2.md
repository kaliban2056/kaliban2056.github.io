+++
title = 'Overthewire Bandit 1 2'
date = 2024-08-04T20:08:05+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task 

Read the content of the file called "-"

SSH: `bandit1@bandit.labs.overthewire.org -p 2220`

Password: `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

# Theory

To read a file with an "unconventional name" such as - we need to use the path of the file `./`.

# Solution

1. We log in to the remote host with the right credentials

```
~$: ssh bandit1@bandit.labs.overthewire.org -p 2220
```

2. Search for the file and read it.

```
bandit1@bandit~$: ls 
-

bandit1@bandit~$: cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

We can now proceed to the next challenge.
