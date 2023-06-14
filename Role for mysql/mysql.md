### using a role for mysql from ansible galaxy

Install mysql role using `https://galaxy.ansible.com/geerlingguy/mysql`

writing a playbook to call for mysql role

```
- name: Install mysql
  hosts: all
  become: yes
  roles:
    - role: geerlingguy.mysql
  vars:
    mysql_bind_address: 0.0.0.0

```
![preview](mysql1.png)

![preview](mysql2.png)

![preview](mysql3.png)

### using a role for mysql with password

```
- name: Install mysql
  hosts: all
  become: yes
  roles:
    - role: geerlingguy.mysql
  vars:
    mysql_bind_address: 0.0.0.0
    mysql_root_username: root
    mysql_root_password: root

```

The output is as follows

![preview](mysqlpswd1.png)

![preview](mysqlpswd2.png)

![preview](mysqlpswd3.png)

