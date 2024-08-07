+++
title = 'Over The Wire - Bandit 6 -> 7'
date = 2024-08-07T15:13:23+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task

The password for the next level is stored somewhere on the server and has all of the following properties:

- owned by user bandit7
- owned by group bandit6
- 33 bytes in size

# Login

SSH: `bandit6@bandit.labs.overthewire.org -p 2220`

Password: `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

# Theory

The process to solve this task is pretty similar to the previous level, we just need the `find` command with some different attribute, `-user [username]` searches for files owned by a specific user and `-group [groupname]` searches for files owned by a specific group.

# Solution

1. Log in to the remote machine with the credentials previously found.

```
~$: ssh bandit6@bandit.labs.overthewire.org -p 2220
```

2. To find the right file we will user the find command with some attributes:

```
bandit6@bandit~$: find / -type f -user bandit7 -group bandit6 -size 33c
...
find: ‘/etc/stunnel’: Permission denied
find: ‘/etc/multipath’: Permission denied
find: ‘/etc/sudoers.d’: Permission denied
find: ‘/etc/credstore.encrypted’: Permission denied
find: ‘/etc/ssl/private’: Permission denied
find: ‘/etc/credstore’: Permission denied
find: ‘/etc/xinetd.d’: Permission denied
find: ‘/etc/polkit-1/rules.d’: Permission denied
find: ‘/root’: Permission denied
find: ‘/tmp’: Permission denied
find: ‘/lost+found’: Permission denied
find: ‘/dev/shm’: Permission denied
find: ‘/dev/mqueue’: Permission denied
find: ‘/var/spool/bandit24’: Permission denied
find: ‘/var/spool/rsyslog’: Permission denied
find: ‘/var/spool/cron/crontabs’: Permission denied
find: ‘/var/lib/udisks2’: Permission denied
/var/lib/dpkg/info/bandit7.password
find: ‘/var/lib/snapd/void’: Permission denied
find: ‘/var/lib/snapd/cookie’: Permission denied
find: ‘/var/lib/ubuntu-advantage/apt-esm/var/lib/apt/lists/partial’: Permission denied
find: ‘/var/lib/private’: Permission denied
find: ‘/var/lib/update-notifier/package-data-downloads/partial’: Permission denied
find: ‘/var/lib/amazon’: Permission denied
...
```

To avoid this kind of output we can add a piece of code at the end of the command to suppress error messages:

```
bandit6@bandit~$: find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password

bandit6@bandit~$: cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

3. Now we can move to the next level.
