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

With main user of the pc (e.g., ares, dodo, zeus) do:
```sh
wget MINICONDA_LINK
bash MINICONDA.sh
sudo chgrp -R GROUP PATH_TO_CONDA
sudo chmod 770 -R PATH_TO_CONDA
```

On normal user do:
```sh
export PATH="PATH_TO_CONDA/bin:$PATH" && exec bash
conda init
exec bash
```

### SSH Passwd-free connection

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

SSH config hosts:  
```
Host HOSTNAME
  HostName IP_ADDRESS
  User USERNAME
```
