 - Ansible uses SSH to establish connections with your devices, but it's highly advisable to enhance security by utilizing SSH keys.
 - In destination just you need python (all the yaml files convert to python script after that execute id)
## How Ansible Works
- In Ansible, we define roles that encompass specific tasks. Additionally, we categorize hosts based on their role, such as development (dev) or staging (stg). Ultimately, we deploy these roles onto the designated hosts.
##  Ansible Directory Structure
To effectively utilize Ansible, it's crucial to follow best practices, which start with organizing your directory structure:
1.  **Main Directory**: Initiate your Ansible project by creating a main directory.
   **Files**:
	   - [[Inventory]] : This file defines your hosts and describes their divisions.
	   - [[Playbook]] :It specifies the tasks you want to perform on hosts.
	   - [[ansible.cfg]] : Your Ansible configuration file, which takes precedence over the global configuration if present. (maybe you had config in /etc/ansible but if you have this file ansible will be use this)
   Directory:
	   - ==host_vars== : This directory stores host-specific variables.
	   - ==group_vars== : Here, you can store variables that apply to entire host groups.
	   - ==roles== : The heart of your Ansible project, this directory contains
	   sub directories as follows:
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

