inventory has different type but  two of them is more public and we use it, is <u>INI</u> & <u>YAML</u> .
## Inventory parameters: 
1. Ansible connection
2. ansible port
3. ansible user 
4. asible ssh pass

# INI
we define our grouping in [] for example: 
[all]
	- h1
	- h2
	- h3
[web]
	- h1
	- h2
[db]
	- h1
	- h2

when you define your grouping maybe one of them is need another all another group host therefor we define in another way :
hosts.ini
```
[web]
h1
h2
[all]
h1
h2
h3
[firewall:childeren]
web #just we say name of the group
all #just we say name of the group
```
# YAML
 like all yaml file is sensitive all space or enter for example define our hosts file base on yaml
 Inventory/main.yaml:
```
---
all:
  hosts:
    lb.sudoer.net:
    db.sudoer.net
      ansible_host: 0.0.0.0 # if we are not set dns name we can use ip if we set dns name dosen't need ths item
    app1.sudoer.net:
      ansible_host: 1.2.3.4  
    app2.sudoer.net:
      ansible_host      
      
app:
  hosts:
    db.sudoer.net
      ansible_host: 0.0.0.0 # if we are not set dns name we can use ip
    app1.sudoer.net:
      ansible_host: 0.0.0.0  

db:
  hosts:
    db.sudoer.net
      ansible_host: 0.0.0.0 # if we are not set dns name we can use ip 

lb:
  hosts:
    lb.sudoer.net:
    db.sudoer.net
      ansible_host: 0.0.0.0 # if we are not set dns name we can use ip
      
```

 `