1) IP address and SSH port number of my server is : 52.66.183.142 and 2200
2) The complete url to hosted Item catalog web application is : http://52.66.183.142
3) list of softwares installed is as follows:
	a) apache2
	b) libapache2-mod-wsgi
	c) postgresql
	d) Python-pip
	e) Flask, httplib2, requests, oauth2client, sqlalchemy
	f) git

4) list of configuration changes to make the server up and running are as under:
	a) Change the ssh port from 22 to 2200
		* On Amazon Lightsail homepage, open the networking tab and add a custom rule to allow tcp connection from port 2200.
		* Then connect to your instance and run the following commands in order to configure the firewall.
			i. sudo ufw default deny incoming
			ii. sudo ufw default allow outgoing
			iii. sudo ufw allow www
			iv. sudo ufw allow ntp
			v. sudo ufw allow 2200/tcp
			vi. sudo ufw enable

	b) Create a new user grader by command "sudo adduser grader"

	c) Give grader the permission to sudo by adding it in directory /etc/sudoers.d.

	d) Create an ssh keypair for grader
		* Run command "ssh-keygen" on your local machine and give a <name> to file when prompted for the same.
		* Two files starting with given <name> and one of those ending with .pub extension will be created.
		* login to the server and create a .ssh directoryin home folder by running command "mkdirectory.ssh"
		* Run "cd .ssh" and create a new file by command "touch authorized_keys"
		* Run "sudo vim authorized_keys" and paste the contents of file <name>.pub from local machine.
		* logout and login with command ssh -i <name> grader@52.66.183.142 -p 2200


	e) Run "cd /var/www" and make a new directory FlaskApp there by command "mkdir FlaskApp"

	f) Run "cd FlaskApp" and clone github repo of Item Catalog app over there by running the command "git clone https://github.com/mgoyal123/Item-Catalog.git"

	g) Add a wsgi file in FlaskApp folder and a FlaskApp.conf file in /etc/apache2/sites-available/ folder.

	h) Run command "sudo a2ensite FlaskApp.conf" and "sudo service apache2 restart" to restart the apache with current configurations.

	i) Visit the site with ip "52.66.183.142" on your browser.
