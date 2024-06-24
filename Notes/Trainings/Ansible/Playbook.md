- This is a file we create to describe works or jobs we want to do it.
-  We write playbook in yaml format.
-  We some roles now we  use it in our playbook.
- Playbook has difference dictionary. In the below example, we have two dictionaries, and they are separated by  `-`.
 ```
 - name:
   hosts: mysql #we define in hosts.yaml
   roles:
	 - mysql #name of the roles
- name: postgres
  hosts: postgres
  roles:
	- postgres 
```
-  If we want to use one playbook but uses difference multiple playbook  we could create `sudoer.yaml` in this file we call playbook
sudoer.yaml:
```
- import_playbook: default.yml
- import_playbook: pre-install.yml
- import_playbook: web.yml
```

- If you want to run your play book in specific host, you can use --limit : `ansible-playbook playbooks/default.yaml --limit h1,h2`. 
- If you want to see this playbook run in which host, you use `--list-hosts`.
-

If you  define variable in playbook,  you  can use variable by call variable name in double braces:
```
name: add dns
hosts: all
vars:
  dns_server: 8.8.8.8
task:
	- lineinfile:
		path: /ete/resolve.conf
		line: 'namesever {{dns_server}}'

```