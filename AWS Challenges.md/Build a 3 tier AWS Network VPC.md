At the end of this project, we will be able to:

- Create a custom VPC
- Create a custom subnet, public and private
- How can make a subnet public or private
- Creation of internet gateway, Nat gateway, Route table;

## Overview

3 tier architectures is a architecture with 3 layers:

1- The region (us-east-1 for our project). In this region, we have 2 avaibility zones
2- Under the region, we have the VPC. Inside the VPC, we have 6 subnets. 3 subnets: 1 public and 2 private per avaibility zones to maintain the high avaibility. The public subnet is attach to the frontend where the users will interact with the UA of the application. 1 private subnet will help to validate data and the other one to as a database for the data customers.

**Public subnet** is a subnet where internet gateway is attached to the route table. In our project, the public route table is attached to the public subnet of both avaibility zone

**Private subnet** is a subnet where the route table is not associated with the internet gateway. Every private route table is attached to each private subnet. Any user sending traffic from outside, we will not get access to the private subnet. Even if we have the internet gateway, we will created **the nat gateway** into differents AZ and different publics subnet. We will atach the each natgateway to each private subnet. 
**Route table** route your traffic for somewhere where you want to take it out. We will attach each natgateway to each private subnet so that nobody from outside will access my private resources as Databases. Even if the database will need internet to do some maintainance, it's important to secure form outside coming source. Like this, incase he needs internet, he will connect to the public subnet which is connected to the internet gateway.

## Default installation of Ressources in AWS

- VPC: By default, AWS has a VPC but it's not recommended to create our application on it. We need to create a custom VPC
- Subnets: We have to create also subnets by avaibility zones. To create Private subnet we need to have Elastic Ip
- Route table: We have 1 route table on which internet gateway is attached. No subnet is attached to this table. So click on **edit associations** and choose all the available subnets


## Create a VPC 

Go on VPC and click create a VPC. Just define the ipv4: 10.0.0.0/16. Our VPC is created in our us-east1

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/a68950b8-7945-4213-8092-45b3d839d687)

Our VPC don't contain any subnet

## Create public subnet in different Avaibility zones

Go to subnet, create subnet , choose the VPC just created.

- Create mypublicsubnet1 in us-east-1a

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/3d8d73ff-a628-4a63-ae2d-e62a4022b8d5)

- Create mypublicsubnet2 in us-east-1b

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/67d366ca-4e68-4b5a-96b6-2c8df7f4ee50)

## Create Private subnet in different AZ 

- Create myprivate subnet1 in us-east-1a
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/13240517-ee4a-4e83-aef3-da7d274373df)

- Create myprivatesubnet2 in us-east-1b
 
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/4478510e-4adb-42fe-bbbe-fa3d5a63e91a)

- Create myprivatesubnet3 in us-east-1a
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/b33edea2-28c9-4b4e-9ca4-3aa4cfe6d11c)

- Create myprivatesubnet4 in us-east-1b
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/225879ba-69e4-426d-b8d3-cf2f0091dcd9)

All our 6 subnets are created in 2 different AZ

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/ec40ea4e-1e7e-4a5f-9f09-c6c7c3dc55b6)

The route table will help us to make our public subnet a public subnet by attaching them to the internet gateway of our VPC

## Create route table

Go on route table, click on create route table, and select our vpc

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/c5f9ddd6-17b8-4e67-a605-bb8cc32b9be9)

Now, we need to attach the public subnet to this route table. Under the new route table, click on Subnet association. The list of all the subnets will appear and we have just to select our 2 public subnets

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/a3cde1bf-7513-4bec-aeac-e0df790fe40a)

## Create an internet gateway and attach to the vpc

Go to internet gateway, click on create internet gateway.  

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/556df81f-1b1b-4c7b-a9fe-659c9bcd7eb6)

We noticed that the state is **in detached mode**. Click on actions and attach vpc

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/3c69b3ae-4fe7-4755-9d94-9b17940c2359)

## Attach the internet gateway to the route table
Go to route table - click on edit route, add a route, select 0.0.0.0/0, target internet gateway and save the changes

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/3070ac67-8f94-45e2-9eb4-9f3270362d1a)

## Create our private route table

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/92214b0f-cdcc-4c87-af09-db1318fedc35)

## Attach the private subnet to the route table
Private subnet1 and 3 to privatetableroute1

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/66e50f7a-ebf0-44f6-9792-f58e2d4d788b)

Privatesubnet2 and 4 to privateroutetable2

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/ce6e935e-318a-43e0-91f3-33b580b15014)



Now that we have our internet gateway attach to our route, let's make our public subnet public

## 














