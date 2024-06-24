We want to install something in our host with package .
The difference action run by tasks are called modulus 
```
---
-name: Install htop
 ansible.builitin.apt:
   name: htop
   state: present

====

-name: Install htop
 apt:    # this is modulus
   name: htop
   state: present
   update_cache: yes # apt update

-name: Install git
 apt:  # this is modulus
   name: git
   state: present
```

As you can see, if we want several packages we need define for each of them, but we can use <u>loop</u> and in one chart install all package we need.
```
-name: install packages
 apt:
   name: "{{ item }}"
   state: present
   update_cache: yes
loop:
   - git
   - htop
```


