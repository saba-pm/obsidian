inventory has different type but  two of them is more public and we use it, is <u>INI</u> & <u>YAML</u> .

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
 like all yaml file is sensitive all space or enter for example define our hosts file base on yaml.
 hosts.yaml:
 ```
 all:
   hosts:
     h1:
     h2:
 web:
   hosts:
     h1:
     h2:    
```
 
 
 
 
 
 
 `