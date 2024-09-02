Installation
sudo apt-add-repository ppa:ansible/ansible
sudo apt update
sudo apt install ansible

Hosts file

sudo nano /etc/ansible/hosts
ansible-inventory --list -y

[servers]
server1 ansible_host=100.26.220.138
server2 ansible_host=54.210.87.140
server3 ansible_host=54.236.43.216

[all:vars]
ansible_python_interpreter=/usr/bin/python3
ansible_user=ubuntu
ansible_ssh_private_key_file=/home/ubuntu/keys/shubham-linux-key.pem



Running commands
ansible all -a "df -h" -u ubuntu
ansible all -m ping -u ubuntu
ansible servers -a "uptime" -u ubuntu

Playbooks
Date:
- 
  name: Play Date
  hosts: servers
  tasks:
    - name: Show date
      command: date









Nginx Install:
-
 name: Install Nginx
 hosts: servers
 become: yes
 tasks:
   - name: Nginx Installer
     apt:
       name: nginx
       state: latest 
   - name: Nginx start
     service:
        name: nginx
        state: started
        enabled: yes









Conditional

- 
  hosts: servers
  become: true

  tasks:
  - name: Install apache
    apt: 
      name: apache2
      state: latest
    
    when: ansible_distribution == 'Debian' or ansible_distribution == 'Ubuntu'

  - name: Install httpd
    yum: 
      name: httpd
      state: latest
    
    when: ansible_distribution == 'CentOS' or ansible_distribution == 'Red Hat Enterprise Linux'


