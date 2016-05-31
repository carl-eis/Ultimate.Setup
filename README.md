# Official Linux Setup
-----
This is my official linux setup document.
It contains all the things you'll need to install to get you started in linux.

Please check the "wiki" section to see more. I've moved most of the content from the wiki to the readme file, for easier viewing and editing.

----
# Getting Started
   
The dollar sign is your linux terminal prompt. When following this guide run any command by typing only what is given after the dollar sign followed by the enter key.  For example when given:
         
    $ echo this

Enter `echo this` into your terminal followed by the enter key.
In this case `echo` just prints its arguments but it can do more. 

You can read more about each command we use by running `man` command. Which will give you the manual page for that command. In this case you would get it by running:

    $ man echo

To exit the man pages simply type `q`

### 1. Update and Install Common Dependencies

#### 1.1 Update packages
First we update the list of available packages and their versions:
    
    $ sudo apt-get update

(We use `sudo` when installing things as `sudo` runs the rest of the command as the root user who has all the admin rights.)

#### 1.2 Upgrade packages

Then we upgrade all installed packages to the new versions in the list:
    
    $ sudo apt-get upgrade

#### 1.3 Install dependencies
Now install the latest versions of a list of programs which other tools we use often depend on: 
    
    $ sudo apt-get install g++ gcc make libc6-dev patch openssl ca-certificates libreadline6 libreadline6-dev curl zlib1g zlib1g-dev libssl-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev autoconf libc6-dev libgdbm-dev libncurses5-dev automake libtool bison pkg-config libffi-dev libcurl3 php5-curl git zsh
(Here `sudo apt-get install` is the command and the rest is a list of programs to install.)
    
### 2. Install important programs

These have been included in the list at point 1.3 but they are important later in this guide so they also get to have their own points. **You don't need to run these commands!**

#### 2.1  Install git

`git` is the most widely used version control system in the world.
 
    $ sudo apt-get install git

#### 2.2 Install zsh

`zsh` is a replacement for bash (the shell/program that runs your terminal) it adds the ability to use Oh-My-Zsh community plugins and themes to optimise your terminal workflow as well as more nice things which you can google. 
    
    $ sudo apt-get install zsh

#### 2.3 Change default shell
Now that `zsh` is installed we need to change our default shell from `bash` to `zsh`.

First we change the shell by running the change shell (`chsh`) command and giving it the save flag (`-s`) to make the change permanent:

    $ sudo chsh -s $(which zsh)
    $ chsh -s $(which zsh)
    $ sudo shutdown -r 0

Then we check that the change worked by printing the current shell variable, `echo` prints its arguments and `$` is used to access shell variables. 

    $ echo $SHELL

If it does not return something like */usr/bin/local/zsh* or anything containing *"zsh"* then you should ask for help in getting that to work. If the change was successful **restart your terminal** before the next step.

#### 2.3 Install Oh-My-Zsh

To install Oh-My-Zsh run the following command:

    $ curl -L http://install.ohmyz.sh | sh

#### Sublime Text 3

Before we start setting up Oh My Zsh, we'll need to install a good text editor. Here are the instructions required to install sublime text 3.

    $ cd ~/Downloads
    $ wget https://download.sublimetext.com/sublime-text_build-3103_amd64.deb ~/Downloads
    $ sudo dpkg -i sublime-text_build-3103_amd64.deb
    $ sudo apt-get install -f


#### 2.4 Oh-My-Zsh  Setup
This setup will use with a theme and plugins we like. You can customise Oh-My-Zsh to your own personal needs.

First we will install a powerline enabled font for use in terminal so we can take advantage of powerline icons in our themes:

Start by downloading the font using the following command.

    $ git clone https://github.com/pdf/ubuntu-mono-powerline-ttf.git ~/.fonts/ubuntu-mono-powerline-ttf 
    
    $ fc-cache -vf

Then navigate to your preferences in terminal and manually set the font to Ubuntu Mono Powerline.

Remember to change your terminal colour theme to **Solarized Dark**.

Afterwords a restart of terminal may be required. For more color schemes click [here](https://apps.owncloud.com/stories/Steven+Harms:+Gnome+Terminal+Color+Schemes?id=106857&PHPSESSID=c61db5c362562ce4c9006abfb273a6b7). 

Finally open up ~/.zshrc (a hidden config file `zsh` created in your home directory). Change the theme to `agnoster` and add any plugins you wish to use. 

    $ subl ~/.zshrc
    $ nano ~/.zshrc 

For a list of plugins and available themes and more on Oh-My-Zsh consult their [GitHub](https://github.com/robbyrussell/oh-my-zsh) or [Website](http://ohmyz.sh/).


### 3. Setup Ruby Environment

Setup the basics for a Ruby development environment for work using gems, Rails and other Ruby based tools.

#### 3.1  Install `rbenv`

`rbenv` is a brilliant tool for managing different versions of ruby on different projects and different gemsets (set of ruby plugins) over different projects.

First we download it by cloning the repo:
      
    $ git clone https://github.com/sstephenson/rbenv.git ~/.rbenv

Then we add it to our `zsh` path so that we can use it in terminal.

    $ echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.zshrc
    $ echo 'eval "$(rbenv init -)"' >> ~/.zshrc

Finally we check that the whole process worked:

    $ type rbenv
        
#### 3.2  Install `ruby-build` and `gem-rehash`  for `rbenv`

Now we can manage different ruby versions and gems very easily though we still need an easier way to install them in the first place. Enter `ruby-build` and `gem-rehash`. 

Once again we clone the repos:
    
    $ git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
    
    $ git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash

For a list of available ruby versions run:

    $ rbenv install -l

Pick the appropriate one and install it with:
    
    $ rbenv install 2.1.2
    $ rbenv install [version number]

To set the newly installed version as your global ruby version run:

    $ rbenv global 2.1.2
    $ rbenv global [version number]

Installing gems globally should now be equally easy.
 For example to install Rails (one of the our favourite web frameworks) simply run:

    $ gem install rails

### 4. Setup Node Environment

Setup the basics for a Node.js development environment for work using npm packages, Meteor, Express.js, Harp.js and other Node based tools.

#### 4.1  Install `nvm`
    $ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.0/install.sh | bash
    $ git clone https://github.com/creationix/nvm.git ~/.nvm
    $ source ~/.nvm/nvm.sh

#### 4.2  Install `npm`   
    $ sudo apt-get install npm
    $ npm -v

#### 4.3 Install `bower`   
    $ sudo npm install -g bower

#### 4.3.2 Link bower to nodejs
    $ sudo ln -s /usr/bin/nodejs /usr/bin/node
    $ bower -v

### 5. Finally, install Node.js
####5.1 Grab latest node.js version in terminal
    $ nvm install node
####5.2 List all installed node.js versions 
    $ nvm ls
####5.3 Select the latest version of node for use
    $ nvm use v6.0.0
    (or whichever version it is you desire)
####5.4 Troubleshooting node install
    $ nvm ls
    $ nvm use stable
    $ nvm install stable

###6. Install Ember
###6.1 Install Ember Globally
    $ sudo npm install -g ember-cli

###7. More Troubleshooting
####7.1
    $ sudo npm cache clean -f
    $ sudo npm install -g n
    $ sudo n stable
    $ node -v
    $ nvm use v6.0.0
    $ nvm current
####7.2 Extra Dangerous, if nothing works:
    $ n=$(which node);n=${n%/bin/node}; chmod -R 755 $n/bin/*; sudo cp -r $n/{bin,lib,share} /usr/local
    
###DONE!


---


#Other Cool Things
We have some other cool programs that are really great to use for creating static sites. My favourite one so far is called Wintersmith, and can be found at www.wintersmith.io

###1. Install Wintersmith
	$ npm install wintersmith -g

###2. Create new project
	$ wintersmith new <path> OR .
	$ cd yourPathHere

###3. Install Dependencies
	$ npm install wintersmith-node-sass --save-dev
	$ npm install wintersmith-handlebars --save-dev
	$ npm install  wintersmith-livereload --save-dev

###4. Run your site
Make sure you're in the site directory (herp derp.)
Then run this:

	$ wintersmith preview
	
It runs on localhost:8080

Running

	$ wintersmith build

Puts your site in the /build directory for distribution. For more details, visit https://github.com/jnordberg/wintersmith#quick-start
> This guide was written by Codelab.io using [StackEdit](https://stackedit.io/).