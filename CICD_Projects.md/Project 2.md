## **Cloud Project: Luxury Hotels & Resorts company migrating application and data to the cloud** 

This project is a real based scenario.

**The Business Problem of this company**: The hotel received a lot of customers per day but didn't know if they are infected to the covid 19 or not. Because, they are very concerned about the safety of the guests and employees, the General Manager of the company requested to the IT engineer to create a new application that we help guests to show if they are infected or not. Like this, every time a new guest come to check-in the hotel, he has to present his negative test. The receptionist will look at the test and scan that for documentation. The application name is ***Covid-19 Testing Status System***. The application was created and hosted in their corporate data centers sitting in one server machine and the data was saved in another server running MySql.But with time, the number of guests increased, they have a lot of traffic and that impacted the application. The application, becomes to have lack of ressources to keep running with the demand and also they have a small data center, so they cannot increase the number of servers. Even if they have space in their big data center, they don't have enough time to order a new hardware and time for installation.
So they decide to **migrate their data to the cloud**.
They hire a consulting team and based of the differents inputs, they create a solution.
 TThey decided to go with Google cloud because the hotel has already some partnership with google. So the components to be created in this cloud are:
 - **VPC**: Virtual Private Cloud which virtualise the network in the cloud provider space
 - **GoogleCloudSQL** which can support MySQL already on premise environnement
 - **Google container Registry (GCR)**: will be used for our application. the applicastion running in a VM on premise, will be running on top of a containerize architecture (docker image). They will create a docker image that will be saved inside a repository as GRC
 - **Google Kubernetes Engine (GKE)**:  to deploy the application.The application will run inside the Kubernetes Engine cluster. When the application is ready in the k8s cluster, it will be connected to the google cloud SQL;
 - **S3** : was already used by the company to store some files to save money. S3 is just a storage in the AWS cloud, the more you use, the cheaper wu pay. So the company want to continue to take advantage of it. When the receptionist open the application and click on **add guest result**, there is a form she has to fill related to the name, the address of the guest, covid test. The receptionist will scan every test and save in pdf format.All these files on-premises environnement are sitting in the application server. But when the company decided to move to the cloud, they cannot put these files with the application no more. So, with the consulting team, decided to saved all these files in a S3 bucket.   
 - **Terraform**: The IT manager wants also to make his architecture and application more agile by using Devops features to automation every task. The Consulting team advise to use Terraform to deploy all this environnement. Inside the **tf files**, we will describe what you want to the cloud providers. Terraform will communicate with the API of the cloud provider and the resources will be created. 
 Now, we have a **multicloud Infrastructure** to deploy.
 
 **Step 1: Create users in AWS and GCP 
 
 In AWS
 - Go to the console and click on IAM
 ![1](https://user-images.githubusercontent.com/102819001/232342193-e2aa1f91-fd82-44f8-b31b-c2b360b06db8.png)
 
 - Go to create user and give a name to your user **terraform-en-1
 ![2](https://user-images.githubusercontent.com/102819001/232343504-93ffcd2e-c9f7-4e35-8ad1-b6d5623742a8.png)
 - Give a permission to the user :Attach a policy
 ![3](https://user-images.githubusercontent.com/102819001/232343560-d65d3a98-2bea-4404-8edf-111c9be494f2.png)
 - Give the aws S3 full access to this user
![4](https://user-images.githubusercontent.com/102819001/232343583-1733541a-7489-4ef4-b9e1-a2e9ea84ca45.png)
- Review and create user: Our user is created
![5](https://user-images.githubusercontent.com/102819001/232343666-684dc990-791d-485d-8bdd-baa11aa11468.png)

