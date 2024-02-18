# 1. Automatization of a fresh Linux OS workstation

Ansible playbook created for smoother proccess of configuring a fresh workstation based from clean template.

# 2. Requirements
- Ansible 
- Distribution compatible with all of the packages mentioned bellow.

# 3. Features

- Installing multiple packages to a workstation with a single command.
- Possible configuration of said packages.

# 4. How to use
## 4.1. Install the Linux distribution of your choice on the target nodes.
In my example i chose Arch v6.7.2. And followed the official instalation guide adjusted to my preferrences.
- https://archlinux.org/download/
- https://wiki.archlinux.org/title/Installation_guide
## 4.2. Acquiring playbook on the control node

First we need to get the playbook (and it's additions), from this repository. Here is how we can do that:
```bash
# Select where you want to store the copy, your choice.
git clone https://github.com/Midiros/LTP_ansible
cd LTP
```

## 4.3. Choosing your target workstations (hosts)

Configure the hosts file with your chosen targets. You can target multiple workstations.

```md
[target]
X.X.X.X
X.X.X.X

```

# 5. Setting up connections
## 5.1. Enabling SSH
To use the playbook on the targets. We need to set up a connection. Using SSH.
```bash
sudo systemctl enable sshd
sudo systemctl start sshd
```
## 5.2. Generate SSH keys.
Generate an SSH key pair on the control node, and afterwards copy the public key to the target nodes. Create them in the .ssh folder in the root folder of user.

```bash
mkdir .ssh
cd .ssh

ssh-keygen

scp id_rsa.pub x.x.x.x:~/.ssh/authorized_keys 
```
## 5.3. Creating .env file
Create a .env file on the control node containing the password of the target node

## 5.4. Run the playbook itself
```bash
ansible-playbook ./main.yml -i ./hosts --become-password-file ./.env
```

# Additional adjustments
- There is the posibility of the jack2 and pipewire-jack packages colidding because of dependencies. Therefore it is required to install pipewire-jack manually

# Author

Playbook made by Midiros alas Adam Lenger.