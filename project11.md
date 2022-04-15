## Ansible Configuration Management
* In project 7-10, we performed a lot of manual operations for setting up virtual servers, installing and configuring required softwares.

* The project aim is to automate most of the tasks with Ansible Configuration Management.

* Install And Configure Ansible on EC2 Instance

* Update the name tag on our Jenkins EC2 Instance to Jenkins-Ansible, it is the server will we use to run our playbook.

* In our Github account create a new repository named ansible-config.

* Configure Jenkins build job to save the repository content everytime a change occurs.

* Create a new freestyle project "ansible" in Jenkins and point it to the "ansible-config" repository.

* Configure Webhook in Github and set webhook to trigger ansible build.

* Test the setup by making some change in README>MD file in main branch and make sure the build starts automatically and Jenkins saves the file.

* Install Ansible sudo apt update, sudo apt install ansible in the instance.

* Create a folder named ansible and cd into it mkdir ansible && cd ansible.
* Clone the ansible-config repository in the ansible folder

## Ansible Development
* Cd into the ansible-config folder and create a branch git checkout -b timi and switch to it.

* In the branch, create two directories playbooks and inventory respectively mkdir playbooks && mkdir inventory.

* The playbooks folder will be used to store all playbook files and the inventory folder will be used to keep the hosts (all servers information) organised.

* In the playbooks folder, create the first playbook named common.yml touch common.yml
* In the inventory folder, create an inventory file (.yml) for each environment (Development, Staging Testing and Production) respectively touch dev.yml staging.yml uat.yml prod.yml.

* Update the inventory/dev.yml to start configuring.
* Ansible uses TCP port 22 by default,which means it needs to ssh into target servers (nfs, db, webservers, lb) which i iused all trafic instead.

## Create a Common Playbook
* It is time to start giving Ansible instructions on what needs to be performed on all servers listed in inventory/dev.yml .

* Update the playbook/common.yml file with the following code:
* Run the playbook and ensures it works properly.

## Update GIT with the latest code.
All the configurations we did are all on our local machine, so we need to push all this changes to Github.

## SCREENSHOTS

![Screenshot (45)](https://user-images.githubusercontent.com/88409151/159381596-475c4430-63f1-4f6a-bf0d-1b938e3cbced.png)


![Screenshot (46)](https://user-images.githubusercontent.com/88409151/159381628-f361674a-6239-44a1-9293-892b05909074.png)

