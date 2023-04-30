## PROJECT : DEPLOY A CLOUD NATIVE MONITORING APPLICATION ON KUBERNETES

In this project, we will learn How to build an application and deploy it on kubernetes. For achieve this we will use many tools like:
- Create a monitoring application in python using flask
- Containerize the application with Docker: Create the Dockerfile, build the image and run the container locally
- create a container registry with Amazon ECR using Python, or boto3 modules
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

-Now , we can create our container by using **docker run -p 5000:5000 imageid

 ![1](https://user-images.githubusercontent.com/102819001/235048801-f1b3a3f9-5a15-4893-ae5a-efaa5e65e9d7.png)

Now, our application is running inside the docker container. we can check on the browser localhost:5000

 ## Push our application image in the ECR- Elastic Container Registry
 
 - Go on AWS console, search for ECR services and create a repository. give the name cloudnativeapp
 ![1](https://user-images.githubusercontent.com/102819001/235049594-598120f5-1e02-4c3a-b6ea-da26487d4abf.png)

Our ECR is created
![1](https://user-images.githubusercontent.com/102819001/235049699-f96da8a0-77ba-4e4b-8297-dbf9796c0975.png)

- To push the application image, we open the repository and click on view push commands. Each command need to be execute in the terminal
 1- Retrieve an authentication token and authenticate your Docker client to your registry.
Use the AWS CLI: aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 507180652719.dkr.ecr.us-east-1.amazonaws.com 

![1](https://user-images.githubusercontent.com/102819001/235050341-35c821c9-929f-4485-8820-9ec37314b476.png)

2- Build your Docker image using the following command. For information on building a Docker file from scratch see the instructions here . You can skip this step if your image is already built: docker build -t cloudnativeapp

 ![1](https://user-images.githubusercontent.com/102819001/235050585-dc1e3738-8e7d-4706-b71a-93e76614666a.png)

3- After the build completes, tag your image so you can push the image to this repository: docker tag cloudnativeapp:latest 507180652719.dkr.ecr.us-east-1.amazonaws.com/cloudnativeapp:latest

4- Run the following command to push this image to your newly created AWS repository: docker push 507180652719.dkr.ecr.us-east-1.amazonaws.com/cloudnativeapp:latest
 ![1](https://user-images.githubusercontent.com/102819001/235050868-e0abd6dc-53f7-44f3-819b-a24109874d0b.png)

**Our docker image is now in the ECR**

 ![1](https://user-images.githubusercontent.com/102819001/235051015-3afa29e7-9658-47e0-b378-5fad1fa27cdd.png)

 ## Create our Kubernetes Cluster with EKS
 - Create a role to manage the cluster
 
 ![1](https://user-images.githubusercontent.com/102819001/235051962-88e84102-35dc-4940-a8c9-934bf8813e87.png)
 
 ![1](https://user-images.githubusercontent.com/102819001/235326548-50da358e-b5d3-4f63-a960-3b8f524aa337.png)

 
 - On AWS console, search EKS-Elastic kubernetes services and create a cluster and follow the different steps
 
 ![1](https://user-images.githubusercontent.com/102819001/235051395-fcee6e97-53b9-427b-9a02-ab6b0febba3f.png)
 
 ![2](https://user-images.githubusercontent.com/102819001/235326556-e0b1d0f0-4844-477c-bfca-0301550546ce.png)

Now that my cluster is created, l need to deploy my application on kubernetes

## Deploy our application on Kubernetes

- Check if the cluster just created is active, Create nodes inside the cluster
![1](https://user-images.githubusercontent.com/102819001/235326667-3817eb84-62af-498a-870a-f9babfa6722b.png)

The node role is created
![1](https://user-images.githubusercontent.com/102819001/235327067-d18a9310-506e-4d7b-bb08-cb6ec2e28b9f.png)

![1](https://user-images.githubusercontent.com/102819001/235355976-777c64f1-6b88-4066-971a-c4b3433b7dee.png)
 
 - Let us write the yaml file in python.the code can be checked on eks.py. Run the code with py eks.py
 - let check the pods, the deployments and the service

![1](https://user-images.githubusercontent.com/102819001/235356523-80681cf2-2e18-4721-96b5-0671d2d62b18.png)

- Port forwarding our application. 
 
![1](https://user-images.githubusercontent.com/102819001/235356963-34367d0d-5cd2-4276-b4ff-e022813d917e.png)

Our application is running very well on port 5000


 
 

