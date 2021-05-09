In this project, we would be implementing a web solution based on MERN stack in AWS Cloud.

<img width="638" alt="MERN-stack" src="https://user-images.githubusercontent.com/10243139/117580145-6d74ac80-b0ee-11eb-9c51-7fe21409ea29.png">

MERN Web stack consists of following components:

- [ ]	MongoDB: A document-based, No-SQL database used to store application data in a form of documents.
- [ ]	ExpressJS: A server side Web Application framework for Node.js.
- [ ]	ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.
- [ ]	Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.


Step 1 - Backend configuration

a) Install Node.js on the server by running the following configurations:
	
- [ ]	Update Ubuntu:
- [x]	sudo apt update

- [ ]	Upgrade Ubuntu:
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
