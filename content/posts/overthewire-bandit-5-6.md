+++
title = 'Over The Wire - Bandit 5 -> 6'
date = 2024-08-07T12:31:20+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task 

Find the only file that respect these requirements and read its content.

The requirements are: 
- human-readable
- 1033 bytes in size
- not executable

# Login

SSH: `bandit5@bandit.labs.overthewire.org -p 2220`

Password: `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

# Theory

To solve this task, we'll use a combination of basic Linux commands to search for and identify the file with the specified properties. Let's break down the key commands we'll be using:

`find` Command

The `find` command in Linux is a powerful tool that allows users to search for files and directories based on various criteria.

- `-find [path] [conditions]`: Basic syntax for the find command.
- `-type f`: This condition specifies that we are looking for regular files (not directories).
- `-size [size]`: Finds files of a specific size. The size can be specified in different units like bytes (c), kilobytes (k), etc. For our task, we'll use 1033c to specify 1033 bytes.
- `-executable`: Checks if a file is executable.
- `! -executable`: Ensures the file is not executable.

`xargs` Command

The `xargs` command is used to build and execute command lines from standard input. In our case, it can be used to perform actions on the results returned by the `find` command.

`file` Command

The `file` command is used to determine the type of a file. It can help verify if a file is human-readable.

# Solution

1. Log in to the host machine with the credentials above.

2. Take a look around for something interesting.

```
bandit5@bandit~$: ls 
inhere

bandit5@bandit~$: cd inhere
bandit5@bandit~/inhere$: ls -la
total 88
drwxr-x--- 22 root bandit5 4096 May  7  2020 .
drwxr-xr-x  3 root root    4096 May  7  2020 ..
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere00
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere01
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere02
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere03
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere04
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere05
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere06
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere07
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere08
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere09
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere10
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere11
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere12
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere13
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere14
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere15
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere16
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere17
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere18
drwxr-x---  2 root bandit5 4096 May  7  2020 maybehere19

bandit5@bandit~/inhere$: ls -la maybehere00
total 72
drwxr-x---  2 root bandit5 4096 May  7  2020 .
drwxr-x--- 22 root bandit5 4096 May  7  2020 ..
-rwxr-x---  1 root bandit5 1039 May  7  2020 -file1
-rwxr-x---  1 root bandit5  551 May  7  2020 .file1
-rw-r-----  1 root bandit5 9388 May  7  2020 -file2
-rw-r-----  1 root bandit5 7836 May  7  2020 .file2
-rwxr-x---  1 root bandit5 7378 May  7  2020 -file3
-rwxr-x---  1 root bandit5 4802 May  7  2020 .file3
-rwxr-x---  1 root bandit5 6118 May  7  2020 spaces file1
-rw-r-----  1 root bandit5 6850 May  7  2020 spaces file2
-rwxr-x---  1 root bandit5 1915 May  7  2020 spaces file3
```

We have a lot of files and folders to look through but we can use the commands mentioned in the theory to help us with this task.

```
bandit5@bandit~$: find . -type f -readable -size 1033c ! -executable
./maybehere07/.file2

bandit5@bandit~$: cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

3. Now we can log in to the next level.
