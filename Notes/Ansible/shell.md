We define in task directory.


```dirtree
- /inventory
- /roles
	- /default
		- /defaults 
			- main.yaml
		- /tasks
			- main.yaml #define here
```

We want to install something in our host with shell.
```
-name: Install packages with shell
 shell: |
    apt update; apt install htop git
```

### Pass env to directory

```
- name: Create Dir
  file: 
    state: directory
    path: "/tmp/dir"
-name: echo env to file
 shell: |
   echo {{ VARIABLE}} > /tmp/dir
- name: print var
  debug:
    msg: "{{ VARIABLE}}"
```