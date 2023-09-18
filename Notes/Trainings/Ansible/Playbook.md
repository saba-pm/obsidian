- This is a file we create to describe works or jobs we want to do it.
-  We write playbook in yaml format.
-  We some roles now we  use it in our playbook.
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
