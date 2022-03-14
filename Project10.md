# LOAD BALANCER SOLUTION WITH NGINX AND SSL/TLS
CONFIGURE NGINX AS A LOAD BALANCER
* I uninstall the apache from the exiting Load Balancer server
* So my /etc/hosts file are still well intact with IP addresses
* Install and configure Nginx as a load balancer to point traffic to the resolvable DNS names of the webservers
* Update the instance and Install Nginx

sudo apt update
sudo apt install nginx

Configure Nginx LB using Web Servers’ names defined in /etc/hosts
* Open the default nginx configuration file

sudo vi /etc/nginx/nginx.conf#

#insert following configuration into http section

 upstream myproject {
    server Web1 weight=5;
    server Web2 weight=5;
  }

server {
    listen 80;
    server_name www.domain.com;
    location / {
      proxy_pass http://myproject;
    }
  }

#comment out this line
#include /etc/nginx/sites-enabled/*;

* Restart Nginx and make sure the service is up and running

sudo systemctl restart nginx
sudo systemctl status nginx

# REGISTER A NEW DOMAIN NAME AND CONFIGURE SECURED CONNECTION USING SSL/TLS CERTIFICATES
* Register a new domain name with any registrar of your choice in any domain zone (e.g. .com, .net, .org, .edu, .info, .xyz or any other)

* Assign an Elastic IP to your Nginx LB server and associate your domain name with this Elastic IP
* Update A record in your registrar to point to Nginx LB using Elastic IP address
Check that your Web Servers can be reached from your browser using new domain name using HTTP protocol – http://<shally.ml>
![Screenshot (37)](https://user-images.githubusercontent.com/88409151/158105018-8c89ec88-d4bd-4386-9f0b-2818f87e1b49.png)

* Configure Nginx to recognize your new domain name
Update your nginx.conf with server_name www.<your-domain-name.com> instead of server_name www.domain.com
* Install certbot and request for an SSL/TLS certificate
 Make sure snapd service is active and running

sudo systemctl status snapd
Install certbot

sudo snap install --classic certbot
sudo ln -s /snap/bin/certbot /usr/bin/certbot
sudo certbot --nginx

Test secured access to your Web Solution by trying to reach https://<shally.ml>
![Screenshot (38)](https://user-images.githubusercontent.com/88409151/158105641-c5738adf-d065-40b3-8131-82126d39125c.png)

* Set up periodical renewal of your SSL/TLS certificate
You can test renewal command in dry-run mode

sudo certbot renew --dry-run

Best pracice is to have a scheduled job that to run renew command periodically. Let us configure a cronjob to run the command twice a day.

To do so, lets edit the crontab file with the following command:

crontab -e
Add following line:

* */12 * * *   root /usr/bin/certbot renew > /dev/null 2>&1
You can always change the interval of this cronjob if twice a day is too often by adjusting schedule expression.






