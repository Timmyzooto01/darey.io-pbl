## Ansible Refactoring And Static Assignments (Import and Roles).

* In this project, we will continue working with ansible-config repository and make some improvements to our code.
* Now we need to refactor our Ansible code, create assignments, and use the imports functionality. Imports allow to effectively re-use previously created playbooks in a new playbook – it allows you to organize your tasks and reuse them when needed.

## Step 1 - Jenkins Job Enhancement
* Lets make some changes to our Jenkins job, every new change in the code creates a seperate directory which is not very convenient when we want to run some commands from one place. Besides, it consumes space on Jenkins servers with each subsequent change.

* We will enhance it by introducing a new Jenkins project/job, which we will require Copy Artifact plugin.

* In the Jenkin-Ansible server, create a new directory called ansible-config-artifact, we will store there all artifacts after each build.

* Change permissions to this directory, so Jenkins could save files here.

* Go to Jenkins web console -> Manage Jenkins -> Manage Plugins -> on Available tab search for Copy Artifact and install this plgin without restarting Jenkins.
* 
* Create a new Freestyle project and name it save_artifacts.

* This project will be triggered by completion of the existing ansible project. Configure it accordingly.

* The main idea of save_artifacts project is to save artifacts into /home/ubuntu/ansible-config-artifact directory. To achieve this, create a Build step and choose Copy artifacts from other project, specify ansible as a source project and /home/ubuntu/ansible-config-artifact as a target directory.

* Test your set up by making some change in README.MD file inside your ansible-config repository (right inside master branch).

* If both Jenkins jobs have completed one after another – you shall see your files inside /home/ubuntu/ansible-config-artifact directory and it will be updated with every commit to your main branch.

## Step 2 - Refactor Ansible Code By Importing Other Playbooks Into site.yml
* Before starting to refactor the codes, ensure that you have pulled down the latest code from master (main) branch, and creat a new branch, name it refactor. Let see code re-use in action by importing other playbooks

* Within playbooks folder, create a new file and name it site.yml, this file will now be considered as an entry point into the entire infrastructure configuration. The site.yml will become a parent to all other playbooks that will be developed.

* Create a new folder in root of the directory and name it static-assignment. The static-assignments folder is where all other children playbooks will be stored. This is merely for easy organization of your work. It is not an Ansible specific concept, therefore you can choose how you want to organize your work.

* Move common.yml file into the newly created static-assignments folder.

* Inside site.yml file, import common.yml playbook.

* Create another playbook under static-assignments and name it common-del.yml. In this playbook, configure deletion of wireshark utility.

* Update site.yml with import_playbook: ../static-assignments/common-del.yml and run against dev servers.

## Step 3 - Configure UAT Webservers with a role 'Webserver'
* Launch 2 EC2 instances using RHEL 8 image, we will use them as our uat servers, so give them names accordingly – Web1-UAT and Web2-UAT.

* To create a role, you must create a directory called roles/, relative to the playbook file or in /etc/ansible/ directory.

* Create a roles directory in the root, cd into the directory, use an Ansible utility called ansible-galaxy, mkdir roles && cd roles && ansible-galaxy init webserver.

* The entire folder structure should like below.

* After removing unnecesary directories and files, the roles structure should look like this.

* Update the inventory ansible-config/inventory/uat.yml file with IP addresses of the 2 UAT Webservers.

* In /etc/ansible/ansible.cfg file uncomment roles_path string and provide a full path to your roles directory roles_path = /home/ubuntu/ansible-config/roles, so Ansible could know where to find configured roles.

* It is time to start adding some logic to the webserver role. Go into tasks directory, and within the main.yml file, start writing configuration tasks to do the following.

* Install and configure Apache (httpd service) Clone Tooling website from GitHub https://github.com/Timmyzooto01/tooling.git. Ensure the tooling website code is deployed to /var/www/html on each of 2 UAT Web servers. Make sure httpd service is started

* The main.yml will consist of the following tasks.

## Step 4 - Reference 'Webserver' role.
* Within the static-assignments folder, create a new assignment for uat-webservers uat-webservers.yml. This is where you will reference the role.

* Remember that the entry point to our ansible configuration is the site.yml file therefore , we need to refer uat-webservers.yml role inside site.yml. The site.yml will look like:

## Step 5 - Commit & Test.
* Commit your changes, create a Pull Request and merge them to master (main) branch, make sure webhook triggered two consequent Jenkins jobs, they ran successfully and copied all the files to your Jenkins-Ansible server into /home/ubuntu/ansible-config/ directory.

* Now run the playbook against the uat inventory.

* You should be able to see both of the UAT Web servers configured and you can try to reach them from your browser: http://<Web1-UAT-Server-Public-IP-or-Public-DNS-Name>/index.php.

* The Ansible architecture now looks like this:
  
  
  
  
  ## SCREENSHOOT
  
  ![Screenshot (54)](https://user-images.githubusercontent.com/88409151/159536728-4d6b988c-3aab-48b3-b7a6-6482eff94b28.png)

  
  ![Screenshot (55)](https://user-images.githubusercontent.com/88409151/159536829-516bd67d-8e69-4401-a656-db3ef47f60d1.png)



