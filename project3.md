In this project, we would be implementing a web solution based on MERN stack in AWS Cloud.

MERN Web stack consists of following components:

MongoDB: A document-based, No-SQL database used to store application data in a form of documents.
ExpressJS: A server side Web Application framework for Node.js.
ReactJS: A frontend framework developed by Facebook. It is based on JavaScript, used to build User Interface (UI) components.
Node.js: A JavaScript runtime environment. It is used to run JavaScript on a machine rather than in a browser.


Step 1 - Backend configuration

a) Install Node.js on the server by running the following configurations:
	
-[x]	Update Ubuntu:
		-[ ]  sudo apt update

	ii)	Upgrade Ubuntu:
		sudo apt upgrade
	iii)	Lets get the location of Node.js software from Ubuntu repositories:
		curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
	iv)	Install node.js with the following command:
		sudo apt-get install -y node.js 
		(The command above installs both nodejs and npm. NPM is a package manager for Node like apt for Ubuntu)
	v)	Verify the node installation with the command below:
		node -v
		npm -v