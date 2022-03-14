# Continous Integration Pipeline For Tooling Website.
The task of the project is to start automating part of our routine tasks with free and open source automation server - JENKINS.

In the project we are going to utilize Jenkins CI capabilities to make sure that every change made to the source code in Github https://github.com/Timmyzooto01/tooling will be automatically be updated to the Tooling website.

# INSTALL AND CONFIGURE JENKINS SERVER
Step 1 – Install Jenkins server
Create an AWS EC2 server based on Ubuntu Server 20.04 LTS and name it "Jenkins"

Install JDK (since Jenkins is a Java-based application)
sudo apt update
sudo apt install default-jdk-headless
# Install Jenkins
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > \ /etc/apt/sources.list.d/jenkins.list'
sudo apt update
sudo apt-get install jenkins
and i make sure Jenkins is up and running
sudo systemctl status jenkins

By default Jenkins server uses TCP port 8080 – open it by creating a new Inbound Rule in your EC2 Security Group which i even used All traffice for the inbound Security Group.
# Perform initial Jenkins setup.
From your browser access http://<Jenkins-Server-Public-IP-Address-or-Public-DNS-Name>:8080

You will be prompted to provide a default admin password

Which i retrieve it from your server

Using this code on my terminal sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Then you will be asked which plugings to install – choose suggested plugins.
Once plugins installation is done – create an admin user and you will get your Jenkins server address.

The installation is completed!

![Screenshot (28)](https://user-images.githubusercontent.com/88409151/158101412-2b71c87a-0fb8-4a26-8299-68d5357861b1.png)

![Screenshot (29)](https://user-images.githubusercontent.com/88409151/158101989-d897faa9-2dfe-46c3-a61d-8d4add97c570.png)

# Configure Jenkins to retrieve source codes from GitHub using Webhooks
1. Enable webhooks in your GitHub repository settings
![Screenshot 2022-03-14 034823](https://user-images.githubusercontent.com/88409151/158101642-8f28f70b-3c89-4954-8d03-163435a18f44.png)



2. Go to Jenkins web console, click "New Item" and create a "Freestyle project"
* To connect your GitHub repository, you will need to provide its URL, you can copy from the repository itself [https://github.com/Timmyzooto01/tooling.git]
* In configuration of your Jenkins freestyle project choose Git repository, provide there the link to your Tooling GitHub repository and credentials (user/password) so Jenkins could access files in the repository.
* Save the configuration and let us try to run the build. For now we can only do it manually.
Click "Build Now" button, if you have configured everything correctly, the build will be successfull and you will see it under #1

3. Click "Configure" your job/project and add these two configurations
* Configure triggering the job from GitHub webhook
* Configure "Post-build Actions" to archive all the files – files resulted from a build are called "artifacts".

* Now, go ahead and make some change in any file in your GitHub repository (e.g. README.MD file) and push the changes to the master branch.

* You will see that a new build has been launched automatically (by webhook) and you can see its results – artifacts, saved on Jenkins server.

![Screenshot (31)](https://user-images.githubusercontent.com/88409151/158102516-b808cf75-f474-4489-b3b5-fab1eb17cac4.png)
  
* By default, the artifacts are stored on Jenkins server locally
  
  ls /var/lib/jenkins/jobs/tooling_github/builds/<build_number>/archive/
 
![Screenshot (33)](https://user-images.githubusercontent.com/88409151/158102711-09f08e8c-7d78-4d7e-ba9b-5b49cfc72f12.png)
  
 # CONFIGURE JENKINS TO COPY FILES TO NFS SERVER VIA SSH
  Step 3 – Configure Jenkins to copy files to NFS server via SSH
  
* Install "Publish Over SSH" plugin.
* Configure the job/project to copy artifacts over to NFS server.
  ![Screenshot (34)](https://user-images.githubusercontent.com/88409151/158103227-153e5ed8-60ec-414b-b0b2-afec25f6c9ce.png)
  
* Save the configuration, open your Jenkins job/project configuration page and add another one "Post-build Action"
* Configure it to send all files probuced by the build into our previouslys define remote directory. In our case we want to copy all files and directories – so we use **.
* Save this configuration and go ahead, change something in README.MD file in your GitHub Tooling repository.
  
  Webhook will trigger a new job and in the "Console Output" of the job you will find something like this:
  ![Screenshot (35)](https://user-images.githubusercontent.com/88409151/158103501-333d9cbb-c7ef-4928-8d96-0a85e62c73b5.png)
* To make sure that the files in /mnt/apps have been udated – connect via SSH/Putty to your NFS server and check README.MD file
  
  cat /mnt/apps/README.md
  ![Screenshot (36)](https://user-images.githubusercontent.com/88409151/158103682-f1a22c05-fbb3-414d-a1a5-f4c25007fc90.png)
* But you have to give /mnt permission for it not be denied in the console output 
  
  sudo chmod -R 777 /mnt
  so i was able to see the changes made in the README.MD file 
  

  











