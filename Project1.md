# WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS

## Connectiong To AWS EC2 instance.
I signed up and created a new ubuntu instance for my project 1 Lamp stack which generated a .pem file which i downloaded from AWS to my pc.
then i connected to the sever using ssh with the .pem file using windows terminal ssh -i project.pem ubuntu@0.0.0.0.0 (the 0 is a reference to my ip address).
I updated & upgraded the server using sudo apt-get update and sudo apt-get upgrade.

INSTALLING THE COMPONENTES OF LAMP Apache, Mysql and Php.

APACHE (engine)
i installed apache using sudo apt install apache2
checked the status using sudo systemctl status apache 2 which showed green dot and displayed status as active.
i then navigate to the instance security group to edit my inbound rules and open port 80 which is http connection port for webpage and using anywhere for the source ip 0.0.0.0.0.
I did checked my localhost address on my browser and it worked. showed apache2 page.

MYSQL (Database)
I installed mysql using sudo apt install mysql-server.
then used mysql secure_installation to authenticate mysql and create a root user with password.
then i opened mysql using sudo mysql and got connected to the database.

PHP (backend script side )
I installed php and all its components using sudo apt install php libapache2-mod-php php-mysql
I checked the status using php -v which showed php 7.4.3 version.
Creating The virtual host
I created a directory to hold my index.php file in the server directory using sudo mkdir /var/www/projectlamp
gave the directory the right permission as root using sudo chown -R $USER:$USER /var/www/projectlamp
I created a new configuration file in the site-available directory named projectlamp.conf using sudo vi /etc/apache2/sites-available/projectlamp.conf
I used nano as my editor.
Then i enabled the projectlamp.conf file as the default web root directory using 000-default.conf default-ssl.conf projectlamp.conf and sudo a2ensite projectlamp to enable the virtual host and sudo a2dissite 000-default to dissable the default preinstalled apache VirtualHost.
did a code unit test to my code if it has any error using sudo apache2ctl configtest
Then reload my apache using sudo systemctl reload apache2
so i did change the dir.conf file using sudo vim /etc/apache2/mods-enabled/dir.conf i changed the order of arrangement and put the index.php first so the webpage can load the index.php as default
Then reload my apache using sudo systemctl reload apache2
To check if the webroot and web page is working i created an index.php file in the /var/www/projectlamp folder and added a php code <?php phpinfo(); in the index.php file .
checked my ip address on the web browser with port 80 http://ip-address:80 and it worked fine showing the php version and all information about my server.

# SCREENSHOTS OF MY RESULTS

For the Apache2
![Screenshot (3)](https://user-images.githubusercontent.com/88409151/157458303-36df710c-1f24-4a33-bc4c-243d04bd0fa1.png)

For Mysql
![Screenshot (4)](https://user-images.githubusercontent.com/88409151/157459558-78d54dbb-ee6e-48cd-a64e-f9bb3e1494df.png)

For the landing page through my DNS/IP Address
![Screenshot (5)](https://user-images.githubusercontent.com/88409151/157459890-7338f3df-c085-4e5a-994f-9b440f81a30a.png)

For the PHP 
which i reloaded it from the DNS 
![Screenshot (7)](https://user-images.githubusercontent.com/88409151/157460024-082b17ec-120c-4207-87bc-7d52b4253a34.png)



