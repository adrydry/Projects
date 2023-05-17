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

**Private subnet** is a subnet where the route table is not associated with the internet gateway. Every private route table is attached to each private subnet. Any user sending traffic from outside, we will not get access to the private subnet. Even if we have the internet gateway, we will created the nat gateway into differents AZ and different public subnet. We will atach the each natgateway to each private subnet. 
**Route table** route your traffic for somewhere where you want to take it out.

