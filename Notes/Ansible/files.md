For transfer files, it's better to do observe structure  like  you want copy file in specific path, create path in ansible.

```dirtree
- /inventory
- /roles
	- /default
		- /defaults #define env here
			- main.yaml
		- /tasks
			- main.yaml
	- files
		- var
			- temp
				- bin
					- temp.sh
				- conf
					- temp.conf
- ansible.cfg
```

Now just we need to create task and in the task create our destination directory, after that use copy modules. 
