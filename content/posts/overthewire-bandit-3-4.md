+++
title = 'Over The Wire - Bandit 3 -> 4'
date = 2024-08-07T11:40:36+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task 

Find and read the content of the hidden file in the `inhere` directory.

# Login

SSH: `bandit3@bandit.labs.overthewire.org -p 2220`

Password: `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

# Theory

To find an hidden file in a linux filesystem is really easy, we can use the `ls` command to list every file in the directory adding to it the `-a` attribute to list hidden files too. They are commonly used for storing user preferences or preserving the state of a utility and are frequently created implicitly by using various utilities.

# Solution

1. SSH in to the remote host with the above credentials.

```
~$: ssh bandit3@bandit.labs.overthewire.org -p 2220
```

2. Go inside the `inhere` directory and list all files to read the content of the hidden one.

```
bandit3@bandit~$: cd inhere
bandit3@bandit~$: ls -a 
. .. ...Hiding-From-You

bandit3@bandit~$: cat ...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

3. Use this password to log to the next level.
