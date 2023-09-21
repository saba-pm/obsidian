  - Ansible uses SSH to establish connections with your devices, but it's highly advisable to enhance security by utilizing SSH keys.
 - In destination just, you need python (all the yaml files convert to python script after that execute ID).
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
	   - [[host_vars]] : This directory stores host-specific variables.
	   - [[group_vars]] : Here, you can store variables that apply to entire host groups.
	   - roles : The heart of your Ansible project, this directory contains. Subdirectories as follows:
	     - <u>handlers</u>: 
	       main.yaml
	     - <u>defaults</u> : 
	       main.yaml
	     - <u>vars</u> : This directory contains `main.yaml` and other variable files.
	       - main.yaml
	     - <u>tasks</u> : Here, you'll find `main.yaml` and other task-related files.
	       - Main.yaml
	     - [[files]]: For file transfers to hosts, you can include subdirectories.
	     -  [[templates]] : This directory can be used for template files.
## Modulus 

In ansible, we can use [[modulus]] and [[shell]] to install something in hosts, usually we use these in roles. 
## Difference between packages and shell

1. Big difference between shell and package related to details when we use packages we can see more details.
2.  Second difference when, we want to check our playbook, or we want to understand packages are already install or not we couldn't use shell.  

## Variable

1. We can define variable in command line input: `ansible-playbool playbooks/default.yaml -e "VARIABLE"=test `. We can use --extra-vars instead -e.
2. Define in role in default.yaml, if you want to use this way across your role create another directory and in the directory create yaml file in there define your variable. 
	1. Just be passion, the priority of input is higher than define in role.
3. Define in inventory. Create var file but your var file name it must be your host name like `host_vars/h1`.  
	1. Between define in role and in host_vars, the host_vars has higher priority.
	2. Between define in command input and in host_vars, the command input has higher priority.
4. Define in group_vars(set env for all host based on define in inventory).
	1. Between host_vars and group_vars, host_vars hast more priority.

```dirtree
- /inventory
	- /host_vars
		- h1.yaml
	- main.yaml
- /roles
	- /default
		- /defaults #define env here
			- main.yaml
		- /tasks
			- main.yaml
- ansible.cfg
```
 
## Variable Priority

1. Command input
2. host_vars
3. group_vars
4. roles

# Ansible Fact
n Ansible, facts are pieces of information about the target hosts (remote servers or systems) that Ansible collects and makes available for use in playbooks and tasks. These facts provide valuable insights into the state and configuration of the target hosts, and they can be used for various purposes, including automation, conditional statements, and reporting.
- We can use fact in roles in the debug section. 
```
-name: facts
 debug:
   msg: "{{ ansible_facts}}" #see all facts
```
Fact are jison, then we can choose specific object like now we need IP: 
```
-name: facts
 debug:
   msg: "{{ ansible_factsdefault_ipv4.address}}"
```
