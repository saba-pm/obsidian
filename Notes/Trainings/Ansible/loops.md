```
- name: Create users         # Playbook name describing the task at a high level
  hosts: localhost           # Specifies that the playbook will run on the local machine
  tasks:                     # A list of tasks to be executed
    - user:                  # An Ansible module for managing user accounts
        name: '{{ item }}'   # Creates a user with the name provided by the item in the loop
        state: present       # Ensures the user is present on the system
      loop:                  # A loop to iterate over the list of user names
        - joe                # Each entry here represents a username to be created
        - george
        - ravi
        - mani
        - kiran
        - jazlan
        - emaan
        - mazin
        - izaan
        - mike
        - menaal
        - shoeb
        - rani

```

- **Playbook Name:** The `name` field is a descriptive label for the playbook. Here, it is "Create users".
- **Hosts:** The `hosts` field specifies the target machines where the tasks will run. In this case, it is set to `localhost`, meaning the tasks will execute on the local machine.
- **Tasks:** This section contains a list of tasks to perform. Each task is an item in the list.
- **User Module:** The `user` module is used to manage user accounts.
    - **Name:** The `name` parameter defines the username. `{{ item }}` is a Jinja2 variable that gets replaced with each item from the loop.
    - **State:** The `state` parameter ensures the user account is present (created if it doesn't exist).
- **Loop:** The `loop` directive iterates over a list of items (usernames) to perform the task multiple times, once for each username in the list.

This playbook will create user accounts for each of the names specified in the loop on the local machine.

```
- name: Create users          # Playbook name describing the task at a high level
  hosts: localhost            # Specifies that the playbook will run on the local machine
  vars:                       # Define variables
    users:
      - name: 'joe'           # Each entry here represents a dictionary with username and age
        age: 25
      - name: 'george'
        age: 30
      - name: 'ravi'
        age: 22
      - name: 'mani'
        age: 28
      - name: 'kiran'
        age: 27
      - name: 'jazlan'
        age: 24
      - name: 'emaan'
        age: 26
      - name: 'mazin'
        age: 29
      - name: 'izaan'
        age: 23
      - name: 'mike'
        age: 31
      - name: 'menaal'
        age: 21
      - name: 'shoeb'
        age: 33
      - name: 'rani'
        age: 32

  tasks:                      # A list of tasks to be executed
    - name: Create user       # Task name describing the specific action
      user:                   # An Ansible module for managing user accounts
        name: '{{ item.name }}'  # Creates a user with the name provided by the item in the loop
        state: present        # Ensures the user is present on the system
      loop: "{{ users }}"     # Reference the loop variable defined in vars

    - name: Display user info  # Task name for displaying user information
      debug: # Ansible module for printing debug messages# Message to display the user's name and age
        msg: "User {{ item.name }} is {{ item.age }} years old."  
      loop: "{{ users }}"     # Reference the loop variable defined in vars

```

# whit
```
- name: Create users          # Playbook name describing the task at a high level
  hosts: localhost            # Specifies that the playbook will run on the local machine
  tasks:                      # A list of tasks to be executed
    - name: Create user       # Task name describing the specific action
      user:                   # An Ansible module for managing user accounts
        name: '{{ item.name }}'# Creates user with the name provided by the item in the loop
        state: present        # Ensures the user is present on the system
      with_items:             # A loop to iterate over the list of user names and ages
        - { name: 'joe', age: 25 }      # Each entry here represents a dictionary with username and age
        - { name: 'george', age: 30 }
        - { name: 'ravi', age: 22 }
        - { name: 'mani', age: 28 }
        - { name: 'kiran', age: 27 }
        - { name: 'jazlan', age: 24 }
        - { name: 'emaan', age: 26 }
        - { name: 'mazin', age: 29 }
        - { name: 'izaan', age: 23 }
        - { name: 'mike', age: 31 }
        - { name: 'menaal', age: 21 }
        - { name: 'shoeb', age: 33 }
        - { name: 'rani', age: 32 }

    - name: Display user info  # Task name for displaying user information
      debug:                  # An Ansible module for printing debug messages
        msg: "User {{ item.name }} is {{ item.age }} years old."  # Message to display the user's name and age
      with_items:             # A loop to iterate over the list of user names and ages
        - { name: 'joe', age: 25 }
        - { name: 'george', age: 30 }
        - { name: 'ravi', age: 22 }
        - { name: 'mani', age: 28 }
        - { name: 'kiran', age: 27 }
        - { name: 'jazlan', age: 24 }
        - { name: 'emaan', age: 26 }
        - { name: 'mazin', age: 29 }
        - { name: 'izaan', age: 23 }
        - { name: 'mike', age: 31 }
        - { name: 'menaal', age: 21 }
        - { name: 'shoeb', age: 33 }
        - { name: 'rani', age: 32 }

```