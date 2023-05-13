## IMPLEMENT A CI/CD END TO END WITH JENKINS

In this project, we will create a Spring Boot application based on Java technologies. We will use many tools: Jenkins, Docker, Sonarqube, Argocd.

We have 2 repositories for our project

**Repository1**: our jenkins pipeline is just use for the continuous integration and stopped when the image is pushed in the docker repository. In this phase, we will make sure the build is smooth, all the tests code are executed, your code quality is maintained,our image is created and save it in the Dockerhub

**Repository2**: is for the continuous delivery that ensure that your deployment is done. we will use k8s. When the CI is done, the CD can take place.

**Presentation of the workflow of the project**:

- We create the Git repository,
- When developpers finished to write the code, they save the code in the github repository
- Whenever a pull request is created, Jenkins pipelines has to be triggered. A **pull request** is a mechanism which helps developpers to notify the other members/developpers that a new feature is completed. They can go and review it
When a developper commit a change in the git repository, Jenkins will be automatically notify by using **Webhooks**. Like this, Jenkins don't need to look to your repository but git repository will inform directly Jenkins incase of a new commit.
To install webhook, we just need to have the url of jenkins and paste in Github Settings. We have the ability to describe for which actions, webhooks need to be triggered jenkins (on commit, on Pull request, on issue,...)
- So Jenkins will triggered the pipelines and the Devops engineer has to write the jenkins file, using **the declarative syntax** because it's easy to write, to collaborate with other even if they dont have knowledge about coding. This Jenkins file will help to perform some actions on the jenkins pipelines like: Build the application using Maven or docker agent, after building, you have to execute some tests: Unit tests,
- we will do some Static Code Analysis to ensure that the application is not exposed to any static code;
- verify application security to ensure that the new changes of the developpers is not an open door of vulnerabilities of the application with tools like SAST, DAST.  Sonarqube will be integrated for security scanning tools. It will help us to verify what happen in our previuos stage (Sonarque will help you to check if the code is matching with the compliance of the organizations, does it has error less than x%, are there any security vulnerabilities for the code,...)
Incase of any failure of one of this test, we will send notifications to developpers using email notifications in Jenkins, also slack or aws email notifications.If these tests are successful, we will move to the next stage. 
- Create our docker image by using docker agent or create a docker plugins or write a shellscript or docker build
- Push this docker image in a docker registry or ECR. **That's is the end of our continuous integration**
 **Beginning of the Continuous delivery** To enable communication between CI & CD, we use **Ansible playbooks or shellscripting webhook** to deploy the artifact on k8s. But these tools are not scalable. 
- For our project, we will use the best continuous delivery tools in the market **Gitops** With this tool, we will create a git repository and save our application manifest inside (k8s pod yaml file). Instead on going directly on k8s and create this file, using Gitops give the possibility to verify the yaml file, to review the code before deployment, like an audit for the code and the application manifest.
- So for the Yaml files to be updated with the new image created in the CI, we can use **Argo image updater**. This tool will continuosly monitor the dockerhub or the container registry. And whenever a new image is updated in your registry, Argo image updater will directly update the git repository where the yaml file is located with the new image
- ArgoCD is constinuosly watching the Git repository where the yaml file is located and whenerver there is a change in this repository, they upload the pod/deploy/service/helmchart yaml and deploy in the k8s cluster. Argocd and Argo image updater are already deploy **inside the k8s cluster** 

## DEPLOY OUR PROJECT

**Launch our EC2 instances**
We will lunch an Ubuntu Ec2 called **Ultimate-cicd** . Because this server will support many heavy tools, we will launch an ubuntu EC2 with a t2.large capacity

![1](https://user-images.githubusercontent.com/102819001/236523967-ca00e5ad-0e69-46b5-b5ce-34ef04887b8d.png)

**Install Java as a prerequisite for Jenkins**
sudo apt update
sudo apt install openjdk-11-jre
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/1ea94ad3-78ea-4fe4-ad3f-7841280d76ab)

**Install Jenkins**
- Go on jenkins.io and select Linux. These are the commands to use to install jenkins on our ubuntu server
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/74c1a676-0784-4d14-a2dc-cd490ea9b8dc)

- To verify Jenkins installation, take the public Ip adress of our instance and open it on port 8080. We noticed that the jenkins page is not accessible 

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/4e1505aa-6c9a-4afa-b905-f57bfcbaea22)

- We need to verify our security group. To ensure that the Inbound traffic on port 8080 is open

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/c701e45c-0d35-440a-a6df-66ba42fa9e30)
  
- Check the status of jenkins

   ![1](https://user-images.githubusercontent.com/102819001/236587209-514585d1-c4d0-461c-b9a4-ac05d3895a06.png)

now jenkins is accessible on the browser
![2](https://user-images.githubusercontent.com/102819001/236587275-49f2d0a6-58aa-44bc-8120-b1b2e3fe95d9.png)
  
  - Generate the token to access jenkins

![1](https://user-images.githubusercontent.com/102819001/236589148-50d95e64-b383-4408-b431-d8902919ef40.png)

 - Installed the different plugins and jenkins is ready
 
 ![1](https://user-images.githubusercontent.com/102819001/236589355-b610043a-2d57-49b7-9865-f537195b450d.png)

 **First thind to do: Write our pipelines**
 - **Set up the jenkins pipeline**   
 In Jenkins, select new item and click on pipeline. This will facilitate collaboration with other members of the team. To write your codes in jenkins, we have 2 differents ways: use the groovy sandbox or paste directly the url of your github repository where the code source is located. Like this, for any microservices of our application, we can find the code and the jenkins file at the same place. Clck on Advanced projects options, define the pipeline as Pipeline Script for SCM. Paste the git repository Url, specify the branch and add the script path (inside the repository where the jenkins file is located) and save. The jenkins file can be in any location and can be name differently of Jenkinsfile

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/89749544-08f8-4abe-9ef9-4e516a2bbbe5)

Now, Jenkins understand where is the jenkinsfile. This integration of the jenkinsfile will help us to integrate all the task of the Continuous integration 
The best way to write a Jenkinsfile is to use Docker as a **agent**. Like this your pipeline will create automatically a container, and whenever a container is created, the configuration will be created and the container will be deleted after the configuration of a deployment. This will help the company to not be charged by AWS. So as soon as, your pipelines is trigger, your pipeline take the responsability to create a docker container, the pipeline will execute all the stages of the jenkins file inside the docker container and when the jenkins file is executed, the docker container is deleted at the end. Like this your ressources are free for other jenkins jobs.
To choose Docker as a agent, inside your pipeline, we need to use Docker plugins and select a compatible image to write your Dockerfile. This is a responsability of a Devops engineer.

- How to write a jenkins pipelines

Jenkinsfile is composed of many stages. Theses stages represents the blocks of what you try to build. Any step of our project is a block. so we need one stage for every block. So, in our case:
Block 1: The checkout stage. Jenkins will checkout because the jenkins file is located also in the git hub repository. we also need checkout for the webhook

Block 2: Build and test my artifact. This stage will help us to clean and package. The difference between mvn clean package and mvn install : the mvn clean package will find the pom.xl file (list all the dependencies of your application)

Block 3: when your artifact fets generated, a new folder target is created and inside this folder the artifact is located. this step help you to tell to jenkins where is the url of your sonarqube. without this url, jenkins will not be able to send the information to sonarqube server

Block 4: define the credentials to integrate sonarqube url as a credentials in jenkins. the package to execute sonar is mvnsonar:sonar. for this stae, we need, the sonarqube url and the sonarqube token

Block 5: define the docker build and push step. Define the docker credentials to help you push the docker image in the dockerhub

Block 6: update the repository. write a shellscript using the github and docker credential

 - Install **Docker pipelines plugins** which contains already Maven
 
 ![1](https://user-images.githubusercontent.com/102819001/236591214-1c9b9cbd-6fbb-4449-899e-bf26d9647146.png)


 **Install Sonarqube inside my jenkins pipelines**

Go to availaible plugins and install **sonarqube scanner**
  
 ![1](https://user-images.githubusercontent.com/102819001/236591437-865d63c9-b754-42fe-b718-11a30b66f735.png)

**Install Sonarqube server on my EC2 instance**
Sonarqube will be placed in the same VPC used by the EC2 instances. During this installation, we will using the Public ip adress of the instance but in our company, its recommaneded to use the private instance

- Create the user adduser sonarqube and Switch to sonarqube user: sudo su - sonarqube and download sonarqube binaries
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/1275fe32-ff27-4b53-851a-c59ab10181b2)

 - Download the sonarqube binaries
 ![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/57935f47-7b61-46af-b8c4-0313582a0986)

 - Return as a root user, install **apt install unzip** and unzip the folder with **unzip**. 
 ![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/81316dfc-0f78-48eb-8f34-d0f08a8a4080)

 - Give new permissions to the unzip file
 chmod -R 755 /home/sonarqube/sonarqube-9.4.0.54424
 chown -R sonarqube:sonarqube /home/sonarqube/sonarqube-9.4.0.54424
 
 - Start sonarqube
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/d39f3785-7dcb-4152-8ad1-a956fbede215)

- Verify is Sonarqube is running
 Sonarqube by default run on 9000. Take the public IPA of our instances and open on the browser. We will notice that the page is not accessible. We have to check our security group and open the port 9000. Now, it's work
 ![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/9eb78e5e-6fc3-4aaa-8510-24c5c9598106)

 - Access the Sonarqube platform
 By default, the default username and password of Sonarqube is **admin**. 
![2](https://user-images.githubusercontent.com/102819001/236593831-bed5dd1a-c0b8-430a-b796-ec3bc03bef68.png)

At the first connection, Sonarqube will require a new password

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/86526044-3363-4cdf-a75f-366bb45e3562)

- After logging, the system will ask you where you want to deploy your project
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/be8912b1-55ba-443e-95d3-3af50ea3f3ec)

Jenkins is integrate with Docker. Now that Sonarqube is installed, how can it communicate with Jenkins (there are 2 differents applications???

**Integrate Jenkins with Sonarqube**

- Go to Sonarqube, click on My account, Click on Security, and generate a oken for Jenkins
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/65f5a370-a122-4a14-a353-edcdb5920e3e)

- Copy this token, Go to Jenkins, Manage credentials and paste it

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/814cb95e-dd7b-446f-a0ee-e83b50ea563d)

So now, my configuration of Sonarqube in Jenkins is done

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/b5744868-8a73-4151-9a20-4460b1eca802)
 
 
 **Do the differents tests with Selenium,...**
 
 **Install Docker on my ec2 instances** using the command **sudo apt install docker.io**

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/37d66462-7e27-4435-a529-a2672dbbdf40)

- Give permissions to jenkins and ubuntu to use docker and restart docker. 
sudo su - 
usermod -aG docker jenkins
usermod -aG docker ubuntu
systemctl restart docker

Write the differents credentials of docker (Id as docker-cred as define in the jenkinsfile, put your dockerhub username and password)and Github (choose secret text, go to the github, choose settings, developper settings and click on personal access tokens, click on token classic and generate a new token)in jenkins
**Restart our Jenkins server**
After installing all these plugins, it's a best practice to restart the jenkins server. 
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/2aa9c312-1d74-4e03-b562-80055a63bf46)

**Create our Minikube**

Minikube is a tool that lets you run k8s locally. It runs a single -node k8s cluster on your personal computer so that you can try k8s for daily work


 - create our minikube and start it
 
 **Instal kubernetes controller using operator**
 Everytime, you want to install any kubernetes controller, the first thing to do is to install the k8s operator. The operator will manage the lifecycle of the k8s controller. so, incase of any update of the controller version, telemetrics of the controller,...we will still up to date. Also, the operator makes the installation process very easy.
 
 - Install k8s via the operator. Go on operatorhub.io.com . Search Argocd, click on install and copy the command for installation
 
 ![1](https://user-images.githubusercontent.com/102819001/236598394-f76d1af2-11de-47b1-8a21-a82b5f562a21.png)

- Verify the installation of the k8s operator using **kubectl get pods -n operators -w**

**Build our jenkins pipelines**
our application pass the different stages 

**Use argocd to deploy our application in k8s
- go to argocd operator documentation - basics. copy the command. 
- create and open a new yaml file and paste the argocd operator
- kubectl apply -f argocd-basic.yml
- kubectl get pods
- kubectl get svc
- kubectl edit svc example-argocd-server
- minikube service argocd-server
- minikube service list: minikube give you an url that will help you to access your application
- kubectl get pods. All the pods are up and running
- copy the link and put in a browser. Argocd is running and we just need to provide the username and password. the username is Admin and fpr the password, go to kubectl get secret and kubectl get secret cluster name. copy the admin password
- echo password | base 64 -d. copy the password and copy on the argocd page
- Open the argocd page and click on create an application
-  







