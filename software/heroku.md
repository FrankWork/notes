1. install virtualenv
	https://github.com/kennethreitz/python-guide/blob/master/docs/dev/virtualenvs.rst
	$ sudo pip install virtualenv
Basic usage:
	1) create a virtual environment for a project
		$ my_project_folder
		$ virtualenv venv
	virtualenv venv will create a folder in the current directory which will contain the Python executable files, and a copy of the pip library which you can use to install other packages. The name of the virtual environment (in this case, it was venv) can be anything; omitting the name will place the files in the current directory instead.
	This creates a copy of Python in whichever directory you ran the command in, placing it in a folder named :file:`venv`
	You can also use a Python interpreter of your choice.
		$ virtualenv -p /usr/bin/python2.7 venv
	This will use the Python interpreter in :file:`/usr/bin/python2.7`

	2)To begin using the virtual environment, it needs to be activated:
		$ source venv/bin/activate
	The name of the current virtual environment will now appear on the left of the prompt (e.g. (venv)Your-Computer:your_project UserName$) to let you know that it's active. From now on, any package that you install using pip will be placed in the venv folder, isolated from the global Python installation.

	Install packages as usual, for example:
		$ pip install requests

	3)If you are done working in the virtual environment for the moment, you can deactivate it:
		$ deactivate
	This puts you back to the system's default Python interpreter with all its installed libraries.
	To delete a virtual environment, just delete its folder. (In this case, it would be rm -rf venv.)

	After a while, though, you might end up with a lot of virtual environments littered across your system, and its possible you'll forget their names or where they were placed.

2 install postgres
	$ sudo apt-get install postgresql
	  正在将用户“postgres”加入到“ssl-cert”组中	  
	  config /etc/postgresql/9.3/main
	  data   /var/lib/postgresql/9.3/main
	  locale zh_CN.UTF-8
	  port   5432

	$ which psql
	 /usr/bin/psql

	新建用户，设置密码
	http://www.ruanyifeng.com/blog/2013/12/getting_started_with_postgresql.html
	 $ sudo -u postgres createuser --superuser pg_admin
	 $ sudo -u postgres psql
	  # \password pg_admin
      # \q
3 Heroku Toobelt
	$ sudo apt-get install ruby
	# Run this from your terminal:
	# Please ensure that you have Ruby installed.
	# wget -O- https://toolbelt.heroku.com/install-ubuntu.sh | sh

oops! i can not download the toobelt!!! i've downlad all the otherfucking 
stuff.

4 remove all the fucking stuff.

 sudo apt-get remove ruby
 sudo apt-get remove postgresql
 sudo pip install virtualenv
 sudo apt-get autoremove
