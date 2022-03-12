# WEB SOLUTION WITH WORDPRESS
Creating two server 1. Wordpress server and 2. Database server all using Red hat
Preparation of web server
First i added 3 new disk to my web server on my EBS volumes
Then i added it by attaching it to my instance using the right availability zone
# DISK MANAGEMENT
i used lsblk to inspect the block device attached to my server which ins in xvdf,xvdg and xvdh and used df -h to see all mount and free space on the server.
Then used gdisk utility to create a single partition on each of the 3 disks. using gdisk /dev/xvdf and all other disk, created new partition and write to the new partition.
I used lsblk to view newly configured partition which added 1 at the back of the partition name xvdf1, xvdg1, xvdh1
Then i installed Logical; volume using sudo yum install lvm2
I used Physical volume to mark the volumes to be used by lvm (pvcreate /dev/xvdf1,....)
Verified my Physical volumes using sudo pvs;
Used vgcreate to add the physical volume to a volume group and named it webdata-vg. (sudo vgcreate webdata-vg /dev/xvdh1 /dev/xvdg1 /dev/xvdf1)
Then use lvcreate to create a logical volume and used half of the physical volume size (sudo lvcreate -n apps-lv -L 14G webdata-vg)
Verified if my lvm is mounted using sudo lvs to verify all the setup (sudo vgdisplay -v #view complete setup - VG, PV, and LV and sudo lsblk )
I format the lv with ext4 filesystem format (sudo mkfs -t ext4 /dev/webdata-vg/apps-lv)
Then make a directory to store websites files (sudo mkdir -p /var/www/html) also the backup log file (sudo mkdir -p /home/recovery/logs)
then i mount my apps lv volume onto the web directory (sudo mount /dev/webdata-vg/apps-lv /var/www/html/)
i used rsync to backup my log file into the home/recovery directory. (sudo rsync -av /var/log/. /home/recovery/logs/)
Now mount the logs lv onto the log directory (sudo mount /dev/webdata-vg/logs-lv /var/log)
Then restore the log file backed up in the home/recover into the /var/log folder.
I edited the /etc/fstab to make the mount permanent.
To get the Id of each lv disk, i did (sudo blkid to display the id)
Then input it into the /etc/fstab file (UUID=b281a5db-b7cb-4f10-b8bd-2d911af68cc4		/var/www/html	ext4 	defaults	0 0 

 UUID=c25564b1-2d76-48e1-be8d-d0b4f2fbba87 		/var/log	ext4	defaults	0 0)
then i reload my configuration ( sudo mount -a and sudo systemctl daemon-reload)
Then verify my setup using df -h.
# DATABASE PREPARATION
I configured a new database server using redhat and mounting 2 new disks to it./db /logs and created database named wordpress
Installing Wordpress On Webserver EC2
i did and update on my (sudo yum update)
install wget and all apache dependencies (sudo yum -y install wget httpd php php-mysqlnd php-fpm php-json)
start apache with (systemctl enable and start httpd)
then i installed all php dependencies (
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
sudo yum install yum-utils http://rpms.remirepo.net/enterprise/remi-release-8.rpm
sudo yum module list php
sudo yum module reset php
sudo yum module enable php:remi-7.4
sudo yum install php php-apcache php-gd php-curl php-mysqlnd
sudo systemctl start php-fpm
sudo systemctl enable php-fpm
setsebool -P httpd_execmem 1)
Restart apache (sudo systemctl restart httpd)
# DOWNLOADING AND SETTING UP WORDPRESS
mkdir wordpress
cd wordpress
sudo wget http://wordpress.org/latest.tar.gz
sudo tar xzvf latest.tar.gz
sudo rm -rf latest.tar.gz
cp wordpress/wp-config-sample.php wordpress/wp-config.php
cp -R wordpress /var/www/html/
Configuring the SELinux Policies
sudo chown -R apache:apache /var/www/html/wordpress
sudo chcon -t httpd_sys_rw_content_t /var/www/html/wordpress -R
sudo setsebool -P httpd_can_network_connect=1
# Installing mysql on my database Server
sudo yum update
sudo yum install mysql-server
sudo systemctl restart mysqld
sudo systemctl enable mysqld
# CONFIGURING DATABASE TO WORK WITH WORDPRESS
sudo mysql
CREATE DATABASE wordpress;
CREATE USER myuser@` IDENTIFIED BY 'mypass';
GRANT ALL ON wordpress.* TO 'myuser'@'';
FLUSH PRIVILEGES;
SHOW DATABASES;
exit
Then i opened port 3306 to connect remotely and also bind my address to 0000
The Webserver EC2 instance, edit wp-config.php in /var/www/html/ folder to include Database Server MySQL information sudo vi wp-config.php.
Restart httpd sudo systemctl restart httpd
Disable the default page of Apache mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.conf_backup.
then install mysql client (yum install mysql ) on the webserver and open my web browser http://publicIP/wordpress

# Screenshots

![Screenshot (20)](https://user-images.githubusercontent.com/88409151/158022373-385bbf65-e75f-4e40-a9c3-380501721784.png)


![Screenshot (21)](https://user-images.githubusercontent.com/88409151/158022390-24e6c091-2703-4372-8c84-a39c357a6dc6.png)
