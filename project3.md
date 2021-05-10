In this project, we would be implementing a web solution based on MERN stack in AWS Cloud.

<img width="638" alt="MERN-stack" src="https://user-images.githubusercontent.com/10243139/117580145-6d74ac80-b0ee-11eb-9c51-7fe21409ea29.png">

MERN Web stack consists of following components:

- [ ]	MongoDB: A document-based, No-SQL database used to store application data in a form of documents.
- [ ]	ExpressJS: A server side Web Application framework for Node.js.
- [ ]	ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.
- [ ]	Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.


Step 1 - Backend configuration

a) Install Node.js on the server by running the following configurations:
	
- [ ]	To Update Ubuntu, run this command:
- [x]	sudo apt update

- [ ]	To Upgrade Ubuntu, run this command:
- [x]	sudo apt upgrade

- [ ]	Lets get the location of Node.js software from Ubuntu repositories:
- [x]	curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -

- [ ]	Install node.js with the following command:
- [x]	sudo apt-get install -y node.js 
- [ ]	(The command above installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu)
	
- [ ]	Verify the node installation with the command below:
- [x]	node -v
- [x]	npm -v

![1 a](https://user-images.githubusercontent.com/10243139/117580201-bdec0a00-b0ee-11eb-9f66-0ea41ab9d12e.jpg)

b) Application Code Setup:

- [ ]	Create a new directory for your To-Do project:
- [x]	mkdir Todo

- [x]	Run the command ls to verify that Todo directory has been created
	
- [ ]	Switch into Todo Directory with the command:
- [x]	cd Todo

- [ ]	Next, you will use the command npm init to initialise your project, so that a new file named package.json will be created:
- [x]	npm init
- [ ]	(You would need to press enter several times to accept the default values and proceed)

- [x]	Run the command ls to confirm that package.json is present

![1 b](https://user-images.githubusercontent.com/10243139/117580213-cf351680-b0ee-11eb-8545-0439140462ef.jpg)


c) Install ExpressJS:

- [ ]	To use express, install it using npm:
- [x]	npm install express

- [ ]	Now create a file index.js with the command below:
- [x]	touch index.js

- [x]	Run ls to confirm that your index.js file is successfully created

- [ ]	Install the dotenv module with this command:
- [x]	npm install dotenv

![1 c iv](https://user-images.githubusercontent.com/10243139/117580331-64d0a600-b0ef-11eb-8532-ee60f24ae7c6.jpg)

- [ ]	Open the index.js file with the command below:
- [x]	nano index.js

- [ ]	Type the code below into it:

		const express = require('express');
		require('dotenv').config();

		const app = express();

		const port = process.env.PORT || 5000;

		app.use((req, res, next) => {
		res.header("Access-Control-Allow-Origin", "\*");
		res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
		next();
		});

		app.use((req, res, next) => {
		res.send('Welcome to Express');
		});

		app.listen(port, () => {
		console.log(`Server running on port ${port}`)
		});
		
![1 c vi](https://user-images.githubusercontent.com/10243139/117580641-d4936080-b0f0-11eb-88e9-03fe94765bb1.jpg)

- [ ]	(Save and exit)	

- [ ]	Now it is time to start our server to see if it works. Open your terminal in the same directory as your index.js file and type:
- [x]	node index.js
- [ ]	(If every thing goes well, you should see Server running on port 5000 in your terminal.)

![1 c vii](https://user-images.githubusercontent.com/10243139/117580527-3bfce080-b0f0-11eb-8578-3b0abc917287.jpg)

- [ ]	We need to create an inbound rule to open port 5000 from the EC2 security group settings

![Port_5000 inbound rule](https://user-images.githubusercontent.com/10243139/117627622-43fc6500-b170-11eb-954d-0ae2eae05628.png)
	
- [ ]	Open up your browser and try to access your server’s Public IP followed by port 5000:
- [x]	http://PublicIP:5000

![1 c ix](https://user-images.githubusercontent.com/10243139/117580609-a57cef00-b0f0-11eb-938b-b69d0e70a3d2.jpg)

d) Routes

- [ ]	For each task, we need to create routes that will define various endpoints that the To-do app will depend on. So let us create a folder routes:
- [x]	mkdir routes

- [ ]	Change directory to routes folder:
- [x]	cd routes
	
- [ ]	Now, create a file api.js with the command below;
- [x]	touch api.js
	
- [ ]	Open the file with the command below:
- [x]	nano api.js
	
- [ ]	Copy below code in the file, save and exit:

		const express = require ('express');
		const router = express.Router();

		router.get('/todos', (req, res, next) => {

		});

		router.post('/todos', (req, res, next) => {

		});

		router.delete('/todos/:id', (req, res, next) => {

		})

		module.exports = router;
		
![1 d v](https://user-images.githubusercontent.com/10243139/117580771-7a46cf80-b0f1-11eb-89ac-e972a9f81830.jpg)

e) Models
	
- [ ]	Change directory back Todo folder with cd .. and install Mongoose:
- [x]	cd ..
- [x]	npm install mongoose

- [ ]	Create a new folder with mkdir models command:
- [x]	mkdir models

- [ ]	Change directory into the newly created ‘models’ folder with cd models:
- [x]	cd models

- [ ]	Inside the models folder, create a file and name it todo.js with this command:
- [x]	touch todo.js

![1 e](https://user-images.githubusercontent.com/10243139/117580888-fe00bc00-b0f1-11eb-8e78-4f3f2256595d.jpg)

- [ ]	Open the file created with nano todo.js then paste the code below in the file:

		const mongoose = require('mongoose');
		const Schema = mongoose.Schema;

		//create schema for todo
		const TodoSchema = new Schema({
		action: {
		type: String,
		required: [true, 'The todo text field is required']
		}
		})

		//create model for todo
		const Todo = mongoose.model('todo', TodoSchema);

		module.exports = Todo;

![1 e v](https://user-images.githubusercontent.com/10243139/117581069-d2320600-b0f2-11eb-8133-e135c09ccac1.jpg)

- [x]	Go back to Routes directory with the command cd /home/ubuntu/Todo/routes/
- [x]	Open api.js with nano api.js 
- [x]	delete the code inside and paste there code below:

		const express = require ('express');
		const router = express.Router();
		const Todo = require('../models/todo');

		router.get('/todos', (req, res, next) => {

		//this will return all the data, exposing only the id and action field to the client
		Todo.find({}, 'action')
		.then(data => res.json(data))
		.catch(next)
		});

		router.post('/todos', (req, res, next) => {
		if(req.body.action){
		Todo.create(req.body)
		.then(data => res.json(data))
		.catch(next)
		}else {
		res.json({
		error: "The input field is empty"
		})
		}
		});

		router.delete('/todos/:id', (req, res, next) => {
		Todo.findOneAndDelete({"_id": req.params.id})
		.then(data => res.json(data))
		.catch(next)
		})

		module.exports = router;

- [ ]	Save and Exit

f) MongoDB Database

- [ ]	We need a database where we will store our data, for this we will make use of mLab. You will need to sign up for a shared clusters free account, which is ideal for our use case. Sign up using this link: https://www.mongodb.com/atlas-signup-from-mlab
	
- [ ]	After signup, Click on Build a Cluster and create a shared cluster which is free and ideal for our test environment
	
- [ ]	Choose your cloud provider which is AWS in this instance and choose a region closest to you, in this case I choose us-east-1 and proceed to create the cluster


![1 f iii](https://user-images.githubusercontent.com/10243139/117581227-b54a0280-b0f3-11eb-97b7-a57d4da886e8.jpg)

- [ ]	Next you click on Database Access from the dashboard and add a new database user and select on password as authentication method.

- [ ]	Add a username and password, leave other setting as default and click on Add User

- [ ]	Next is to click on Network Access from the dashboard, followed by add ip address. Select allow access from anywhere and change the entry to 1 week instead of 6 hours, then click on confirm.
- [ ]	 Although this is not the best practice but it is okay for a test scenario.

- [ ]	Next on the Dashboard is clusters then click on Collections. Click on add my own data, add a database name and collection name and click on create
	
- [ ]	Create a file in your Todo directory and name it .env:
- [x]	touch .env

- [ ]	Add the connection string to access the database in it, just as below:
- [x]	nano .env 
- [ ]	( then input below into the file )
- [x]	DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
- [ ]	(Ensure to update <username>, <password>, <network-address> and <database> according to your setup)

- [ ]	Now we need to update the index.js to reflect the use of .env so that Node.js can connect to the database.
- [ ]	Simply delete existing content in the file, and update it with the entire code below:

		const express = require('express');
		const bodyParser = require('body-parser');
		const mongoose = require('mongoose');
		const routes = require('./routes/api');
		const path = require('path');
		require('dotenv').config();

		const app = express();

		const port = process.env.PORT || 5000;

		//connect to the database
		mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
		.then(() => console.log(`Database connected successfully`))
		.catch(err => console.log(err));

		//since mongoose promise is depreciated, we overide it with node's promise
		mongoose.Promise = global.Promise;

		app.use((req, res, next) => {
		res.header("Access-Control-Allow-Origin", "\*");
		res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
		next();
		});

		app.use(bodyParser.json());

		app.use('/api', routes);

		app.use((err, req, res, next) => {
		console.log(err);
		next();
		});

		app.listen(port, () => {
		console.log(`Server running on port ${port}`)
		});
- [ ]	Save and exit from the editor

- [ ]	Run the command:
- [x]	node index.js
- [ ]	(It is possible you come across this error but not to worry, we would just need to kill the process currently using the port 5000. You can find this solution with a simple google search)
- [ ]	To get the process using the port, use the command lsof -i tcp:5000

![1 f xi](https://user-images.githubusercontent.com/10243139/117581585-7b79fb80-b0f5-11eb-9cc6-92bcae56868f.jpg)

- [ ]	So to kill this process use the command:
- [x]	kill -9 <process-id>

- [x]	And run the node index.js command again, this time you shall see a message ‘Database connected successfully’

![1 f xii](https://user-images.githubusercontent.com/10243139/117581618-b7ad5c00-b0f5-11eb-9951-fcdfae3bc80a.jpg)


g) Testing Backend Code without Frontend using RESTful API

- [ ]	Download and install postman on your laptop using this link https://www.getpostman.com/downloads/
	
- [ ]	Now open your Postman, create a POST request to the API http://<PublicIP>:5000/api/todos ( make sure your set header key Content-Type as application/json )

- [ ]	Edit the body and send with POST

![1 g iii](https://user-images.githubusercontent.com/10243139/117581684-15da3f00-b0f6-11eb-98b4-20857515219f.jpg)

- [ ]	Receive with GET and click send

![1 g iv](https://user-images.githubusercontent.com/10243139/117581704-2b4f6900-b0f6-11eb-9ded-f53f5346ebcd.jpg)


Step 2 - Frontend creation

a) Running a React App

- [ ]	To start out with the frontend of the To-do app, we will use the create-react-app command to scaffold our app. Run the command in the Todo Directory:
- [x]	npx create-react-app client
- [ ]	(This will create a client folder inside the Todo folder)

![2 a i](https://user-images.githubusercontent.com/10243139/117581767-69e52380-b0f6-11eb-9bc8-0cf893e3e447.jpg)

- [ ]	Install concurrently, it is used to run more than one command simultaneously from the same terminal window
- [x]	npm install concurrently --save-dev

- [ ]	Install nodemon, it is used to run and monitor the server. If there is any change in the server code, nodemon will restart it automatically and load the new changes:
- [x]	npm install nodemon --save-dev

![2 a iii](https://user-images.githubusercontent.com/10243139/117581844-dcee9a00-b0f6-11eb-8ad5-04e0ef1992a8.jpg)

- [ ]	In Todo folder open the package.json file. Change the script part of the file and replace with the code below:
		
		"scripts": {
		"start": "node index.js",
		"start-watch": "nodemon index.js",
		"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
		},
		
b) Configure Proxy in package.json

- [ ]	Change directory to ‘client’:
- [x]	cd client
	
- [ ]	Open the package.json file and add the key value pair in the package.json file "proxy": "http://localhost:5000"
- [x]	nano package.json

- [ ] Add the key value pair in the package.json file:
- [x] "proxy": "http://localhost:5000"
- [ ] (This can be added to any part of the file)

- [ ]	Now, ensure you are inside the Todo directory, and simply do:
- [x]	npm run dev

![2 b iii](https://user-images.githubusercontent.com/10243139/117582022-f217f880-b0f7-11eb-8d2d-f4cc0365cb06.jpg)

- [ ]	Your app should open and start running on http://<PUBLIC-IP>:3000 

![2 b iv](https://user-images.githubusercontent.com/10243139/117582065-2095d380-b0f8-11eb-8e2a-6686c1b7b245.jpg)

- [ ]	In order to be able to access the application from the Internet you have to open TCP port 3000 on EC2, by adding a new Security Group rule


c) Creating your React Components

- [ ]	From your Todo directory run:
- [x]	cd client
	
- [ ]	Move to the src directory:
- [x]	cd src
	
- [ ]	Inside your src folder create another folder called components:
- [x]	mkdir components

- [ ]	Move into the components directory with:
- [x]	cd components
	
- [ ]	Inside ‘components’ directory create three files Input.js, ListTodo.js and Todo.js:
- [x]	touch Input.js ListTodo.js Todo.js

![2 c v](https://user-images.githubusercontent.com/10243139/117582139-72d6f480-b0f8-11eb-8ebd-7d1d2a3a8a9e.jpg)

- [ ]	Open Input.js file, and paste below code in it:

		import React, { Component } from 'react';
		import axios from 'axios';

		class Input extends Component {

		state = {
		action: ""
		}

		addTodo = () => {
		const task = {action: this.state.action}

    		if(task.action && task.action.length > 0){
     		 axios.post('/api/todos', task)
        		.then(res => {
         		  if(res.data){
            		      this.props.getTodos();
            		      this.setState({action: ""})
          		   }
        		})
        		.catch(err => console.log(err))
    		}else {
      		console.log('input field required')
    		}

		}

		handleChange = (e) => {
		this.setState({
		action: e.target.value
		})
		}

		render() {
		let { action } = this.state;
		return (
		<div>
		<input type="text" onChange={this.handleChange} value={action} />
		<button onClick={this.addTodo}>add todo</button>
		</div>
		)
		}
		}

		export default Input

- [ ]	Save and Exit

d) Make use of Axios, which is a Promise based HTTP client for the browser and node.js

- [ ]	Move to the src folder:
- [x]	cd ..
	
- [ ]	Move to clients folder:
- [x]	cd ..
	
- [ ]	Install Axios:	
- [x]	npm install axios
	
- [ ]	Go to ‘components’ directory:
- [x]	cd src/components

- [ ]	After that open your ListTodo.js file and insert the following code:

		import React from 'react';

		const ListTodo = ({ todos, deleteTodo }) => {

		return (
		<ul>
		{
		todos &&
		todos.length > 0 ?
		(
		todos.map(todo => {
		return (
		<li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
		)
		})
		)
		:
		(
		<li>No todo(s) left</li>
		)
		}
		</ul>
		)
		}

		export default ListTodo

- [ ]	Save and Exit
		
- [ ]	Then in your Todo.js file, write the following code:

		import React, {Component} from 'react';
		import axios from 'axios';

		import Input from './Input';
		import ListTodo from './ListTodo';

		class Todo extends Component {

		state = {
		todos: []
		}

		componentDidMount(){
		this.getTodos();
		}

		getTodos = () => {
		axios.get('/api/todos')
		.then(res => {
		if(res.data){
		this.setState({
		todos: res.data
		})
		}
		})
		.catch(err => console.log(err))
		}

		deleteTodo = (id) => {

		    axios.delete(`/api/todos/${id}`)
		      .then(res => {
			if(res.data){
			  this.getTodos()
			}
		      })
		      .catch(err => console.log(err))

		}

		render() {
		let { todos } = this.state;

		    return(
		      <div>
			<h1>My Todo(s)</h1>
			<Input getTodos={this.getTodos}/>
			<ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
		      </div>
		    )

		}
		}

		export default Todo;
		
- [ ]	Save and Exit

- [ ]	We need to make little adjustment to our react code, delete the logo and adjust our App.js file. 
- [ ]	Move to the src folder:
- [x]	cd ..


- [ ]	Make sure that you are in the src folder and open App.js

- [ ]	Copy and paste the code below into it:

		import React from 'react';

		import Todo from './components/Todo';
		import './App.css';

		const App = () => {
		return (
		<div className="App">
		<Todo />
		</div>
		);
		}

		export default App;
		
- [ ]	Save and exit from the editor

- [ ]	In the src directory open the App.css
- [ ]	then paste the following code into App.css:

		.App {
		text-align: center;
		font-size: calc(10px + 2vmin);
		width: 60%;
		margin-left: auto;
		margin-right: auto;
		}

		input {
		height: 40px;
		width: 50%;
		border: none;
		border-bottom: 2px #101113 solid;
		background: none;
		font-size: 1.5rem;
		color: #787a80;
		}

		input:focus {
		outline: none;
		}

		button {
		width: 25%;
		height: 45px;
		border: none;
		margin-left: 10px;
		font-size: 25px;
		background: #101113;
		border-radius: 5px;
		color: #787a80;
		cursor: pointer;
		}

		button:focus {
		outline: none;
		}

		ul {
		list-style: none;
		text-align: left;
		padding: 15px;
		background: #171a1f;
		border-radius: 5px;
		}

		li {
		padding: 15px;
		font-size: 1.5rem;
		margin-bottom: 15px;
		background: #282c34;
		border-radius: 5px;
		overflow-wrap: break-word;
		cursor: pointer;
		}

		@media only screen and (min-width: 300px) {
		.App {
		width: 80%;
		}

		input {
		width: 100%
		}

		button {
		width: 100%;
		margin-top: 15px;
		margin-left: 0;
		}
		}

		@media only screen and (min-width: 640px) {
		.App {
		width: 60%;
		}

		input {
		width: 50%;
		}

		button {
		width: 30%;
		margin-left: 10px;
		margin-top: 0;
		}
		}
		
- [ ]	Save and exit the Editor

- [ ]	In the src directory open the index.css and
- [ ]	copy the code below:

		body {
		margin: 0;
		padding: 0;
		font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
		"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
		sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		box-sizing: border-box;
		background-color: #282c34;
		color: #787a80;
		}

		code {
		font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
		monospace;
		}
		
- [ ]	Save and Exit the Editor

- [ ]	Go to the Todo directory

- [ ]	When you are in the Todo directory run:
- [x]	npm run dev


Assuming no errors when saving all these files, our To-Do app should be ready and fully functional with the functionality discussed earlier: 
- [ ]	creating a task, 
- [ ]	deleting a task and
- [ ]	viewing all your tasks.

![2 d xiii](https://user-images.githubusercontent.com/10243139/117583550-9b162180-b0ff-11eb-8874-c98199cbc7b2.jpg)


- [x]	In this Project MERN we have created a simple To-Do and deployed it to MERN stack.
- [x]	We wrote a frontend application using React.js that communicates with a backend application written using Expressjs.
- [x]	We also created a Mongodb backend for storing tasks in a database.
