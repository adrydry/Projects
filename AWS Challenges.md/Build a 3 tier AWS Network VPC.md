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

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/4274f9fd-72f6-4a11-8ac2-9246376c0343)

## Create Private subnet in different AZ 

- Create myprivate subnet1 in us-east-1a
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/13240517-ee4a-4e83-aef3-da7d274373df)

- Create myprivatesubnet2 in us-east-1b
 
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/4478510e-4adb-42fe-bbbe-fa3d5a63e91a)




