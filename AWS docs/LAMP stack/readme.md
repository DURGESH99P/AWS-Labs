# LAMP stack
LAMP stack stands for Linux, Apache Web Server, MariaDB/MySQL and PHP. It is a popular open-source web platform that can be used to host dynamic websites and web applications on an Amazon Web Services (AWS) EC2 instance running Amazon Linux 2. The page provides detailed instructions on how to set up a LAMP stack on an AWS EC2 instance.

For the AWS documentation, refer to the below link

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html

*******************************************************************************************************************

LAMP stack stands for
L = Linux (i.e Linux instance on which the server is going to host )
A = Apache Web Server (on this server we are going to host our website)
M = Mariadb / MySQL (Database needed for the storing the user/website data)
P = PHP (for the connection between the database and Webpage)


## Steps for Implementation of LAMP Stack

### Step 1.

Create a simple Linux instance in EC2 service.
(things to take care of
    A. download the ppk file of Key-pair, if pem file is downloaded then convert it in ppk using
puttyGen.
    B. add the HTTP inbound rule from `0.0.0.0/0`)
![instances](https://github.com/hrishikesh26/Projects/assets/94166344/23d8eed9-7336-4aba-98a7-c077bb4226a1)

### Step 2.

Connect the Linux instance using putty
![putty terminal](https://github.com/hrishikesh26/Projects/assets/94166344/64ff5e1f-018e-4734-9197-973eacafacd0)


### Step 3.

Follow bellow commands to update / download the required applications in Instance.
-> `sudo yum update -y`  (for update the sysytem) 

-> `sudo amazon-linux-extras install -y lamp-mariadb10.2-php7.2 php7.2`  (Amazon Linux Extras repositories to get the latest versions of the LAMP MariaDB and PHP packages for Amazon Linux 2.)

-> `sudo yum install -y httpd mariadb-server`  (installing the httpd i.e apache server)

-> `sudo systemctl start httpd`  (Start the Apache web server)

-> `sudo systemctl enable httpd`  (to enable the server)

-> `sudo systemctl is-enabled httpd`  (check the status enable or not)

![termial with code](https://github.com/hrishikesh26/Projects/assets/94166344/d09d2077-da13-4cb5-87fa-21db7270a4f9)

Now, Once done with this, check whether the apache test page is visible by pasting the ipv4 address
of your instance to the web browser.

![apache test page](https://github.com/hrishikesh26/Projects/assets/94166344/cc828f5e-efe2-476f-ba46-b7b87843ebe7)

### Step 4.

As the default test page is visible. So in future if EC2 user or any other user whats to add, delete, and edit files in the Apache document root, enabling you to add content, such as a static website or a PHP
application.

Then follow the bellow steps. 

-> `sudo usermod -a -G apache ec2-user`

-> `exit`

-> `groups`

-> `sudo chown -R ec2-user:apache /var/www`

-> `sudo chmod 2775 /var/www && find /var/www -type d -exec sudo chmod 2775 {} \;`

-> `find /var/www -type f -exec sudo chmod 0664 {} \;`

### Step 5. 

Test your LAMP server.

For that

a. Create a PHP file in the Apache document root.

-> `echo "<?php phpinfo(); ?>" > /var/www/html/phpinfo.php`

b. In a web browser, type the URL of the file that you just created
Eg. `18.215.16.33/phpinfo.php`

![php webpages](https://github.com/hrishikesh26/Projects/assets/94166344/a6aebc22-4410-4643-abef-fcb1a487c102)

c. Delete the phpinfo.php file. Although this can be useful information, it should not be
broadcast to the internet for security reasons.

-> `rm /var/www/html/phpinfo.php`

### Step 6.

Secure the database server.

-> `sudo systemctl start mariadb`
(Start the MariaDB server.)

-> `sudo mysql_secure_installation`
(Run mysql_secure_installation.
After this command You need to enter as there no any already existing password is there
And need to assing a new password, and need to select yes for all the suggestion.)


### Step 7.
Installl phpMyadmin.

-> `sudo yum install php-mbstring php-xml -y`

-> `sudo systemctl restart httpd`

-> `sudo systemctl restart php-fpm`

-> `cd /var/www/html`

-> `wget https://www.phpmyadmin.net/downloads/phpMyAdmin-latest-all-languages.tar.gz`

-> `mkdir phpMyAdmin && tar -xvzf phpMyAdmin-latest-all-languages.tar.gz -C phpMyAdmin
--strip-components 1`

-> `rm phpMyAdmin-latest-all-languages.tar.gz`

-> `sudo systemctl start mariadb`

After this In a web browser, type the URL of your phpMyAdmin installation.
I.e `18.215.16.33/phpMyAdmin`

![php login](https://github.com/hrishikesh26/Projects/assets/94166344/aee4dc4a-03f5-40b3-a84e-1435a4c986ea)


Now you need to select **Username** as **root** and **password** that you saved in **step 6**.

![php login root](https://github.com/hrishikesh26/Projects/assets/94166344/8b19f526-69f1-47e0-8ea4-507e641cec4e)


And after this
You will successfully loging into your database.

![phpmyadmin webpage](https://github.com/hrishikesh26/Projects/assets/94166344/988f2eb7-d168-44e1-99f9-ad5bdd408254)









    
