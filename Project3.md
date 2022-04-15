# Project WEB STACK IMPLEMENTATION (MERN STACK)
MongoDB ExpressJS ReactJS and NodeJS
Backend COnfiguration with NODEJS.
as usual i connected to my ec2 instances. did and update and upgrade on the server using sudo apt update && upgrade
So i downloaded the node js repository using curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
The i installed it using (sudo apt-get install -y nodejs) and checked the node using (node -v) and (npm -v) which is the package manager for installing node packages and dependencies.
i created a new directory (mkdir Todo) and navigate to the directory (cd Todo).
Then i initialize the project in the Todo direcory using (npm init) and accepted the default values and write out the file package.json.
then i used ls to check in the Todo folder if my package.json file is created.
# ExpressJS Installation
i used npm to install the express.js (npm install express)
then created a file index.js, then install dotenv module using (npm install dotenv)
i inserted a code into the .=index.js file using vim editor. its a server configuration thats pinting to port 5000 and listening to port 5000 as well which i opened on my ec2 instance security group.
then i used node index.js to check if my index,js file is connected to port 5000. and i checked it on web browser http://ip/5000 on port 5000
# ROUTES
The todo list need to use an end point HTTP request method of POST, GET and DELETE method.
First we make new directory (mkdir routes)
change directory to the routes (cd routes)
create a file in the folder and name it api.js then copied the connection router code to the file and write it on the file.
# Models and installation of MONGODB
first install mongoose inside the Todo directory using npm package (npm install mongoose)
we need to create and navigate to models directory (mkdir models && cd models)'
create a file named todo.js and open the todo.js file using vim
then i copied the connection code to the todo.js file write and saved it
i updated the api.js file with new code i copied from the page by mapping out the model directory and router.
# INSTALATION OF MONGODB DATABASE
First i created a new database on mLab as services solution and i selected shared cluster free account and AWS as service provider.
i allowed access to the database from anywhere as for testing and changed the time frame from 6hrs to 1week.
I created a MongoDB database on the mlab patform and coppied my cluster connection data so i can connect i used the node.js collection string.
Back to the server
I created and opened a new file in my Todo directory and named it .env then i paste the connection string copied from the mlab db cluster collection into the .env fileand saved it in it
Then io updated my index.js file to reflect the use of .env file so the node can connect to the mlab database.
i used vim to edit it and pasted the code into the file index.js
then i start my server with (node index.js and database was successfully connected)
# RESTFUL API
POSTMAN this is a resful api development that is used to test API.
# INSTALLATION AND CONFIGURATION OF POSTMAN
I downloaded and install postman software on my machine then i created a POST request to the Api and set my header key content-Type as application/json
Then created a GET rquest api request to get records from the database and sent it as a response to GET request.
Front end creation. (this is the part that will be shown on the web browser)
FIrst in my Todo directory used npx create-react-app client to scrfold the app which created a folder called client which is the place i added all my react code
RNUUNING THE REACT APP
First i need to install all dependencies that reacts need to use to run or app ( npm install concurrently --save-dev) (npm install nodemon --save-dev) the nodemon is used to monitor the server also used to restart theserver if there are changes in the code.
i changed some code in the package.json file in the Todo folder ("scripts": {"start": "node index.js","start-watch": "nodemon index.js","dev": "concurrently "npm run start-watch" "cd client && npm start""},) and saved it.
Next i configured the package.json proxy.
i cd to the client directory, used vim to edit my package.json file
Then i added a key value pair to the package.json file proxy using ("proxy": "http://localhost:5000".)
Then i checked if im in the right directory which is Todo directory and i run (npm run dev) and it shows app is running on localhost:3000. then i opened the port in my ec2 security group to port 3000
Creating the react component
in my todo app i cd to client directory and cd to src directory, in src directory i make another directory called components (mkdir components) and cd into the components directory (cd components)
I created 3 seperate files named Input.js, ListTodo.js and Todo.js respectively. (touch Input.js ListTodo.js Todo.js).
then copied the code into the Input.js file.
then i cd into the clients folder and install axios in the folder using (npm install axios)
then cd back to the src/component folder and opend the ListTodo.js file copied and paste the react code into it, saved it.
edited my Todo,js and paste the react code in it also.
Cd back to my src folder and edited the App.js file by pasting the react code in it
Also editied the App.css file and pasted the css code in it
I did edited the index.css file also
Then cd back to the Todo folder (cd ../..)
and ran npm run dev
checked my app on http://localhost:3000 port 3000 and it was sucessfull
PROBLEMS ENCOUNTERED
The probelem i encounter was that i was runnung a code on client which is meant to be on the Todo directory itself.


# Screenshot


![Screenshot 2022-03-11 070953](https://user-images.githubusercontent.com/88409151/157842600-f592701d-25b8-46e2-b434-7b9f9ca56ca1.png)


![Screenshot 2022-03-11 071316](https://user-images.githubusercontent.com/88409151/157842720-c5518566-8bec-4104-ab45-8c33bfc2bd27.png)


![Screenshot 2022-03-11 075009](https://user-images.githubusercontent.com/88409151/157842841-5d6f69de-710e-4e7f-9ccb-3d977d8efbc8.png)

![Screenshot 2022-03-11 080554](https://user-images.githubusercontent.com/88409151/157842947-66b510f4-43f8-4261-9594-8c6a6bc87544.png)


![Screenshot 2022-03-11 080757](https://user-images.githubusercontent.com/88409151/157843100-70a090b5-f63a-4531-b272-1c1c7c49b6c7.png)


![Screenshot (5)](https://user-images.githubusercontent.com/88409151/157843257-8430c42a-032d-40aa-b3c3-9ab618025c3d.png)

![Screenshot (6)](https://user-images.githubusercontent.com/88409151/157843315-352e06d4-ad9c-4e66-b056-9212bef6839c.png)




