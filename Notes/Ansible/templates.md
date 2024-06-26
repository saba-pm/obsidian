Templates in Ansible are used to generate configuration files dynamically based on variables and data defined in your Ansible playbook or inventory.
- In template like file, it's better to follow that structure. 
```dirtree
- /inventory
- /roles
- templates
	- var
		- temp1
			- bin 
				- temp1.sh
			- conf
				- temp1.conf
- ansible.cfg
```

If you want to use dynamic var, you can follow this template in temp1.conf:

```
listen_ip: 1.2.3.4
listen_port: 80
temp_var: {{ VARIABLE }}
```
- when we set our template now, you can use in tasks:
```
-name: create dir
 file:
   state: "{{ item }}"
   loop:
     - "/var/temp1/conf"
     - "/var/temp1/bin"
- name: Template
  template:
    src: path (/var/temp1/conf/temp1.conf)
    dest: path (/var/temp1/conf/temp1.conf)
```

 - To use templates in Ansible, you typically employ a template engine like Jinja2, which provides powerful template capabilities for generating dynamic content. Ansible's modules like `template` or `template` in conjunction with `with_items` or `loop` can be used to render these templates and deploy the generated configuration files to target hosts. 