---
layout: post
title:  "Stack Setup"
date:   2019-12-26 
categories: Basic
---

I will be doing quite a bit of coding, especially in machine learning, so it would be a good place for me to blog what I believe would be the most basic setup for someone to get started on a fresh computer.

Additional Setup Step for Mac
My computer is a Mac, so there is one more step! Homebrew!! (Or use the code below in your terminal)

> /usr/bin/ruby -e “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)”

After installing homebrew, just use brew to install Git, Sublime, and everything else.

## Basic Installs
Before you even decide on what stack you would want to go with (Given that you have very little to no programming experience.) I think you should get the following:

1. Github (Or equivalence such as Bitbucket.)
2. Sublime [1] (Or equivalence such as Atom or VSCode.)
    * Vim doesn’t count.
3. Postgres (Or equivalence such as MySQL or MongoDB.)
Now on to the language of your choice! I went with Python3 and JavaScript. Anything after this would be whatever you want! (AKA building your OWN stack.)

The next thing is to link your ~/.bashrc with your ~/.bash_profile so you could just update one main bash file for all of your custom commands in case you have to access both login and non-login terminal on your Mac.

To make your life easier, you may also want to add

> subl

as a command to launch sublime with this tutorial.

Lastly, SSH! If you want a more secure way to communicate with a server without typing in password. 🙂

## Python Customization
If you are new to Python, I suggest you go straight into Python 3. Here is a pretty good intro on what you’d need for the setup. I’ve also installed some of the sublime plugins following this tutorial and this post, however, YMMV. If you are coding in Python 2, DON’T remove the pre-installed python and install python via brew. [2]

## Reference
1. https://www.codementor.io/mattgoldspink/best-text-editor-atom-sublime-vim-visual-studio-code-du10872i7
2. http://docs.python-guide.org/en/latest/starting/install/osx/
