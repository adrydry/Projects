## What is Terraform?
   Known as an Iac, **Terraform** is a provisioning infrastructure tool. It used to automate the provisioning our infrastructure on the platform where our application will be deployed and manage also the services of this platform.

## How does Terraform works?
Terraform has 2 mains components:
**1- Terraform code**: Terraform converts the configuration file (script file) in a language that the API of the cloud providers will understand
**2- Providers for specific Technologies**:

## Why Terraform is mostly used in the market?
We have many IAC tools in the market but Terraform is mostly used because, it can:
- **Manage any infrastructure**: Terraform providers can communicate with many API of cloud providers platform. So even if a company decides to move from one cloud provider to another one or to adopt a multicloud system, Terraform will easily update the configuration file without need to learn the new platform;
- **Track your infrastructure**: we dont have to log in the cloud platform to see the infrastructure you have created. You can simply logging in your terraform machine and look your **state file**. This state file will explain your entire organization (which ressources were used?,...)
   - **Automate all the changes** because in real world, after creating our infrastructure for our project, we will continue and we will need to adjust or change things and instead of doing that manually, Terraform will be very helpful. The changes can be: Add the number of servers, of containers, change the services, deploy more microservices, add some security configurations or remove something, etc...;
- **replicate our first infrastructure**
