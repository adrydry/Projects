## PROJECT : DEPLOY A CLOUD NATIVE MONITORING APPLICATION ON KUBERNETES

In this project, we will learn How to build an application and deploy it on kubernetes. For achieve this we will use many tools like:
- Create a monitoring application in python using Splunk
- Containerize the application with Docker: Create the Dockerfile, build the image and run the container locally
- create a container registry with Amazon ECR using Python, boto3 modules
- Move to the deployement phase where we will create an Elastic cluster with Amazon EKS,
- Deploy our application on k8s. We will create deployment service using python so that our application can be accessed from the internet


## PREREQUISITES

- Avoid problematic access by creating an Administrator user or any other user different from the user of the company and create his Access key and Secret Keys. Save the credentials files.
These credentials will help you to take control of your console through the AWS CLI

- Open the terminal through VSC and use **aws configure**. The system will ask for your credentials.
![1](https://user-images.githubusercontent.com/102819001/234981183-b69bdb44-0ebf-4d82-a584-8957041627ca.png)

- Use **aws iam list-users** to verify if you are connected 
![2](https://user-images.githubusercontent.com/102819001/234981215-5f2f5784-bc67-4cc7-89e9-b59d21d0a32b.png)

- Verify if Python is already installed in our computer by using in the terminal **python --version**
![1](https://user-images.githubusercontent.com/102819001/234983723-5b8c6bba-6f80-46ec-81b5-f9ac6182a9e4.png)

- Verify if Docker is installed by using **docker --version**

![1](https://user-images.githubusercontent.com/102819001/234984041-7650f9a1-a7b3-4828-83e7-da10c91eef78.png)
 
- Verify is Kubectl is installed by using **kubectl version**
![1](https://user-images.githubusercontent.com/102819001/234985996-79da255a-caaf-4534-a3ee-48f0f2dd0756.png)
 
 Now that, we have everything installed, Let's go to our project
 
 ## STEP1: BUILD OUR APPLICATION
 Go in my home directory and create a new folder
 
  
