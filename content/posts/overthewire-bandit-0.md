+++
title = 'Over The Wire - Bandit 0'
date = 2024-08-04T19:47:52+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Introduction

OverTheWire is a free online platform “to learn and practice security concepts in the form of fun-filled games”. It has different, so-called “Wargames”, that deal each deal with an area of security.

The first game that is recommended is called Bandit. It is recommended first because it teaches “the basics needed to be able to play other wargames”. This includes mainly basic Linux and Git commands.

I worked through the levels and decided to write a walkthrough for my blog. There are already walkthroughs on the internet, from different persons and with different solutions. However, I still decided to publish mine, to at the very least get more comfortable with writing and maybe, since my explanations and thought processes may vary from other writers, help someone understand the solutions better. Also, this way future me has a reference to look back at.

I will try to explain the important concepts shortly, however, there is always a lot more we can learn about them. What the game and I would encourage you to do, is research on your own.

Great, now that you know what this article is about and why I am doing this, let’s start with the walkthrough of Level 0.

# Bandit Level 0

## Task 

Log into the level with SSH.

Server: `bandit.labs.overthewire.org`

Port: `2220`

Username: `bandit0`

Password: `bandit0`

## Theory

This challenge wants us to user SSH, which stands for Secure Shell, is a cryptographic network protocol used to securely access and manage network devices and servers over an insecure network. It provides a secure channel over an unsecured network by using encryption to protect the communication between the client and the server.

Key features of SSH include:
    - Secure Remote Login: Allows users to securely log into a remote machine.
    - Command Execution: Enables users to run commands on a remote server.
    - File Transfer: Facilitates secure file transfers through protocols like SCP (Secure Copy Protocol) and SFTP (SSH File Transfer Protocol).
    - Port Forwarding: Supports tunneling of network services over a secure connection.

SSH helps ensure that data transmitted between the client and server remains confidential and protected from eavesdropping and tampering.

It is a very common service. So common in fact that it was assigned its own standard port, Port 22. A port is an endpoint that allows your computer to know which service should be accessed - kind of like office room numbers, so you know in which room the person you need to talk to is.

## Solution

To solve this challenge first we SSH into the remote machine with the credentials in the Level Goal.

```
~$ ssh bandit0@bandit.labs.overthewire.org -p 2220
```

After typing the password we're in and this is the end of the level 0.
