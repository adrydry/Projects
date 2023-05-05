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


**Step1: Launch our EC2 instances**
We will lunch an Ubuntu Ec2 called **Ultimate-cicd** . Because this server will support many heavy tools, we will launch an ubuntu EC2 with a t2.large capacity

![1](https://user-images.githubusercontent.com/102819001/236523967-ca00e5ad-0e69-46b5-b5ce-34ef04887b8d.png)


