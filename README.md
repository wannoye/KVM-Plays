# KVM Plays

## "update.yml" Ansible Playbook

Updates Debian and RedHat based linux servers using the OS package manager.<br/>
Where possible, servers are rebooted after taking updates.<br/>
For out of date systems, this playbook can take quite a while to complete.

### Requires:

- An admin username and password assigned to the 'ansible_user' and 'ansible_become_pass' vars in 'group_vars/all.yml'

### Usage:

```ansible-playbook update.yml -i inventory --ask-vault-pass```

## "setup_user.yml" Ansible Playbook

Creates a new administrator user on target systems with a home directory.<br/>
For ease of use with Ansible, the account will not require a password for sudo privlege.<br/>
SSH keys are created on the local device and pushed to remote servers.<br/>
Works with Debian and RedHat based linux servers.

### Requires:

- The following variables assigned in 'group_vars/all.yml':<br/>
    - An admin username and password assigned to 'ansible_user' and 'ansible_become_pass'<br/>
    - An account name to be created assigned to 'new_user'<br/>
    - A password for the new user assigned to 'user_pass'<br/>

Note: A hashed password string can be created with the command 'mkpasswd -m sha512crypt'.

### Usage:

```ansible-playbook setup.yml -i inventory --ask-vault-pass```

## "install_cockpit.yml" Ansible Playbook

Installs the Cockpit management console and nessessary components.<br/>
Where needed, firewall rules are created to allow access.<br/>
The 'cockpit-machines' package is installed if a KVM hypervisor is identified.<br/>
Works with Debian and RedHat based linux servers.

### Requires:

- An admin username and password assigned to the 'ansible_user' and 'ansible_become_pass' vars in 'group_vars/all.yml'

### Usage:

```ansible-playbook install_cockpit.yml -i inventory --ask-vault-pass```

## "mount_cifs_shares.yml" Ansible Playbook

Mounts CIFS shares as defined by the 'cifs_server' and 'cifs_share' vars in group_vars/all.yml.<br/>
The 'cifs-utils' package will be installed and mount points created at '/mnt' if missing.<br/>
Works with Debian and RedHat based linux servers.

### Requires:

- The following variables assigned in 'group_vars/all.yml':<br/>
    - An admin username and password assigned to 'ansible_user' and 'ansible_become_pass'<br/>
    - A username and password assigned to 'cifs_user' and 'cifs_pass'<br/>
    - An IP or Server name assigned to the 'cifs_server'<br/>
    - One or more share names assigned to the 'cifs_share' list<br/>

Note: The CIFS account must already exist both locally and remote.

### Usage:

```ansible-playbook mount_cifs_shares.yml -i inventory --ask-vault-pass```