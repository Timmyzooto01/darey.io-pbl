# MEAN STACK DEVPLOYMENT TO UBUNTU IN AWS
MongoDB Express Angular Nodejs
Setting up Ubuntu server
as usual i created a new ec2 instance and connected to my ec2 instances. did and update and upgrade on the server using sudo apt update && upgrade
NodeJs installation.
i installed nodeJs with (sudo apt install -y nodejs)
MongoDB installation
First i downloaded the key using (sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6)
and echo the deb file from the repository using (echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list)
Then install the mongod using (sudo apt install -y mongodb)
i did start the mongodb sever (sudo servece mongodb start)
Then checked the status of my server if its running using (sudo systemctl status mongodb ) which is running
next i installed the node package manager npm (sudo apt install -y npm) using aptitude package
also installed the body-paser a node package that process json files request. (sudo npm install body-parser)
Creation of the server folder and configuration
i created the server and cd in into the folder named books (mkdir Books && cd Books)
I intialize npm in the books folder (npm init )
Then created a file named server.js (vim server.js ) and copied the webserver code into it (var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
console.log('Server up: http://localhost:' + app.get('port'));
});)
# EXPRESS AND MONGOOSE INSTALATION
I installed express using (sudo npm install express mongoose)
Then in the Book folder i created a new directory folder named apps then cd into the apps folder (mkdir apps && cd apps)
i creates a new file named routes.js and pasted the code into it( its the json code)
Then in the apps folder i created a folder named models and cd into the folder models (mkdir models && cd models)
in the models folder i created a new file named book.js which will hold the connection code for the mongoosedb connections
ACCESSING THE ROOT WITH ANGULARJS
I cd back into the Books directory and created a folder called public also cd into the public folder (mkdir public && cd public)
Then, i created a new file called script.js did a copy and pate the controller configuration code for angular into the script.js
I then create a file called index.htm in the public folder and pasted an html web cod into the file index.html
then i cd back into the books directory. (cd.. )
I did start my sever using (node server.js)
Then i checked my server is connected on localhost port 3300 using (curl -s http://localhost:3300)
also added and opened the port fot 3300 in my ec2 inbound security rules
then i checked my server on web browser using (http://ip:3300)
and i added a new register
PROBLEMS ENCOUNTERED
The problem was the npm is not installing which i have to install aptitude 
sudo apt install aptitude
then install your package with aptitude
sudo aptitude install npm
then it later worked fine 


# Screenshot


![Screenshot (10)](https://user-images.githubusercontent.com/88409151/157887254-ec1344df-796c-4cce-b3a3-a53183ae458d.png)


