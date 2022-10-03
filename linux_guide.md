# PINLab Linux Guide

## Create user

```sh
# create user with name USERNAME (e.g. paolo)
# GROUP_NAME corresponds to the name of the pc (e.g. ares)
sudo useradd -g GROUP_NAME -G sudo -m -s /bin/bash USERNAME

# set user password in order to be able to access
sudo passwd USERNAME

# remember to change the host in your ssh command with the new username
```


## Conda

### Installing miniconda

With main user of the pc (e.g., ares, dodo, zeus) do:
```sh
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh
bash ~/miniconda.sh
rm ~/miniconda.sh
sudo chgrp -R GROUP PATH_TO_CONDA
sudo chmod 770 -R PATH_TO_CONDA
```

On normal user do:
```sh
export PATH="PATH_TO_CONDA/bin:$PATH" && exec bash
conda init
exec bash
```

### Cloning old environments

Due to changes in the path of the conda environments, copy and pasting the old env folder into the new directory does not fully work.
The best solution is to export the old environment into a `yaml` file and then creating a new one.

Export and remove the old environment:
```sh
conda activate ENV_NAME
conda env export --no-builds > env.yml
conda remove --name ENV_NAME --all
```

Create the new environment:
```sh
conda env create -f env.yml
```

## SSH

### Passwd-free connection

Create a ssh key on your laptop (linux) if you don't have one:
```sh
ssh-keygen -t ed25519 -C "your_email@example.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

Copy public key to the workstation:
```sh
ssh-copy-id -i ~/.ssh/id_ed25519.pub REMOTE_HOST
```

SSH config hosts by adding the following to `~/.ssh/config`:  
```
Host HOSTNAME
  HostName IP_ADDRESS
  User USERNAME
```
