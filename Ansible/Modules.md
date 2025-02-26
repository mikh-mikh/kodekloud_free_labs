# Ansible modles lab

Success doesn't come from what you do occasionally. It comes from what you do consistently.

– Marie Forleo

## 1 / 19
info
In this lab exercise you will use below hosts. Please note down some details about these hosts as given below :

student-node :- This host will act as an Ansible master node where you will create playbooks, inventory, roles etc and you will be running your playbooks from this host itself.
node01 :- This host will act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:

User: bob
Password: caleston123
node02 :- This host will also act as an Ansible client/remote host where you will setup/install some stuff using Ansible playbooks. Below are the SSH credentials for this host:
User: bob
Password: caleston123
Note: Please type exit or logout on the terminal or press CTRL + d to log out from a specific node.

## 2 / 19
Which of the following Ansible modules support free_form parameter?

https://docs.ansible.com/ansible/latest/collections/ansible/builtin/command_module.html

right answer - command module

## 3 / 19
Does Ansible support idempotancy?

yes, для этого его и придумали

right answer - yes

## 4 / 19
Which of the following commands we can use to see the information about Ansible modules from command line?

right answer - ansible-doc

## 5 / 19
Which Ansible module is used in the following playbook?

```
---
- hosts: localhost
  become: yes
  become_user: root
  tasks:
    - name: create user
      user: 
	    name: admin
```

right answer - user

## 5 / 19
Which Ansible module is used in the following playbook?

A. It only adds the given line in file if that line doesn't exist in that file.
B. It adds the given line in file even if that line already exists in that file.
C. It replaces all existing lines in the file with a new given line.
D. It keeps the existing lines as well and add a new given line in the file.
		
right answer - D & A

## 7 / 19
What are Ansible system modules used for?

A. System modules are basically used to create/update files and directories.
B. System modules are actions to be performed at a system level such as modifying the users and groups on a system, modifying iptables, starting/stopping the service etc.
C. System modules are used to execute commands or scripts on a system.
D. System modules are used to install and setup packages on a system.

right answer - B

## 8 / 19
Your organization uses a proprietary cloud service that is not natively supported by Ansible. 
You need to develop a custom Ansible module to interact with this cloud service's API and provision resources.
Which type of the Ansible plugins allows you to integrate with a cloud provider's API for custom resource provisioning?

a. Connection Plugin
b. Lookup Plugin
c. Module Plugin
d. Action Plugin

right answer - module plugin (why? idk)

## 9 / 19
You've developed a custom module named custom_cloud. To test this module in a playbook named deploy.yml, which of the following task definitions is correct?

a: 
```
- name: Provision custom cloud resource
  action: custom_cloud
  args:
    param1: value1
    param2: value2
```
b:
```
- name: Provision custom cloud resource
  module: custom_cloud
  parameters:
    - param1: value1
    - param2: value2
```
c:
```
- name: Provision custom cloud resource
  custom_cloud:
    param1: value1
    param2: value2
```
d:
```
- name: Provision custom cloud resource
  use_module: custom_cloud
  with_args:
    param1: value1
    param2: value2
```
right answer - c

## 10 / 19

You are tasked with setting up an Ansible playbook that automates the deployment of applications on AWS ec2 instances. 
Before running the playbook, you need to ensure that Ansible has an up-to-date inventory of all ec2 instances in your AWS account.
Which type of Ansible plugin would you use to fetch real-time information about your AWS ec2 instances?

right answer - d (dynamic inventory)

## 11 / 19

You have a custom dynamic inventory script named aws_inventory.py. Which command would you use to list all hosts in your AWS inventory using this script?

a. ansible-inventory --list -i aws_inventory.py
b. ansible-playbook --inventory aws_inventory.py
c. ansible aws_inventory.py --list-hosts
d. ansible-list --inventory aws_inventory.py

right answer - a

## 12 / 19

You are tasked with finding a collection in Ansible that provides modules specifically designed for managing Cisco IOS devices. Using the Modules & Plugins Index, which of the following collections is best suited for this purpose?

a. cisco.config
b. cisco.ios
c. cisco.setup
d. cisco.network

right answer - b

## 13 / 19

Which of the following is not a common connection parameter used by modules within the cisco.ios collection for managing Cisco IOS devices?

a. hostname
b. password
c. ios_version
d. username

right answer - c

## 14 / 19

Which of the following Ansible versions is cisco.ios module likely to be compatible with?
Note: This can be a hypothetical answer; the actual version compatibility would need to be checked in the Modules & Plugins Index.

a. Ansible 1.5
b. Ansible 2.8
c. Ansible 3.1
d. Ansible 4.0

right answer - b (idk)

## 15 / 19

You're planning to deploy an application on AWS and need to set up ec2 instances using Ansible. Which module is primarily used for managing ec2 instances?

a. aws_instance
b. aws_ec2_config
c. ec2_instance
d. aws_setup

https://docs.ansible.com/ansible/latest/collections/amazon/aws/ec2_instance_module.html

right answer - caleston123

## 16 / 19

Update the playbook named playbook.yaml under /home/bob/playbooks directory with a task named Execute a script to run a script. The script is located at /tmp/install_script.sh on student-node.
Use the script module.
Note: There is already an inventory file /home/bob/playbooks/inventory present on student-node system.

```
---
- name: 'hosts'
  hosts: all
  become: yes
  tasks
```

```
- name: 'hosts'
  hosts: all
  become: yes
  tasks:
    - name: Execute a script
      ansible.builtin.script: /tmp/install_script.sh
```

```
export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook -i playbooks/inventory playbooks/playbook.yaml
[bob@student-node ~]$ export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook -i playbooks/inventory playbooks/playbook.yaml 

PLAY [hosts] *********************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************
ok: [node01]
ok: [node02]

TASK [Execute a script] **********************************************************************************************************
changed: [node01]
changed: [node02]

PLAY RECAP ***********************************************************************************************************************
node01                     : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
node02                     : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

## 17 / 19

Update the playbook /home/bob/playbooks/playbook.yaml to add a new task to start httpd service on all web nodes defined in /home/bob/playbooks/inventory file.
Use the service module.

```
---
- name: 'hosts'
  hosts: all
  become: yes
  tasks:
    - name: 'apache restart'
      service:
        name: httpd
        state: restarted
```

## 	18 / 19

Update the playbook /home/bob/playbooks/playbook.yaml to append the /var/www/html/index.html file on all web nodes. The line needs to be added is Welcome to ansible-beginning course, create the index.html file if doesn't exist.
Use the lineinfile module.

```
---
- name: 'hosts'
  hosts: all
  become: yes
  tasks:
    - name: 'Execute a script'
      script: '/tmp/install_script.sh'
    - name: 'Start httpd service'
      service:
        name: 'httpd'
        state: 'started'
    - name: 'add text to html'
      lineinfile:
         path: '/var/www/html/index.html'
         line: 'Welcome to ansible-beginning course'
         create: yes
```
```
[bob@student-node ~]$ export ANSIBLE_HOST_KEY_CHECKING=False && ansible-playbook -i playbooks/inventory playbooks/playbook.yaml 

PLAY [hosts] *********************************************************************************************************************

TASK [Gathering Facts] ***********************************************************************************************************
ok: [node01]
ok: [node02]

TASK [Execute a script] **********************************************************************************************************
changed: [node01]
changed: [node02]

TASK [Start httpd service] *******************************************************************************************************
ok: [node01]
ok: [node02]

TASK [add text to html] **********************************************************************************************************
changed: [node01]
changed: [node02]

PLAY RECAP ***********************************************************************************************************************
node01                     : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0   
node02                     : ok=4    changed=2    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
[bob@student-node ~]$ curl node01
Welcome to ansible-beginning course
```

## 19 / 19
Update the playbook /home/bob/playbooks/playbook.yaml to add a new task to create a new user called web_user.

Use the user module for this task. You can find the user details as below.

Username: web_user
uid: 1040
group: developers

```
---
- name: 'hosts'
  hosts: all
  become: yes
  tasks:
    - name: 'Execute a script'
      script: '/tmp/install_script.sh'
    - name: 'Start httpd service'
      service:
        name: 'httpd'
        state: 'started'
    - name: "Update /var/www/html/index.html"
      lineinfile:
        path: /var/www/html/index.html
        line: "Welcome to ansible-beginning course"
        create: true
    - name: 'add user'
      user:
        name: web_user
        uid: 1040
        group: developer
```

я не уложился в час логгируя и пья чай - работает:) для последнего задания они взяли guid 1030 из примера официальной доки по энсиблу:)		