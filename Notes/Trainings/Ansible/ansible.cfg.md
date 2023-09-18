We define our files and user we want work with it.

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

