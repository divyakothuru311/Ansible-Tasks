## playbook for broadleaf commerce application.

[Refer here]https://khajaworkspace.slack.com/archives/D059G0S487Q/p1686154331416509  repository where the broadleaf application is present.

we need to clone the application from the repository which is in remote machine to the local machine.

The command for cloning is `git clone`(url of repository)
![preview](images/broad1.png)

Install maven using `sudo apt install maven`

next follow the manual commands 
![preview](images/broad2.png)

As of now there is no service file for this application .

The playbook for broadleaf commerce is
```
---
- name: BROADLEAF COMMERCE
  hosts: all
  become: yes
  tasks:
    - name: cloning from git 
      ansible.builtin.git:
        url: https://github.com/BroadleafCommerce/DemoSite.git
        dest: /home/devops/Demosite
    - name: Install maven
      ansible.builtin.apt:
        name: maven
        update_cache: yes
        state: present
    - name: clean install maven
      ansible.builtin.shell:
        chdir: /home/devops/Demosite
        cmd: mvn clean install
    -name: spring boot run
      ansible.builtin.shell:
        chdir: /home/devops/Demosite/site
        cmd: mvn spring-boot:run
```
The output for the application is as follows 
![preview](images/broad3.png)


