
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

