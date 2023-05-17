This will be a complete CICD Devops projects

During this project (Java Application), we will use:
- **Visual studio code** to write our configuration, manifest file,
- **Github** as a repository for the code
- **Jenkins shared Librairies** help us to make our Jenkins reusable. Instead of doing the samr=e thing many times, we can centralize everything in this Librairies
- **Jenkins** will run Maven. When the code is in the Github repository, Jenkins through the webhook, started doing unit testing and integration testing on our Java code application;
- **Sonarqube** After that, Sonarqube will do the Static code analysis to see if you pass or failed the quality Gate status;
- **Maven** will be compiling our application to have an artifact
- **Docker** to create our image and run our container. Before pushing this image to the ECR, we scan the docker image 
- **ECR** to store the docker image
- Our CI is done. Now we can deploy our application on k8s.


## Create Jenkins Server
Go on the EC2 instances and launch the instances :
- Choose ubuntu 22,
- Create a key pair
- take a t2.medium 
- Modify the security group: open the port 8080 for Jenkins and 9000 for Sonarqube
- Go to advanced details and paste all the command related to the installation of Jenkins and docker. We will also install Sonarqube as a Container. 
- Click on launch instances and our EC2 is successfully created































