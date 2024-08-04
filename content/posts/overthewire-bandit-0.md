+++
title = 'Over The Wire - Bandit 0'
date = 2024-08-04T15:45:39+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Introduction

[OverTheWire](https://overthewire.org/wargames/) is an online platform that provides a series of interactive war games designed to teach and challenge users in various aspects of cybersecurity, programming, and systems administration. These war games cover a diverse range of topics, from basic Linux command line usage to complex cryptography and network exploitation techniques.

# Bandit 0

## Level Goal

The goal of this level is for you to log into the game using SSH. The host to which you need to connect is `bandit.labs.overthewire.org`, on port `2220`. The username is `bandit0` and the password is `bandit0`.

## Theory

1. Introduction to SSH:
    - Definition: SSH or Secure Shell, is a cryptographic network protocol used for secure data communication, remote command-line login, and other secure network services between two networked computers.
    - Purpose: It ensures that the data sent over the network is encrypted, providing confidentiality and integrity of data and secure authentication.
2. Understanding SSH Authentication:
    - Authentication mechanisms: SSH supports various authentication methods, including password-based authentication, public key authentication and host based authentication. For this level, the focus is on password-based authentication.
    - Process: WHen using password-based authentication, the client provides a username and password, which the server verifies. If the credentials are correct, access is granted.
3. Connecting to a Remote Host Using SSH:
    - Basic Command Structure: The basic syntax for connection to a remote host via SSH is:
    ```bash
    ssh [username]@[hostname] -p [port]
    ```
    - Parameters:
        - `username`: The username you are logging in with.
        - `hostname`: The remote host’s address (in this case, bandit.labs.overthewire.org).
        - `port`: The port number to connect to (in this case, 2220).
4. Common Pitfalls and Troubleshooting:
    - Incorrect Credentials: Ensure that you are using the correct username and password. Typos can lead to authentication failures.
    - Firewall and Network Issues: Ensure that your network allows outbound connections on port `2220`. If you are behind a restrictive firewall, you might need to adjust your network settings.

## Solution

To solve this level simply SSH into the remote host with the credentials given in the level goal and find the password for the next level.

```
~$ ssh bandit0@bandit.labs.overthewire.org -p 2220

~$ ls
readme

~$ cat readme
Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

Password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If

