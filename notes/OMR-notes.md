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

## Git

### Git Setup

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

To see if you have files that are modified or staged, run

	git status
	
Suppose we accidentally delete something important.  To get back the last committed version of the directory, run

	git add .
	git checkout -f
	
You can checkout a specific file, but the `-f` option just checks out everything.

### Github Setup

Make sure you have an account at [Github](github.com).  To make it faster to push and pull from Github, add an ssh key by following the directions [here](https://help.github.com/articles/generating-ssh-keys).

On Github, create a new repository and give it a useful name.  Then follow the instructions on the page to push your existing repo to Github:

	git remote add origin git@github.com:jnaecker/One-Month-Rails.git
	git push -u origin master
	
### Git Workflow

The typical workflow is as follows:  After making some changes to our files and saving those changes, stage the changes for commit, commit them, and push the commit to Github:

	git add .
	git commit -m "Message"
	git push

## Creating Your Homepage

Navigate to your `pinteresting` folder and start the server with

	rails server
	
You can see the result at [http://0.0.0.0:3000](http://0.0.0.0:3000).  To make a new page, run

	rails generate controller pages home
	
This page is viewable at [http://0.0.0.0:3000/pages/home](http://0.0.0.0:3000/pages/home).  To edit it, navigate to `pinteresting/app/views/pages/home.html.erb`.  You can then make any edits you want to the page contents.

## Setting the Root Path

Find routes in the file `config/routes.rb`.  Currently, this says that there is a page at http://0.0.0.0:3000/pages/home.  To make the default landing page point here, chance the second line of the routes file to `root pages#home`.


