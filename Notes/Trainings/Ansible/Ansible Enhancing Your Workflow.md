 - Ansible relies on SSH to establish connections with your devices, but it's advisable to use SSH keys for enhanced security.
 - In destination just you need python (all the yaml files convert to python script after that execute id)
## What is ansible work?
We define some roles for ansible and in roles we have some tasks, In other way we have hosts and we divided them base on structure like dev or stg . at the end we deploy roles on hosts
## Ansible Structure 
To effectively employ Ansible, it's essential to adhere to best practices, starting with organizing your directory structure:
1.  Begin with a main directory for your Ansible project.
   Files:
   - ==[[Inventory]]== : This file defines your hosts and describes their divisions.
   - ==Playbook== :It specifies the tasks you want to perform on hosts.
   - ==ansible.cfg== :1. - Your Ansible configuration file, which takes precedence over the global configuration if present. (maybe you had config in /etc/ansible but if you have this file ansible will be use this)
   Directory:
   - ==host_vars== : This directory stores host-specific variables.
   - ==group_vars== : Here, you can store variables that apply to entire host groups.
   - ==roles== : The heart of your Ansible project, this directory contains
     - ==handlers==: 
       main.yaml
     - ==defaults== : 
       main.yaml
     - ==vars== : This directory contains `main.yaml` and other variable files.
       - main.yaml
     - ==tasks== : Here, you'll find `main.yaml` and other task-related files.
       - main.yaml
     - ==files==: For file transfers to hosts, you can include sub directories.
     -  ==templates== : This directory can be used for template files.