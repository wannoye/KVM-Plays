# KVM Automation Scripts

## "vm_prep.py" Python Script

Created to prep a KVM host and create a new VM.<br/>
The script can accomplish the following tasks:

- Remove a logical volume
- Extend a logical volume
- Create a logical volume
- Format a logical volume
- Mount a file system
- Unmount a file system
- Create a new virtual machine

The main menu prompts the user to select a task.<br/>
Subsequent prompts guide the user through completion of each task.

### Requires:

- Python 3.6.9 or greater
- Change "vg", "mount_point", and "iso_dir" variables

### Usage:

```python3 vm_prep.py```

## "update.yml" Ansible Playbook

Updates Debian and RedHat based linux servers using the OS package manager.<br/>
Where possible, servers are rebooted after taking updates.<br/>
For out of date systems, this playbook can take quite a while to complete.

### Requires:

- A username and password for and administrator account in "group_vars/all.yml"

### Usage:

```ansible-playbook update.yml -i inventory --ask-vault-pass```

## "setup.yml" Ansible Playbook

Creates a new user as defined in group_vars/all.yml.<br/>
Administrator privilege is assigned so that a 'sudo' password is not required.<br/>
SSH keys are created on the local device and pushed to remote servers.

### Requires:

- A username and password for and administrator account in "group_vars/all.yml"
- An account name to be created and a hashed password string for the new user<br/>

Note: A hashed password string can be created with the command 'mkpasswd -m sha512crypt'.

### Usage:

```ansible-playbook setup.yml -i inventory --ask-vault-pass```

## "cockpit.yml" Ansible Playbook

Installs the Cockpit management console and nessessary components.<br/>
Where needed, firewall rules are created to allow access.<br/>
The 'cockpit-machines' package is installed if a KVM hypervisor is identified.

### Requires:

- A username and password for and administrator account in "group_vars/all.yml"

### Usage:

```ansible-playbook cockpit.yml -i inventory --ask-vault-pass```

## "docker.yml" Ansible Playbook

Installs the Docker service and any needed dependencies.<br/>
A 'docker' group is created and users are added to allow non-superuser administration.<br/>

### Requires:

- A username and password for and administrator account in "group_vars/all.yml"

### Usage:

```ansible-playbook docker.yml -i inventory --ask-vault-pass```

