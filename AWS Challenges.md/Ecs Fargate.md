## AWS ECS FARGATE
In this project, we will learn more about Ecs Fargate

Consider that my application is ready for deployment. It's a long weekend and l don't have the server or network engineer on-call. The application has many microservices and l'm not sure about the server hardware requirements (how many servers? and for how long?).

The deployment solution is **FARGATE**. Fargate is preferred because:
- deploys in minutes, pay for seconds of vCPU and memory used;
- no need for server admin or network engineers
- start with modest server hardware specifications
- can scale up or/and scale out the solution
- can be monitored with cloudwatch
**Swat deployment with Fargate**: 
-Serveless (no server to provision, no OS to install, no agents to install,no security batches to update, no schedule maintenance downtime,etc...);
- it's web based application, no application to install and maintain unless you decide to deploy with the Aws CLI;
- It's autoscaling service AWS LaMBDA is cheaper but don't scale vertically. it's can scale vertically by increasing the CPU and the memory allocation or horizontally by spinning out more tasks in the service depending on schedule, web traffic or workload;
- it's time saving solution, Deplozement takes minute rather than dazs or hours
- the cost of ownership is 0 because we don't have to invest in servers. we just rent cpu and memory.
For data persistent, we can use an external storage like s3
By monday morning, the testers will have the tester application url. Deployment will take minute not hours
 **FOCUS ON THE CODE NOT THE SERVERS**

We will lunch an ECS cluster included a dedicated vpc included an internet gateway, a couple of public subnet and in one of which, we we launched our ECS fargate task. It will pull our application image from the repository and running as a container. This fargate task will have a private and public IP adress. It will also get a security group to control access. We will leave Port 80, open for internet traffic
**Save the application image in our dockerhub repository**
- Go to C disk- search Users/ Administrator - create a folder Tester1 - Inside this folder create a folder src - Inside this folder create the folder html and inside this html folder Create a text file and convert it to a html file. This static file will be use as our web application 

![1](https://user-images.githubusercontent.com/102819001/234862525-2b5967b7-4faf-46da-88d3-32aba6d6cf42.png)

- Inside the Tester1 folder, create a a text a text file and name it Dockerfile
-
![1](https://user-images.githubusercontent.com/102819001/234863703-ed15ca0b-e5b6-4851-aaae-0e386baefb6f.png)
 
 - Open our Docker file with notepad and Write the syntax of our Docker file. Save and close. Push the code to docker repository
 
 ![1](https://user-images.githubusercontent.com/102819001/234864312-c589dc78-924b-4cdb-954f-6c8e9e98d054.png)

- Install Docker on our laptop : Go to the documentation page of Docker and download the executable file

![1](https://user-images.githubusercontent.com/102819001/234865149-306061bc-b716-4390-9978-0c8e1b70976a.png)
 - Open Powershell and choose Run ISE as administrator and check if Docker is installed by using docker --version
 
![1](https://user-images.githubusercontent.com/102819001/234865886-bc5010fa-9b8e-4573-8848-f9125b38de22.png)

- Go to the directory where the Dockerfile is located and Build my docker image by using the command **docker build -t hello-fargate .** And pull the image to the docker repository

![1](https://user-images.githubusercontent.com/102819001/234869035-a58678be-88ba-4fba-8d79-a0b2a5e145ec.png)

- Check the avaibility of my image by using **docker images**
![1](https://user-images.githubusercontent.com/102819001/234870309-6260bfd0-8183-48e3-9399-8a7bd57d9c0e.png)

- Create my container and check the avaibility **docker run -d -p 80:80 image name** and **docker ps -a**

![1](https://user-images.githubusercontent.com/102819001/234867573-2ef93094-eda6-44c3-a7aa-7c7595d3f900.png)

- Let test our application. Go on the browser and just put **localhost**. The message will appear. Our web application is running. So the docker image passed the test application
![1](https://user-images.githubusercontent.com/102819001/234871452-4ce12b6d-d0f1-4edc-8b35-c527b8160540.png)

**Create an Ecs Fargate task definition**
Go on ECS on AWS console and create a task definition in json
![1](https://user-images.githubusercontent.com/102819001/234884438-0623dcd7-c4ad-4b06-919f-cade33a89e0e.png)

![1](https://user-images.githubusercontent.com/102819001/234884751-0cf1f8e0-9d18-4e19-a64b-ab0d8c74dce1.png)


**Create an ECS Cluster**
On the left of ecs page, click on Cluster and Create a cluster
![1](https://user-images.githubusercontent.com/102819001/234892225-a897fb30-24de-4389-84b4-7b7a9b886d1c.png)

The new cluster is visible on Cloudformation dashboard
![1](https://user-images.githubusercontent.com/102819001/234892702-e712c208-2cd3-4ce9-9edb-085654caa7e1.png)

- Go on vpc dashboard. Give the name test_vpc to this vpc
![1](https://user-images.githubusercontent.com/102819001/234895510-d3371736-92d4-4508-8d3f-93371c760521.png)
 
- Return to cloudformation and check the events. the cluster is created
 ![1](https://user-images.githubusercontent.com/102819001/234896719-fe100168-e076-4447-ba47-87708674fcab.png)

**Launch the task in the cluster**


**Test the application**



**View the ressource footprint in cloud formation**


**Delete the test-cluster, test-vpc and test-task-definition
