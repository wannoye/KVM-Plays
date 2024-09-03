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

- An admin username and password assigned to the 'ansible_user' and 'ansible_become_pass' vars in "group_vars/all.yml"

### Usage:

```ansible-playbook update.yml -i inventory --ask-vault-pass```

## "setup_user.yml" Ansible Playbook

Creates a new administrator user on target systems with a home directory.<br/>
For ease of use with Ansible, the account will not require a password for sudo privlege.<br/>
SSH keys are created on the local device and pushed to remote servers.<br/>
Works with Debian and RedHat based linux servers.

### Requires:

- The following variables assigned in "group_vars/all.yml":<br/>
    - An admin username and password assigned to the 'ansible_user' and 'ansible_become_pass' vars<br/>
    - An account name to be created assigned to the 'new_user' var<br/>
    - A password for the new user assigned to the 'user_pass' var<br/>

Note: A hashed password string can be created with the command 'mkpasswd -m sha512crypt'.

### Usage:

```ansible-playbook setup.yml -i inventory --ask-vault-pass```

## "install_cockpit.yml" Ansible Playbook

Installs the Cockpit management console and nessessary components.<br/>
Where needed, firewall rules are created to allow access.<br/>
The 'cockpit-machines' package is installed if a KVM hypervisor is identified.<br/>
Works with Debian and RedHat based linux servers.

### Requires:

- An admin username and password assigned to the 'ansible_user' and 'ansible_become_pass' vars in "group_vars/all.yml"

### Usage:

```ansible-playbook install_cockpit.yml -i inventory --ask-vault-pass```

## "install_docker.yml" Ansible Playbook

Installs the Docker service and any needed dependencies.<br/>
A 'docker' group is created and users are added to allow non-superuser administration.<br/>
Works with Debian and RedHat based linux servers.

### Requires:

- An admin username and password assigned to the 'ansible_user' and 'ansible_become_pass' vars in "group_vars/all.yml"

### Usage:

```ansible-playbook install_docker.yml -i inventory --ask-vault-pass```

## "mount_cifs_shares.yml" Ansible Playbook

Mounts CIFS shares as defined by the 'cifs_server' and 'cifs_share' vars in group_vars/all.yml.<br/>
The 'cifs-utils' package will be installed and mount points created at '/mnt' if missing.<br/>
Works with Debian and RedHat based linux servers.

### Requires:

- The following variables assigned in "group_vars/all.yml":<br/>
    - An admin username and password assigned to the 'ansible_user' and 'ansible_become_pass' vars<br/>
    - A username and password assigned to the 'cifs_user' and 'cifs_pass' vars<br/>
    - An IP or Server name assigned to the 'cifs_server' var<br/>
    - One or more share names assigned to the 'cifs_share' var list<br/>

Note: The CIFS account must already exist both locally and remote.

### Usage:

```ansible-playbook mount_cifs_shares.yml -i inventory --ask-vault-pass```