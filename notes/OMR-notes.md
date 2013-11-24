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

## Creating Pages

### Creating Your Homepage

Navigate to your `pinteresting` folder and start the server with

	rails server
	
You can see the result at [http://0.0.0.0:3000](http://0.0.0.0:3000).  To make a new page, run

	rails generate controller pages home
	
This page is viewable at [http://0.0.0.0:3000/pages/home](http://0.0.0.0:3000/pages/home).  To edit it, navigate to `pinteresting/app/views/pages/home.html.erb`.  You can then make any edits you want to the page contents.

### Setting the Root Path

Find routes in the file `config/routes.rb`.  Currently, this says that there is a page at http://0.0.0.0:3000/pages/home.  To make the default landing page point here, chance the second line of the routes file to `root pages#home`.

### Creating More Pages

There are three steps to creating a new page for your app (in this case an about page):

First, add a new action in the controller.  In `apps/controllers/pages_controller.rb` add

	def about
	end
	
Second, add the content for this page in the view.  Create the file `app/views/pages/about.html.erb` and then add some html.

Third, add a route for this new page.  In `config/routes.rb`, add this line:

	get "about" => "pages#about"
	
### Embedded Ruby

Normally you would create a link in html like so:

	<a href="link.com">here<a>
	
However, note that our homepage is actually an .erb file, standing for Embedded Ruby.  This means we can add small snippets of Ruby to what otherwise looks like an html file.   In general embedded Ruby occurs between these tags:

	<%= [ruby function] %>
	
To add make a link, for example:

	<%= link_to "here", "#" %>

This calls the Ruby function `link_to` with two arguments.\

### Creating Navigation Links

The line
	
	get "about" => "pages#about"
	
in our `config/routes.rb` creates the variable `about_path`.  We can use this to link from our home page to the about page by adding

	<%= link_to "about", about_path %>
	
to our `home.html.erb`.   We could add a similar link to the about page back the home page.  We could even add both links to the top of both pages to have a consistent menu of links across pages.

However, maintenance of this link set can get annoying, since we have the same set of links copied in different pages.  There is a centralized way to do this: the file `app/views/layouts/application.html.erb` contains information that is shared by all pages in our app.  For example, you'll note the html `<title>Pinteresting</title>`, which gives each page the same title.

In the body of this file, we can add

	<%= link_to "Home", root_path %>
	<%= link_to "About Us", about_path %>
	
This will add the given links to every page in our app.

## Bootstrap

### Installing Bootstrap

Gems are a simple way to include extensions to Ruby.  They are stored in your `Gemfile`.  Groups are used to tell which gems should be active when (eg development vs deployment).

[Bootstrap](http://getbootstrap.com/) is a gem for making a nice front-end with icons, menus, navbars, etc.  Bootstrap was recently updated, so we have to tell the Gemfile to get a particular version from Github.  In `Gemfile`, add 

	gem 'bootstrap-sass', github: 'thomas-mcdonald/bootstrap-sass', branch: '3'
	
Then at the top of the directory, run

	bundle install
	
to install all the gems in the `Gemfile` (and their dependencies).

To get bootstrap running, create a new file `app/assets/stylesheets/bootstrap_and_customization.css.scss`.  (The name is actually not important.  The file `applications.css` automatically combines all the files in the `stylesheets` directory to run in your app.)

`.scss` files are precompilers for CSS.

To the new `.scss` file you just created, add the line

	@import 'bootstrap;'
	
When you restart your server (as you'll need to do every time you add a new gem), you'll notice the much nicer formatting for your app pages.

### Adding Bootstrap Elements

#### Containers

To align our page contents more nicely, we go to `app/views/layouts/application.html.erb`.  Recall that this is sort of the master template for all of our app pages.  The content of all the pages is stored in the variable `yield`, so to align our content, modify the file as so:

	<div class="container">
			<%= yield %>	
	</div>
	
#### Adding a Navbar

We can just copy the default navbar code from Bootstrap.  However, it is cleaner to create a file `apps/view/layouts/_header.html.erb`.  This is called a *partial*.   To then link to this partial, add the line

	<%= render 'layouts/header' %>
	
at the desired location in your `applications.html.erb`.  Then add the desired navbar html from the Bootstrap site.  To get the dropdown menu to work, add bootstrap to your `app/assets/javascripts/application.js`:

	//= require bootstrap

#### Viewports

To get your app to look right on mobile devices, add

	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	
inside the `<head>` tags in your `/app/views/layout/application.html.erb`.
	
#### Jumbotron

To get the Jumbotron look on your homepage, wrap the header and other content you want is <div> tags like so:
	
	<div class="jumbotron">
		<h1>Welcome to my app!</h1>
		<p>Sign up <%=	link_to "here", "#" %>.</p>
	</div>

#### Buttons

You can add buttons as specified on the Bootstrap website:

	<button type="button" class="btn btn-default">Default</button>

But the `link_to` function also allows takes an argument `class` that allows you to make a button another way:

	<p>Click here to <%= link_to "sign up", "#" , class: "btn btn-primary btn-lg" %></p>

### Customizing Bootstrap

You can edit the color and appearance by directly editing the CSS, but you can also add *LESS* variables in your `bootstrap_and_customization.css.scss` file, above the `@import` line.  These variables are listed [here](http://getbootstrap.com/customize/#less-variables).  Note that they start with `@`, but since we are using the bootstrap gem, all of these will start with `$` instead.

#### Color

Change the background color:

	$body-bg: red;
	
The basic colors are a bit to intense, so recommend checking out [http://flatuicolors.com/](http://flatuicolors.com/).  Clicking a color copies the hex code for that color to your clipbaord

	$body-bg: #3498db;
	
Navbar background color and link color:
	
	$navbar-default-bg: #2980b9;
	$navbar-default-link-color: white;

Jumbotron background color:

	$jumbotron-bg: white;
	
#### Fixed Navbar to Top

You can change the `class` attribute of your navbar to make it fixed to the top of the page:
	
	<nav class="navbar navbar-default navbar-fixed-top" role="navigation">
	
Note that you'll have to add padding to the body of your pages now; otherwise the navbar will sit on top of some of your content.  This can be controlled through CSS as welll, by adding the following to your `bootstrap_and_customization.css.scss` file:

	body { padding-top: 70px; }



	
	