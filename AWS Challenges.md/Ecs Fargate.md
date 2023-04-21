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
-Serveless (no server, no agents to install,no security batches to update, no schedule maintenance downtime,etc...);
- it's web based application, no application to install and maintain unless you decide to deploy with the Aws CLI;
- It's autoscaling service AWS LaMBDA is cheaper but don't scale vertically. it's can scale vertically by increasing the CPU and the memory allocation or horizontally by spinning out more tasks in the service depending on schedule of web traffic or workload;
- it's time saving solution;
- the cost of ownership is 0 because we don't have to invest in servers. we just rent cpu and memory
By monday morning, the testers will have the tester application url. Deployment will take minute not hours





**Save the application image in our dockerhub repository**


**Create an Ecs Fargate task definition**


**Create an ECS Cluster**


**Launch the task in the cluster**


**Test the application**



**View the ressource footprint in cloud formation**


**Delete the test-cluster, test-vpc and test-task-definition
