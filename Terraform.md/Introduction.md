## What is Terraform?
   Known as an Iac, **Terraform** is a provisioning infrastructure tool. It used to automate the provisioning our infrastructure on the platform where our application will be deployed and manage also the services of this platform.

## How does Terraform works?
Terraform has 2 mains components:
**1- Terraform code**: Terraform takes the configuration file you have written, create an API for it and submit the API to the target API of the cloud provider. So Terraform converts the configuration file (script file) in a language that the API of the cloud providers will understand.
**2- Providers for specific Technologies**:

## Why Terraform is mostly used in the market?/ Advantages of Terraform
We have many IAC tools in the market but Terraform is mostly used because, it can:
- **Manage any infrastructure**: Terraform providers can communicate with many API of cloud providers platform. So even if a company decides to move from one cloud provider to another one or to adopt a multicloud system, Terraform will easily update the configuration file without need to learn the new platform;
- **Track your infrastructure**: we dont have to log in the cloud platform to see the infrastructure you have created. You can simply logging in your terraform machine and look your **state file**. This state file will explain your entire organization (which ressources were used?,...)
- **Automate all the changes** because in real world, after creating our infrastructure for our project, we will continue and we will need to adjust or change things and instead of doing that manually, Terraform will be very helpful. The changes can be: Add the number of servers, of containers, change the services, deploy more microservices, add some security configurations or remove something, etc... After making a change, you can put your terraform file in a github repository and share with  your peers, so that they can give their feedback;
- **replicate our first infrastructure**
- **Standardize configurations** : With terraform, you standardize the way you configure your infrastructure.

## What is Terraform lifecycle?
**Step1: Initialise the repository for the Configure file**
It is important to create a repository where the configuration file will be located
**Step2:Write the configuration files**
To write your configuration file (terraform project), we just need to:
- Go to **Terraform Hashicorp** on your browser, 
- Check the documentation related to the cloud provider of your choice,
- Select the ressources you need for your configuration. The cloud providers will give you all the detail to write these ressources;
- Copy the code and change the information

*NB: If you don't find a ressource in the documentation related to your cloud provider, that's mean Terraform doesn't support this ressource*
**Step2: Plan - Review the changes Terraform will make to your infrastructure**
Before executing your configuration file, we need to check if it is correct. To do that, Terraform supports a tool called **driden**. With this tool, we can see what will happen with our configuration file and make the necessary adjustments before execution. So, at this step, we use the command **Terraform Plan**

**Step3: Aplly the changes**
Terraform provisions your infrastructure and update the state file

**Step4: Destroy**
Delete our configuration file

## Contents of a Terraform file
A Terraform file contents at leat the following informations:

