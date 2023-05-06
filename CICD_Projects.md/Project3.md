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

**Connect to the server using gitbash and clone the repository where the Source code is located**

![1](https://user-images.githubusercontent.com/102819001/236577381-cc206cc5-78c9-4a80-9645-20d2c5b128e1.png)

**Install Jenkins**
Go to the directory where the source code is located

![1](https://user-images.githubusercontent.com/102819001/236578192-32d3f236-8e95-4a5f-ad94-dd24b2b6e35d.png)
  
  - Go on Jenkins.io.com and copy te differents commands to install jenkins
  
  To verify is jenkins is install, go on the browser and open the localhost with the port 8080. We noticed that it's not possible to reach the jenkins page. We need to verify our inbound traffic on our server to ensure that 8080 is open
  ![2](https://user-images.githubusercontent.com/102819001/236587065-ef12bb6a-ac4d-4276-ba60-2087babd0720.png)
  
- Check the status of jenkins

   ![1](https://user-images.githubusercontent.com/102819001/236587209-514585d1-c4d0-461c-b9a4-ac05d3895a06.png)

now jenkins is accessible on the browser
![2](https://user-images.githubusercontent.com/102819001/236587275-49f2d0a6-58aa-44bc-8120-b1b2e3fe95d9.png)
  
  - Generate the token to access jenkins

![1](https://user-images.githubusercontent.com/102819001/236589148-50d95e64-b383-4408-b431-d8902919ef40.png)

 - Installed the different plugins and jenkins is ready
 
 ![1](https://user-images.githubusercontent.com/102819001/236589355-b610043a-2d57-49b7-9865-f537195b450d.png)

 **Deploy our pipelines**
 - Set up the jenkins pipeline   
 In Jenkins, select new item and click on pipeline. This will facilitate collaboration with the other members of the team
 
 ![1](https://user-images.githubusercontent.com/102819001/236589776-5a0c827a-89fb-4102-9aea-ff83d364c2eb.png)

 To write 2 codes in jenkins, we have 2 differents ways: in the groovy sandbox or Jenkins allows to put directly the jenkins file in the repository where the code source is located. Like this, for any microservices of our application, we can find the code and the jenkins file at the same place
 
 On jenkins, Clck on Advanced projects options, define the pipeline as Pipeline Script for SCM. Paste the git repository Url, specify the branch and add the script path (inside the repository where the jenkins file is located) and save. The jenkins file can be in any location and can be name differently of Jenkinsfile
 
 - Install **Docker pipelines plugins** which contains already Maven
 
 ![1](https://user-images.githubusercontent.com/102819001/236591214-1c9b9cbd-6fbb-4449-899e-bf26d9647146.png)

 - Install Sonarqube
 Install sonarqube plugins on my jenkins pipelines (**sonarqube scanner**)
  
 ![1](https://user-images.githubusercontent.com/102819001/236591437-865d63c9-b754-42fe-b718-11a30b66f735.png)

we have ton install Sonarqube server on my EC2 instance
- Create the user adduser sonarqube
![1](https://user-images.githubusercontent.com/102819001/236591727-be4b9a24-f8c5-4a5f-a4ef-791c34de0891.png)

- Switch to sonarqube user: sudo su - sonarqube and download sonarqube binaries

 ![1](https://user-images.githubusercontent.com/102819001/236592836-2bf17592-d3a5-4e0e-9a75-bc39c256ae16.png)

 - unzip the folder with **unzip**. 
 
 ![1](https://user-images.githubusercontent.com/102819001/236593104-02215e5f-f74b-4689-8607-de5aa08df183.png)
 
![1](https://user-images.githubusercontent.com/102819001/236593723-bf77ec95-7a7d-425f-a520-72d6826f6262.png)

 - Start sonarqube
 ![1](https://user-images.githubusercontent.com/102819001/236593825-8f6973c9-0279-4375-ac40-d997b6685634.png)
 
 Sonarqube by default run on 9000 and his default username and password is **admin**. 
![2](https://user-images.githubusercontent.com/102819001/236593831-bed5dd1a-c0b8-430a-b796-ec3bc03bef68.png)

At the first connection, Sonarqube will require a new password

 ![2](https://user-images.githubusercontent.com/102819001/236594018-7655f213-e7a1-4bc0-bd85-efe4a7d7e7fe.png)

 
 - create our minikube and start it
 
 **Instal kubernetes controller**
 Everytime, you want to install any kubernetes controller, the first thing to do is to install the k8s operator. The operator will manage the lifecycle of the k8s controller. so, incase of any update of the controller version, telemetrics,...we will still uptodate. Also, the operator makes the installation process very easy.
 
 - Install k8s via the operator. Go on operatorhub.io.com . Search Argocd and copy the command for installation
 
 ![1](https://user-images.githubusercontent.com/102819001/236598394-f76d1af2-11de-47b1-8a21-a82b5f562a21.png)









