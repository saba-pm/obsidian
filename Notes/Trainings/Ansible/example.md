In this scenario we have 4 servers all of them has got NGINX  one of them is our load balance on two of them is our web, in web we have WordPress at the end web server connect to db server.
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

ansible.cfg:
```
[defaults]
inventory   = ./inevtory/main.yaml
remote_tmp  = /tmp
forks       = 150
sudo_user   = root
remote_user = root
roles_path  = ./roles
host_key_checking = False
log_path    = ./log/ansible.log

[privilege_escalation] # when we want change our user after connect to the server we define here id we don't want use root user.
#become        = true
#become_method = sudo
#become_user   = asghar #become this user 
#become_ask_pass = false

[ssh_connection]
scp_if_ssh = True
```

Now we want to define one role and it must run on all the servers. `touch roles/default/tasks/main.yaml`:
