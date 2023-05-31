
A **technology Stack** is a set of frameworks and tools used to develop a software product.This set of frameworks and tools are very specifically chosen to work together in creating a weel-functioning software. We have many technologies as:
- **LAMP** - Linux Apache, MySQL, PHP or Python, or Perl
- **LEMP** - Linux, Nginx, MySQL, Php, Perl
- **MERN** - MongoDB, ExpressJS, ReactJS, NodeJS
- **MEAN** - Mongodb, ExpressJS, AngularJS, NodeJS
Web stack implementation refers to the process of setting up and configuring the various technologies and components that form the foundation of a web application or website. It involves selecting and integrating the different layers of software and infrastructure required to deliver a functional and performant web application. 

Web stack implementation involves installing and configuring the necessary software components, setting up the database, configuring web servers, and writing code using the selected web application framework and programming language. It also involves optimizing the performance, security, and scalability of the web application, as well as testing and debugging to ensure its proper functionality.


In this project, we will implement the **LAMP** on AWS

**Spin an EC2 instance on Ubuntu**

 - Create first the Security Group of our instance. Make sure to open the port 22 for ssh and 80 for http
 
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/3b20baa1-aabb-4475-bcc4-910a2cb2c064)

Our EC2 is up and running on ubuntu

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/6c54561c-5f90-49da-aa10-d49cbf54a5ed)

**Connect the new instance with our server**

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/3ccf4423-fafe-4904-81bf-d7f3f12da4d2)

Now, we have create our EC2 instance on Ubuntu, let's install Apache

**Install Apache**

**Apache** is one of the best web server application which allow us to make our application accessible trough internet. To install and verify that Apache2 is installed, we use the commands below:
- Update a list of packages in package manager : sudo apt update
- Run apache2 package installation: sudo apt install apache2
- Verify Apache2 installation: sudo systemctl status apache2

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/07648063-b529-4357-ba88-55b19cde30b2)

Now, our server is running and we can access it locally and from the internet.
To check if it is accessible locally on our ubuntu shell: curl http://localhost:80. Our webpage is up and running

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/dc995f65-570a-4779-b804-c28d60295413)

To check if our server is running on internet: http://PublicIP adress:80. Our server is available on the internet

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/4f12b7d6-c374-4ecd-a31d-fa3a5da05acb)

**Troubleshoot**: Incase the server is not accessible on internet, check the security group of the EC2 instance, to mahe sure that the port 80 is open.


**Install mysql**
From our ubuntu terminal, we cannot perform directly actions related to the database. We need first to install the Mysql console with the command:**sudo apt install mysql-server**. After the installation to connect to the console, we use: **sudo mysql**

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/c129d44d-fb8b-46a8-8ede-efa2dae95fd0)

It's recommended to run a security script that comes pre-installed with Mysql. Before running the srcipt, we will set a password for the root user

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/867d8543-e575-49b0-bded-342c543b0368)

- Start the interactive script by running: sudo mysql_secure_installation. The system will ask for the password for the root user. we just have to use the password we have used in the step before

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/bd49a5b3-0feb-4b6d-a62e-a03c4fd6447d)

Our SQL installation is now secure
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/d7bf0808-04ea-4b02-b604-623d8dd82cb7)


**Install PHP**


