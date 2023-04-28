## PROJECT : DEPLOY A CLOUD NATIVE MONITORING APPLICATION ON KUBERNETES

In this project, we will learn How to build an application and deploy it on kubernetes. For achieve this we will use many tools like:
- Create a monitoring application in python using flask
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
 
 ## STEP 1: BUILD OUR APPLICATION
- Go in my home directory and create a new folder Cloud-native-monitoring. Open this folder through VSC. Create a file app.py where the code of our application will be located
![1](https://user-images.githubusercontent.com/102819001/235011552-92d0789b-62a9-4353-966b-f6e41739b37d.png)

 - Write the code for my application with python and the requirements.txt file that contains all the dependencies. 
  ![1](https://user-images.githubusercontent.com/102819001/234998206-8fb35304-b5f7-48a2-924a-768632628914.png)

- Install all the dependencies by using **pip install -r requirements*

![1](https://user-images.githubusercontent.com/102819001/235011978-bb483e99-e202-451d-80d5-d4d5dae5848f.png)

![1](https://user-images.githubusercontent.com/102819001/235012129-2eca8ff1-4325-4df7-b060-344aa88b2905.png)

- Run the application by using by using **py app.py**

![1](https://user-images.githubusercontent.com/102819001/235012387-1790b352-a683-46d0-8cf1-9c7ee24b40cd.png)

We can now access our application from the browser **localhost:5000**.

![1](https://user-images.githubusercontent.com/102819001/235012816-1cb9bb6b-c7ac-4b8b-808e-e1c5c3c0239a.png)

## DOCKERIZE OUR APPLICATION AS A CONTAINER
- We need to define our Dockerfile. For that Go to docker.com and find an image for Python

![1](https://user-images.githubusercontent.com/102819001/235013874-6fd981a1-9419-47bd-acc7-a8c5c5cfa45e.png)
 Select the official image of python
 
 ![2](https://user-images.githubusercontent.com/102819001/235013930-23022bcc-7d00-4fed-9e47-5b7901c6191a.png)

 This is our Dockerfile
 ![1](https://user-images.githubusercontent.com/102819001/235014664-28d8788a-d184-48a9-8cb0-fccf899482eb.png)
 
- Build an image from this Dockerfile by using **docker build -t my-flask-app .**
![1](https://user-images.githubusercontent.com/102819001/235016094-efc21f8f-c8be-4ec0-8b0b-cd348fda0343.png)

- To verify that the images is created, use **docker images**

 ![1](https://user-images.githubusercontent.com/102819001/235016235-1fc5fb95-4ccb-4320-8dce-94a7b312f7c1.png)

-Now , we can create our container


 
 
 
 
 
 
 
 
 
 
 
 
 
