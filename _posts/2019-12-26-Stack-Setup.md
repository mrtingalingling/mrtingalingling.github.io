---
layout: post
title:  "Stack Setup"
date:   2019-12-26 
categories: Basic
---

This post is intended to be a step to step reference for setting up a fresh Mac or Linux machine for development.

#### Additional Setup Step for Mac
My computer is a Mac, so there is one more step! **Homebrew!!** (Or use the code below in your terminal)

> /usr/bin/ruby -e “$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)”

After installing homebrew, just use brew to install Git, VS Code, and everything else.

## Basic Installs
Before you even decide on what stack you would want to go with (Given that you have very little to no programming experience.) I think you should get the following:

1. Github (Or equivalence such as Bitbucket.)
```
sudo apt install git
mkdir ~/git && cd ~/git
git config --global user.name "Your name"
git config --global user.email "Your email address"
# This is optional, but I like to remove remote branches automatically.
git config --global fetch.prune true
```

2. SSH
Enable SSH: 
```
sudo systemctl start ssh
sudo systemctl enable ssh
```
**Google how to make keys!**
If you will have services that need to use your keys (I would recommend to prepare a different set of keys with limited privilage.) You could also save your keys in keychain, 
```
keychain --agents
source .keychain/`hostname`-sh
keychain --eval
eval `keychain --eval`
```
In your local environment, I'd also recommend you to setup keyforwarding in **~/.ssh/config**, 
```
Host $IPs
     User $YOUR_USERNAME
     ForwardAgent yes
     HostKeyAlgorithms +ssh-dss
```
Lastly, SSH! If you want a more secure way to communicate with a server without typing in password. 🙂

3. Python 
In whichever environment, it's best-practice to not depend on system python for development or production scripts. Therefore, it's highly recommended to install [miniconda](https://docs.conda.io/en/latest/miniconda.html) as listed below.
#### Linux
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p ~/miniconda3
```
#### Mac
```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-MacOSX-x86_64.sh
bash Miniconda3-latest-MacOSX-x86_64.sh -b -p ~/miniconda3
```
#### For both versions, initialize and setup .bash_profile after the installation.
```
source ~/miniconda3/bin/activate && conda init
```
Log out and log back in and miniconda will be your default python.

If, for some reason you get the error `ERROR: cannot verify repo.anaconda.com's certificate` using wget, you can probably run:
> curl -o Miniconda3-latest-Linux-x86_64.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh

#### Python Virtual Environment
***BEFORE YOU START: Create a virtual environment***
You can save it anywhere, I would recommend doing it within the git directory, 
```
mkdir -p ~/git/.venv && python3 -m venv $REPO_venv
source ~/git/.venv/REPO_venv/bin/activate
```

I would also recommend setting up alias in your ~/.bashrc (Or .bash_profile) and/or create a bash script in ~/, 
```
#!/bin/bash

. /home/`whoami`/.keychain/`hostname`-sh

# >>> conda initialize >>>
# !! Contents within this block are managed by 'conda init' !!
__conda_setup="$('/home/`whoami`/anaconda3/bin/conda' 'shell.bash' 'hook' 2> /dev/null)"
if [ $? -eq 0 ]; then
    eval "$__conda_setup"
else
    if [ -f "/home/tto/`whoami`/etc/profile.d/conda.sh" ]; then
        . "/home/tto/`whoami`/etc/profile.d/conda.sh"
    else
        export PATH="/home/`whoami`/anaconda3/bin:$PATH"
    fi
fi
unset __conda_setup
# <<< conda initialize <<<

# Custom Setting
export ORACLE_HOME="/opt/oracle/instantclient"
export LD_LIBRARY_PATH=$ORACLE_HOME:$LD_LIBRARY_PATH
export PATH=$PATH:$ORACLE_HOME:$LD_LIBRARY_PATH

cd /home/`whoami`/Envs/$1
source $1"_venv/bin/activate"
```

### Remote Servers (VPS) 
***If it's on a remote server, Setup the firewall and other security measures!***
Coming Soon! 

1. Docker 
##### Follow the instructions on the [docker ubuntu page](https://docs.docker.com/install/linux/docker-ce/ubuntu/):
```
sudo apt-get update
sudo apt-get install apt-transport-https ca-certificates curl gnupg-agent software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

##### Follow the [post-installation instructions](https://docs.docker.com/install/linux/linux-postinstall/):
```
sudo groupadd docker
sudo usermod -aG docker $USER
# You'll need to log out and log back in for the permissions to take effect.
```

#### Disable apparmor, otherwise you might have trouble killing docker containers[3]:
```
sudo systemctl disable apparmor.service --now
sudo service apparmor teardown
sudo systemctl restart docker
```

2. Database - Postgres (Or equivalence such as MySQL or MongoDB.)
```
sudo apt install postgresql-client
```
Now on to the language of your choice! I went with Python3 and JavaScript. Anything after this would be whatever you want! (AKA building your OWN stack.)


### Editor 
VSCode [1] (Or equivalence such as Atom or Sublime.)
    * Vim doesn’t count.
    * I personally recommend VSCode especially if you are like me, coding from a 2015 Mac Air to the VSP. 
        * Check out [Vultr](https://www.vultr.com/?ref=8353147) or [Linode](https://www.linode.com/?r=bdc2269637cd5a93fb87c69634de596292799f99)


The next thing is to link your ~/.bashrc with your ~/.bash_profile so you could just update one main bash file for all of your custom commands in case you have to access both login and non-login terminal on your Mac.

If on Mac, you may also want to [add the code command to your PATH](https://code.visualstudio.com/docs/setup/mac). 


## Python Customization
If you are new to Python, I suggest you go straight into Python 3. Here is a pretty good intro on what you’d need for the setup. I’ve also installed some of the sublime plugins following this tutorial and this post, however, YMMV. If you are coding in Python 2, DON’T remove the pre-installed python and install python via brew. [2]

#### Additional Python setup 
Every language has their own style, the most common styles for python are Black and Flake8, so installing them as your linters would be a good start, 
```
pip install black flake8
```


## Additional Reference
1. https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-on-linux

[1]: https://www.codementor.io/mattgoldspink/best-text-editor-atom-sublime-vim-visual-studio-code-du10872i7
[2]: http://docs.python-guide.org/en/latest/starting/install/osx/
[3]: https://forums.docker.com/t/can-not-stop-docker-container-permission-denied-error/41142
