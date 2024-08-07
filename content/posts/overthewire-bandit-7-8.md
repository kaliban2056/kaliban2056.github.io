+++
title = 'Over The Wire - Bandit 7 -> 8'
date = 2024-08-07T17:01:48+02:00
draft = false
tags = ["cyber security", "bandit", "over the wire"]
+++

# Task 

The password for the next level is stored in the file `data.txt` next to the word `millionth`.

# Login

SSH: `bandit7@bandit.labs.overthewire.org -p 2220`

Password: `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

# Theory

To solve this level and move one we just need to use one command, the `grep` command scan search

# Solution

grep "millionth" data.txt
millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
