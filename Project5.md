# CLIENT SERVER ARCHITECTURE
Connecting two server. Server A will have mysql client this will connect to the mysql database on sever B.
SERVER CLIENT SETUP
I installed mysql client on the client server (sudo apt install mysql-client )
MYSQL SERVER SETUP
I setup my AWS server and named it mysql server.
I installed mysql server on the server (sudo apt install mysql-server).
Just as i did in project 1 with mysql installation and creation of a user that can access the mysql link here 
Then opened port 3306 in the mysql server security inbound rules and open the source to the client ip address.
I then bind the address to 0.0.0.0 in mysql configuration file (sudo vi /etc/mysql/mysql.conf.d/mysqld.cnf )
# CONNECTION OF CLIENT TO SERVER
i connected the client using mysql -u remote_user -h 172.31.95.186 -p "thats the server ip address".
Then got connected.

![Screenshot (17)](https://user-images.githubusercontent.com/88409151/157946542-8b743019-2b28-4e01-964c-13db41b272c6.png)
