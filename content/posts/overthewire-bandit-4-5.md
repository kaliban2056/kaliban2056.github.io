+++
title = 'Over The Wire - Bandit 4 -> 5'
date = 2024-08-07T11:50:31+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task 

Find the only human-readable file inside the `inhere` directory.

# Login

SSH: `bandit4@bandit.labs.overthewire.org -p 2220`

Password: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

# Theory

To find what file is human-readable we can check the type of data inside the file. To do that we can use the `file` command, some examples would be: `ASCII text`, `directory`, `POSIX tar archive`. Trying to read a non human-readable file would show something like this in the output `l�����]�a߯-@gQ�÷�wz�P�ߠy�`.

# Solution

1. SSH in to the remote host again and go to the inhere directory.

2. Use the file command to find what file is human-readable and read his content.

```
~$: ssh bandit4@bandit.labs.overthewire.org -p 2220

bandit4@bandit~$: cd inhere
bandit4@bandit~$: file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data

bandit4@bandit~$: cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

This is the password for the text level.
