### playbook of openmrs without variables

```
---
- name: installing openmrs
  become: yes
  hosts: all
  tasks:
    - name: install java
      ansible.builtin.apt:
         name: openjdk-8-jdk
         update_cache: yes
         state: present
    - name: adding group
      ansible.builtin.group:
        name: tomcat
        state: present
    - name: create user
      ansible.builtin.user:
        name: tomcat
        create_home: yes
        shell: /bin/false
        group: tomcat
        state: present
    - name: download tomcat
      ansible.builtin.get_url:
        url: https://archive.apache.org/dist/tomcat/tomcat-7/v7.0.109/bin/apache-tomcat-7.0.109.tar.gz
        dest: /tmp/apache-tomcat-7.0.109.tar.gz
    - name: create a directory
      ansible.builtin.file:
        path: /opt/tomcat
        state: directory
      notify:
        - extract tomcat
        - changing ownership of directory
    - name: setting execute permissions
      ansible.builtin.file:
        path: conf
        recurse: yes
        owner: tomcat
        group: tomcat
        mode: g+r,g+x
    - name: changing ownership
      ansible.builtin.file:
        path:
          - webapps
          - work
          - temp
          - logs
        recurse: yes
        state: directory
        owner: tomcat
        group: tomcat
    - name: copy service file
      ansible.builtin.copy:
        src: tomcat.service
        dest: /etc/systemd/system/tomcat.service
    - name: daemon-reload
      ansible.builtin.systemd:
       daemon_reload: true
    - name: start tomcat
      ansible.builtin.systemd:
        state: started
        name: tomcat
    - name: changing ownership
      ansible.builtin.file:
        path: /var/lib/OpenMRS
        state: directory
        recurse: yes
        owner: tomcat
        group: tomcat
    - name: download openmrs
      ansible.builtin.get_url:
        url: https://sourceforge.net/projects/openmrs/files/releases/OpenMRS_Platform_2.5.0/openmrs.war
        dest: /tmp/openmrs.war
    - name: copy openmrs
      ansible.builtin.copy:
        src: /tmp/openmrs.war
        dest: /opt/tomcat/webapps/
        remote_src: yes
    - name: change ownership of mrs
      ansible.builtin.file:
        path: /opt/tomcat/webapps/
        state: directory
        recurse: yes
        owner: tomcat
        group: tomcat
  handlers:
    - name: extract tomcat
      ansible.builtin.unarchive:
        src: /tmp/apache-tomcat-7.0.109.tar.gz
        dest: /opt/tomcat
        extra_opts:
          --strip-components=1
        remote_src: yes
    - name: changing ownership of directory
      ansible.builtin.file:
        path: /opt/tomcat
        state: directory
        recurse: yes
        owner: tomcat
        group: tomcat

```
Execute the playbook with `ansible-playbook -i hosts openmrs.yml`

The output of the playbook executed is 

![preview](images/opn1.png)

![preview](images/opn2.png)

The output of tomcat page is

![preview](images/opn3.png)

The output of openmrs app is 

![preview](images/opn4.png)


