## 1.WEB STACK IMPLEMENTATION (LEMP STACK)
*What is LEMP Stack:* LEMP stack refers to a development framework for Web and mobile applications based on four open source components: Linux operating system. NGINX Web server. MySQL relational database management system (RDBMS) PHP, Perl, or Python programming language.


In this project we will implement a stack using *NGINX*

*Tools to be used:*
1. AWS Account 
2. Git Bash here we'll install NGINX, NySql and PHP.

AWS => First we create an instance on our AWS account then using our private .pem key we run the following command on Git Bash which will look like this  ![reference image ](/Pictures/pic1.PNG)

Next we update our server's package index then install NGINX WEb Server using the following command ![reference image](/Pictures/pic2.PNG) and ![reference image](/Pictures/pic3.PNG) when promted enter Y to confirm you want to install NGINX and also running on Ubuntu
Verify NGINX was successfully installed and is running as a service in Ubuntu, if it's like this => ![reference image](/Pictures/pic4.PNG) then you just launched your first web server in the clouds.
add a rule to your instance security group, the  inbound rule connection to allow all traffic connections through port 80: ![reference image](/Pictures/pic19.PNG)
then access your localhost in the Ubuntu shell using the curl command $curl http://localhost:80 and test to see if your Nginx server can respond to request from the internet using any web browser of your choice  and  you should see this ![reference image](/Pictures/pic5.PNG)

Now we install mysql ![reference image](/Pictures/pic6.PNG) and log into the mysql console
Now run a security script that comes pre-installed with mysql which will remove some insecure default settings and lock down access to your database system. using mysql_native_password as default authentication method use password as Password.1 withe the following command ; ALTERUSER'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'Password.1';
Then exit mysql 
Then start the interactive scriptlike this ![reference image](/Pictures/pic7.PNG) answer yes to all the prompted questions ![reference image](/Pictures/pic8.PNG) then enter 1 for the medium password 
When you're done test if you're able to log into the mysql console as previously shown the input the password you previously created after you successfully log then you can exit ![reference image](/Pictures/pic9.PNG)
Next we Install PHP using this command: $sudo apt install php-fpm php-mysql when promted with *y* press *enter* to confirm installation.
## 2.CONFIGURING Nginx TO USE PHP PROCESSOR
When using the Nginx web server, we can can create server blocks similar to virtual hosts in apache to encapsulate configuration details and host more than one domain on a single server. Here we will ise projectLEMP as an example domain name.
create the root web directory for your_domain using the floowing commands then assign ownwership to the directory with the $USER environment variable then open a new configuration file in Nginx's *sites-available* directory using any CLI editor I used *nano* though ![reference image](/Pictures/pic10.PNG) then input the following configuration ![reference image](/Pictures/pic12.PNG)
1. listen - defines what port will listen on
2. root - defines the document root where the files served by this website are stored
3. index - defines in which order Nginx will prioritize files for this websites 
4. server_name - defines which domain names or IP addresses this server block should respond to
5. location/ - checks for the existence of files or directories matching a URL request
6. location ~ \.php$ - This location block handles the actual PHP processing by pointing Nginx to the fastcgi-php.
7. location ~/\.ht - The last location blocks deals with *.htaccess* files, which Nginx does not process
Activate the configuration by linking to the config file from Nginx's *sites-enabled* using: $sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
this will tell Nginx to use the configuration next time it is reloaded then test your configuration for syntax errors then disable default Nginx host that is currently configure to listen on port 80 then finally reload Nginx to apply changes you'll see this  ![reference image](/Pictures/pic13.PNG) 
Now go to your browser and access your IP address
The next step is to test PHP with Nginx because at this point your LEMP Stack is completely installed and fully running 
Next is to create a PHP file in your document root open a new file called *info.php* your document root in you text editor types the following lines:
1. <?php
2. phpinfo();
YOu can now access your web browser by visiting the domain name or public IP address, after checking relevevant information about your PHP server through that page it's best to remove the file you created as it contains sensitive information about your PHP environment and your Ubuntu server. if you follow the above procedure you should see this ![reference image](/Pictures/pic14.PNG) and this ![reference image](/Pictures/pic15.PNG) 

## 3. Retrieving data from MySQL database with PHP
Here you will create a test database (DB) with simple "To do list" and configure access to it, so the Nginx website would be able to query data from the DB and display it.
1. First we create a database named *example_databse* and user named *example_user* but you can replace the names with diffrent values. Connect to the MySQL console using the root account: $sudo mysql then cretae a database using the following command ![reference image](/Pictures/pic16.PNG)
2. Now we create a test table named todo_list. from MySQL console ![reference image](/Pictures/pic17.PNG)
3. Use the Nano editor to write the following script using this command $ nano /var/www/projectLEMP/todo_list.php ![reference image](/Pictures/pic18.PNG) save and close when you done editing
4. access your page using your browser by visiting the domain name or IP address configured on your website and you'll see this ![reference image](/Pictures/pic19.PNG)
5. Which means you PHP environment is ready to connect and interact with your MySQL server.
### AND THIS HAS COME TO THE END OF OUR LESSON I HOPE YOU ENJOYED THE RIDE 


