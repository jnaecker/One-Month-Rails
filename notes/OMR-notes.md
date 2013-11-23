One Month Rails
============

## Installing the Programs You Need

coming soon

## Starting a New Application

To create a new application, type the command

	rails new app_name
	
To then run this app, you need to start the rails server:

	rails server
	
The app will be available by default on your local machine at http://localhost:3000/.  To quit the server, enter `cmd-C` at the command line.

## Git Setup

You should already have git installed and configured from the setup.  Check that your username and email are set with 

	git config -l
	
To start your git repo, navigate to the desired folder and run

	git init
	
To tell git to ignore certain files, add those filenames to the .gitignore file at the top of the directly. It's recommended to add the .DS_Store file here, for example.

To stage files, run

	git add .
	
from the top level of the directory. Then commit the files with 

	git commit -am "Initial commit"
	
The `-m` option allows to you add a message.  The `-a` option tells git to automatically stage deleted to modified files.