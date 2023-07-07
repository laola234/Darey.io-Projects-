
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

Your MySQL server is now installed and secured.

### INSTALLING PHP

PHP is the component of our setup that will process code to display dynamic content to the end user. In addition to the php package, you’ll need php-mysql, a PHP module that allows PHP to communicate with MySQL-based databases. You’ll also need libapache2-mod-php to enable Apache to handle PHP files. Core PHP packages will automatically be installed as dependencies.

To install these 3 packages at once, run:

sudo apt install php libapache2-mod-php php-mysql

![image](https://github.com/laola234/Darey.io-Projects-/assets/136293714/84b41c1a-8ec8-40cc-a13d-0a8973fb8bf5)

Once the installation is finished, you can run the following command to confirm your PHP version:

php -v

![image 9](https://github.com/laola234/Darey.io-Projects-/assets/136293714/19ed306f-3609-48a3-aef3-134fa9ddd21a)

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

We will create a new directory called projectdock inside the /var/www/ directory using ‘mkdir’ command as follows:

sudo mkdir /var/www/projectdock

Next, assign ownership of the directory with your current system user:

sudo chown -R $USER:$USER /var/www/projectdock

 
