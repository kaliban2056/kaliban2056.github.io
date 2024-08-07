+++
title = 'Over The Wire - Bandit 0 -> 1'
date = 2024-08-04T19:51:15+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task 

Find the file `readme` stored in the filesystem.

SSH: `bandit0@bandit.labs.overthewire.org -p 2220`

Password: `bandit0`

# Theory

After loggin in the remote host you can use a set of commands to understand where are you and what files are in your directory:
- `pwd` this command show the name of the working directory, the directory you're in right now.
- `ls` list the files in the current folder, you can add the attribute `-a` to show hidden files, using `-l` instead will show additional information on the files.
- `cat` read the content of a file and print them to standard output.

# Solution

1. We log in with SSH using the information above.

2. Make sure the `readme` file is in the directory.

```
bandit0@bandit:~$ ls 
readme
```

3. We can read the content of the file.
```
bandit0@bandit:~$ cat readme
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

Now we can move on to the next challenge.
