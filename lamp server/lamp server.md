### Installing and configuring ansible
 * creating two ubuntu vms and one redhat vm.
 * we will name one ubuntu vm as ansible control node,another ubuntu vm as node1.
 * Redhat vm as node2. 
 * creating a user 'devops' in two vms with sudo permissions.
  
   ![divya](./images/images/1node2.png)

 * Generate a keypair in ansible control node.
  
   ![](./images/ansible4.png)

 * copy the publickey to other vms from ansible control node.
   
   ![](./images/ansible6.png)

 * Install Ansible in Ansible control node.
   
   ![](./images/ansible9.png)

 * After installation u can verify the ansible version
  
   ![](./images/ansible1.png)

 *  We need to create an inventory with file named as hosts and with ipaddress in it.
 
 *  Now enable password authentications by editing config file
   
    ```
    /etc/ssh/sshd_config
    ```

 * and set password authentication from no to yes.
 * Execute sshd restart service
   
   ![](./images/1node2.png)
  
  # Installing lamp server on ubuntu

 * create a directory with playbooks and ubuntu.yml file in it.
   
   ![](./images/ansible12.png)

 * ubuntu.yml file contains playbook 
   
   ![](./images/ansible13.png)

 * create a file info.php
   
   ![](./images/ansible14.png)

    ```
    <?php phpinfo(); ?>
    ``` 
 *  check the connectivity by executing 
   
    ```
    ansible -m ping -i hosts all
    ```

    ![](./images/ansible2.png)

 * we need to check the syntax of playbook
   ```
   ansible-playbook -i <inventory-path> --syntax-check <playbook-path>
   ```

 * Execute the playbook 
  
   ```
   ansible-playbook -i <inventory-path> <playbook-path>
   ```
   ![](./images/ansible16.png)

 * cross check the installation
  
   ![](./images/ansible19.png)
 
 # Installing lamp server on Redhat
 * create redhat.yml file in playbooks directory.
  
   ![](./images/ansible14.png)
  
 * Execute the playbook 
  
   ```
   ansible-playbook -i <inventory-path> <playbook-path>
   ```
   ![](./images/ansible16.png)

 * verify the installation
   
   ![](./images/ansible20.png)

 