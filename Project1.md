
## WEB STACK IMPLEMENTATION (LAMP STACK) IN AWS
A LAMP Stack is a set of open-source software that can be used to create websites and web applications. LAMP is an acronym, and these stacks typically consist of the Linux operating system, the Apache HTTP Server, the MySQL relational database management system, and the PHP programming language.

A LAMP means (Linux, Apache, MySQL, PHP or Python, or Perl)

Linux: The operating system. Linux is a free and open source operating system (OS) that has been around since the mid-1990s. Today, it has an extensive worldwide user base that extends across industries. Linux is popular in part because it offers more flexibility and configuration options than some other operating systems.

Apache: The web server. The Apache web server processes requests and serves up web assets via HTTP so that the application is accessible to anyone in the public domain over a simple web URL. Developed and maintained by an open community, Apache is a mature, feature-rich server that runs a large share of the websites currently on the internet. 

MySQL: The database. MySQL is an open source relational database management system for storing application data. With My SQL, you can store all your information in a format that is easily queried with the SQL language. SQL is a great choice if you are dealing with a business domain that is well structured, and you want to translate that structure into the backend. MySQL is suitable for running even large and complex sites. See "SQL vs. NoSQL Databases: What's the Difference?" for more information on SQL and NoSQL databases.

PHP, PYTHON OR PERL: The programming language. The PHP open source scripting language works with Apache to help you create dynamic web pages. You cannot use HTML to perform dynamic processes such as pulling data out of a database. To provide this type of functionality, you simply drop PHP code into the parts of a page that you want to be dynamic. 

## HOW TO CREATE AN EC2 INSTANCE 

We need to create a AWS  account, log into the cloud services and create an EC2 Ubuntu instance running on 22.04 version instance type T2 micro. Creating an instance would require you to create and choose a Keypair which automatically downloads a private key(*.pem) on your computer, and then launch instance. 

![Ist Image](https://github.com/laola234/Darey.io-Projects-/assets/136293714/fe327f6c-6139-4ee5-9c45-c743c8e1abc3)

After connecting to an instance machine, i followed the 4 steps by opening first Open a terminal, then open an SSH client, Locating my private key file. i.e The key used to launch the instance, Kitan.pem, run command if neccesary then connect to my instance using its Public DNS:
To locate the private key file, ensure you change directory in your terminal by typing cd space download in your terminal 

Connect to your instance using its Public DNS: by using the command below 

ssh -i "Kitan.pem" ubuntu@ec2-18-117-166-177.us-east-2.compute.amazonaws.com

![image 2](https://github.com/laola234/Darey.io-Projects-/assets/136293714/e6d67436-6d48-4999-ae4f-df7b2df47b97)

Configuring EC2 machine to serve a Web server!

### INSTALLING APACHE AND UPDATING THE FIREWALL

We need to install Apache using Ubuntu’s package manager ‘apt’:

#update a list of packages in package manager

sudo apt update

sudo apt install apache2

To verify that apache2 is running as a Service in our OS, i used following command:

sudo systemctl status apache2

![image 3](https://github.com/laola234/Darey.io-Projects-/assets/136293714/de656743-8389-40ae-8a4d-912f653d9414)

If it shows green and running, that means a Web Server has just been launched in the Clouds!

## We need to add a rule to EC2 configuration to open inbound connection through port 80:

When the instance is created, we have a default TCP rule on port 22 opened which is useful for SSH connection to a terminal. In order to ensure that our webpage are being acccessed on the internet, we need to open a TCP port 80 inbound rule.

![image 4](https://github.com/laola234/Darey.io-Projects-/assets/136293714/aecbcbb5-f86d-4f38-8223-765f0e7236d7)

 We can access it locally in our Ubuntu shell, by running the following command:

 curl http://localhost:80 or curl http://127.0.0.1:80

![image 5](https://github.com/laola234/Darey.io-Projects-/assets/136293714/422df696-65f4-4f1b-bc68-950213c0ed77)

We need to test that the Apache HTTP server can respond to requests from the Internet.

Open a web browser of your choice and try to access following url

http://<Public-IP-Address>:80

![image 6](https://github.com/laola234/Darey.io-Projects-/assets/136293714/abcdc0e4-67c9-470c-91d8-8eae643a174b)

### INSTALLING MYSQL

We need to install a Database Management System (DBMS) to be able to store and manage data for our site in a relational database.

Use ‘apt’ to acquire and install this software with the following command

![image 7](https://github.com/laola234/Darey.io-Projects-/assets/136293714/a829804a-d73d-4c8c-915d-63526bb3a83e)

When the installation is finished, log in to the MySQL console by typing:

$ sudo mysql

![image 8](https://github.com/laola234/Darey.io-Projects-/assets/136293714/8a255335-5896-47ab-a5ef-beb637e08ace)

It’s recommended that you run a security script that comes pre-installed with MySQL. This script will remove some insecure default settings and lock down access to your database system. Before running the script you will set a password for the root user, using mysql_native_password as default authentication method.
Your MySQL server is now installed and secured.

Exit the MySQL shell with:

mysql> exit

![image 11](https://github.com/laola234/Darey.io-Projects-/assets/136293714/4bdfa0ff-534a-4edf-83ac-fd6315dabd2f)

Start the interactive script by running:

![image 12](https://github.com/laola234/Darey.io-Projects-/assets/136293714/b50f9c8d-f399-4b79-bdd5-405ecf7ee107)

Once its succcesfully configured, test if you’re able to log in to the MySQL console by typing:

$ sudo mysql -p

![image 14](https://github.com/laola234/Darey.io-Projects-/assets/136293714/7b0df69c-e3f1-442b-ac84-4c8fccaf0cd5)

Exit from the MySQL terminak by typing 

mysql> exit

![image 11](https://github.com/laola234/Darey.io-Projects-/assets/136293714/b14d3065-7328-4669-9c88-1877704bff6d)

You have Apache installed to serve your content and MySQL installed to store and manage your data. PHP is the component of our setup that will process code to display dynamic content to the end user. In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need libapache2-mod-php to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.

To install these 3 packages at once, run:

sudo apt install php libapache2-mod-php php-mysql

![image](https://github.com/laola234/Darey.io-Projects-/assets/136293714/84b41c1a-8ec8-40cc-a13d-0a8973fb8bf5)

Once the installation is finished, you can run the following command to confirm your PHP version:

php -v
![image 16](https://github.com/laola234/Darey.io-Projects-/assets/136293714/f2154048-9c83-406e-9489-85d7ab16700a)

At this point, your LAMP stack is completely installed and fully operational.

Linux (Ubuntu)

Apache HTTP Server

MySQL

PHP


To test your setup with a PHP script, it’s best to set up a proper Apache Virtual Host to hold your website’s files and folders. Virtual host allows you to have multiple websites located on a single machine and users of the websites will not even notice it.

![image 10](https://github.com/laola234/Darey.io-Projects-/assets/136293714/2c7980ba-4d0e-4941-a883-6fe68f6f5cd9)

We will configure our first Virtual Host in the next step.

### CREATING A VIRTUAL HOST FOR YOUR WEBSITE USING APACHE

Apache on Ubuntu 20.04 has one server block enabled by default that is configured to serve documents from the /var/www/html directory.

We will create a new directory called projectlamp inside the /var/www/ directory using ‘mkdir’ command as follows:

sudo mkdir /var/www/projectlamp

![image 17](https://github.com/laola234/Darey.io-Projects-/assets/136293714/d32a7623-7340-4cf0-a39d-061ee764271f)

Next, assign ownership of the directory with your current system user:

sudo chown -R $USER:$USER /var/www/projectlamp

![image 18](https://github.com/laola234/Darey.io-Projects-/assets/136293714/206d60b2-6263-4213-884d-1c0f2a3c60a0)
 
Then, create and open a new configuration file in Apache’s sites-available directory using your preferred command-line editor. Here, we’ll be using vi or vim (They are the same by the way):

sudo vi /etc/apache2/sites-available/projectlamp.conf

![image 19](https://github.com/laola234/Darey.io-Projects-/assets/136293714/1674c74a-2b9d-4d87-85f1-b615cc2b775c)

ou can use the ls command to show the new file in the sites-available directory

sudo ls /etc/apache2/sites-available

![image 20](https://github.com/laola234/Darey.io-Projects-/assets/136293714/ff2faa05-6637-4c2b-a380-82dbfca43969)

With this VirtualHost configuration, we’re telling Apache to serve projectlamp using /var/www/projectlampl as its web root directory. If you would like to test Apache without a domain name, you can remove or comment out the options ServerName and ServerAlias by adding a # character in the beginning of each option’s lines. Adding the # character there will tell the program to skip processing the instructions on those lines.

You can now use a2ensite command to enable the new virtual host:

sudo a2ensite projectlamp

![image 21](https://github.com/laola234/Darey.io-Projects-/assets/136293714/c793828e-b41d-4299-974e-720d7a6ffcb4)

To make sure your configuration file doesn’t contain syntax errors, run:

sudo apache2ctl configtest

![image 22](https://github.com/laola234/Darey.io-Projects-/assets/136293714/28a0bea7-ac25-47e6-88c6-1854d7da7b23)

Finally, reload Apache so these changes take effect:

sudo systemctl reload apache2
![image 23](https://github.com/laola234/Darey.io-Projects-/assets/136293714/f525d950-4a7d-4eb3-af3d-2b7ef539ae8f)

## ENABLE PHP ON THE WEBSITE

With the default DirectoryIndex settings on Apache, a file named index.html will always take precedence over an index.php file. This is useful for setting up maintenance pages in PHP applications, by creating a temporary index.html file containing an informative message to visitors. Because this page will take precedence over the index.php page, it will then become the landing page for the application. Once maintenance is over, the index.html is renamed or removed from the document root, bringing back the regular application page.

In case you want to change this behavior, you’ll need to edit the /etc/apache2/mods-enabled/dir.conf file and change the order in which the index.php file is listed within the DirectoryIndex directive:

sudo vim /etc/apache2/mods-enabled/dir.conf

![image 26](https://github.com/laola234/Darey.io-Projects-/assets/136293714/2d6eba62-53fa-4464-bf59-847244b56f1d)

After saving and closing the file, you will need to reload Apache so the changes take effect:

sudo systemctl reload apache2

![image 24](https://github.com/laola234/Darey.io-Projects-/assets/136293714/75c6e8fa-5730-4505-b866-93a369e1197c)

Finally, we will create a PHP script to test that PHP is correctly installed and configured on your server.

Now that you have a custom location to host your website’s files and folders, we’ll create a PHP test script to confirm that Apache is able to handle and process requests for PHP files.

Create a new file named index.php inside your custom web root folder:

vim /var/www/projectlamp/index.php



This will open a blank file. Add the following text, which is valid PHP code, inside the file

<?php
phpinfo

![image 28](https://github.com/laola234/Darey.io-Projects-/assets/136293714/187376d8-b248-4929-94ad-91e0e98ac8c3)

When you are finished, save and close the file, refresh the page and you will see a page similar to this:

![image 30](https://github.com/laola234/Darey.io-Projects-/assets/136293714/8b8450f4-2769-4435-84b3-353962aa1e50)

After checking the relevant information about your PHP server through that page, it’s best to remove the file you created as it contains sensitive information about your PHP environment -and your Ubuntu server. You can use rm to do so:

sudo rm /var/www/projectlamp/index.php
![image 31](https://github.com/laola234/Darey.io-Projects-/assets/136293714/372a33fe-4aa4-463e-be0c-2a17da4c8c4e)













