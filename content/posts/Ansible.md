---
title: "Ansible"
date: 2023-01-18T14:55:57+01:00
draft: false
---

# Run Ansible Playbook
To run the Ansible playbook, we will use bash scripts. First, navigate to the scripts directory:

```bash
$ cd scripts

```

this is the folders we need:
```
.
├── playbook
│   ├── README.md
│   ├── change_to_new_hosts.bash
│   ├── deleteme.bash
│   ├── docker_playbook.yml
│   ├── hosts
│   ├── packages_playbook.yml
│   └── start_ansible_playbook.bash
└── ssh
    ├── README.md
    ├── authorized_keys
    ├── put_here_your_ssh_key_to_send.bash
    ├── remove_knowhost.bash
    └── ssh_to_workstation.bash
```


1. Remote any old know host to prevent any conflict:

```ruby
 $ bash remove_knowhost_beforeanything.bash
```
 2. Transfer SSH Public Key to Workstations

 `IMPORTANT`: there are two methods used but one of them is commented.

    a. Insert your SSH public key to the bash script.

    b. Insert your SSH public key in "authorized_keys" file(Commented).

To run it use this command in your terminal:
```ruby
 $ bash put_here_your_ssh_key_to_send.bash
```

## Running the ansible Playbook 
1. Navigate to the playbook directory:

```bash
$ cd ../playbook
```

2. Before running the Ansible playbook, make sure to create a `hosts` file with the new public IP addresses of your VMs. You can use the following command to automatically generate this file:

```ruby
$ bash change_to_new_hosts.bash
```
3. After creating the hosts file, you can now run the Ansible playbook. We have two playbooks available  {we will add more in the future}

Choose the playbook that you want to run:

        A. Installing Docker.
        B. Installing multiple tools for our Developers.

4. run and execute the following command to run both:
```ruby
$ bash start_ansible_playbook.bash
```
 ________
NOTE: if you want to not use ssh and cp the playbook inside the vm and run it locally you can make sure to make the necessary changes

<!-- `README.md`: A file explaining the purpose of the directory

`change_to_new_hosts.bash`: A bash script to create the hosts file with the new public IP of the VMs

`copy_ansible_playbook_to_workstations.bash`: A bash script to copy the Ansible playbook to the workstations

`docker_playbook.yml`: An Ansible playbook to install Docker

`hosts`: A file containing the IP addresses of the workstations

`packages_playbook.yaml`: An Ansible playbook to install multiple tools for our developers

`start_ansible_playbook.bash`: A bash script to start the Ansible playbook -->