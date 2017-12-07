# Linux Server Configuration
### Quickstart
* **IP address** and **SSH** port number of the server is : _52.66.183.142_ and _2200_
* The complete **url to hosted Item catalog web application** is : _http://52.66.183.142_
* List of softwares installed is as follows:
	* apache2
	* libapache2-mod-wsgi
	* postgresql
	* Python-pip
	* Flask, httplib2, requests, oauth2client, sqlalchemy
	* git

### Configuration
* Change the ssh port from 22 to 2200
	* On **Amazon Lightsail** homepage, open the networking tab and add a custom rule to allow tcp connection from port _2200_.
	* Then connect to your instance and run the following commands in order to **configure the firewall**.
		* `sudo ufw default deny incoming`
		* `sudo ufw default allow outgoing`
		* `sudo ufw allow www`
		* `sudo ufw allow ntp`
		* `sudo ufw allow 2200/tcp`
		* `sudo ufw enable`

* Create a **new user grader** by command `sudo adduser grader`

* Give grader the **permission to sudo** by adding it in directory _/etc/sudoers.d_.

* Create an **ssh keypair** for grader
	* Run command `ssh-keygen` on your local machine and give a <name> to file when prompted for the same.
	* Two files starting with given <name> and one of those ending with _.pub extension_ will be created.
	* login to the server and create a **.ssh directory** in home folder by running command `mkdirectory.ssh`
	* Run `cd .ssh` and create a new file by command `touch authorized_keys`
	* Run `sudo vim authorized_keys` and paste the contents of file _<name>.pub_ from local machine.
	* logout and login with command `ssh -i <name> grader@52.66.183.142 -p 2200`

* Run `cd /var/www` and make a new directory _FlaskApp_ there by command `mkdir FlaskApp`

* Run `cd FlaskApp` and **clone github repo** of Item Catalog app over there by running the command `git clone https://github.com/mgoyal123/Item-Catalog.git`

* Add a **wsgi file** in _FlaskApp_ folder and a **FlaskApp.conf** file in _/etc/apache2/sites-available/_ folder.

* Run command `sudo a2ensite FlaskApp.conf` and `sudo service apache2 restart` to **restart the apache** with current configurations.

* Visit the site with ip _52.66.183.142_ on your browser.

### License
The contents of this repository are covered under the MIT License.