+++
title = 'Over The Wire - Bandit 2 -> 3'
date = 2024-08-06T17:51:53+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task 

Read the content of the file called "spaces in this filename".

# Login

SSH: `bandit2@bandit.labs.overthewire.org -p 2220`

Password: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

# Theory

We can't read a file that has a space in his filename normally. To read it we can simply put the name of the file between quotes `"filname"` and then we can read it.

# Solution

1. Log in to the remote host with the credentials from the last level.

```
~$: ssh bandit2@bandit.labs.overthewire.org -p 2220
```

2. Search for the file and read his content.

```
bandit2@bandit~$: ls
spaces in this filename

bandit2@bandit~$: cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

We can not move to the next challenge.
