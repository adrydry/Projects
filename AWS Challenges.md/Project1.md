In this challenge, we will learn AWS by doing some services


## 1- IAM
It's not recommended to execute daily tasks with the root account. That's why is important to create differents users to secure the access in the console. Identity Access and Management, this service helps us to create users in our account.
In this project, we will create administrator user

![1](https://user-images.githubusercontent.com/102819001/233518450-d5709ceb-3678-4ba3-9e49-dec67bc7fef5.png)

The user can change this password at next sign-in. Click on Next and set the permissions for this user
**Create a group and attach give him full access as an aadministrator**
You can add this user to a group
![1](https://user-images.githubusercontent.com/102819001/233518691-861e3fd4-0ef7-4327-9860-c457ecbab78e.png)

![1](https://user-images.githubusercontent.com/102819001/233519017-5f00f31e-7e0c-4273-8bcc-51cdec9ad8cc.png)

![1](https://user-images.githubusercontent.com/102819001/233519259-199d9b41-627a-404f-b33c-f0ad28837f3b.png)
The new user is created
![1](https://user-images.githubusercontent.com/102819001/233519487-768c223a-28b0-4fa0-9293-db3ae41d0336.png)

**Add a tag** Tag is just a key-value pairs that can be added to a user to organize, track, or control access for this user. It can be an email address, a job title,...
![1](https://user-images.githubusercontent.com/102819001/233520044-2b4b0273-e69a-4803-9af2-642070aaabd6.png)
**The user is created**
![1](https://user-images.githubusercontent.com/102819001/233520179-34fa9151-7d64-49c3-bff9-9b304683ded6.png)

You can download the .csv file and send email with the log information to the users
![1](https://user-images.githubusercontent.com/102819001/233521138-16842899-75c7-4e37-95bd-70b2ee0709ea.png)
 
 The new user will use the link to connect to the AWS and he will have to change his password
 ![1](https://user-images.githubusercontent.com/102819001/233521358-22689e25-236c-4657-94e1-330457179036.png)

Now, he is connected to his own account

![1](https://user-images.githubusercontent.com/102819001/233521602-b04850d4-febe-4e33-913e-6592f562488d.png)

**well done**

To create **access key** for an iam user, choose the users who like to create acces key           
            
       ![1](https://user-images.githubusercontent.com/102819001/233523427-ec2866c7-06b3-4414-9021-43e1d3947cb7.png)
     
  Go on security credentials and click on create access key
  
        ![1](https://user-images.githubusercontent.com/102819001/233523650-35f0d01a-a2d1-4b72-a84f-2ac63a71c87a.png)
    
 Choose the best practices
 ![1](https://user-images.githubusercontent.com/102819001/233524135-5f44bbd4-8aba-4253-91eb-4f8f57d70d3b.png)
and download the .csv file and save in a secure location. Never shared it, even AWS will never ask you your secret key


**Download the CLI MSI Installer** at https://awscli.amazonaws.com/AWSCLIV2.msi.  The AWSCLI gives you the ability to automate the entire process of controlling and managing AWS services through scripts. In other words, the CLI will help us to take control of our AWS console
  ![1](https://user-images.githubusercontent.com/102819001/233526055-3f0dbe73-c940-4fbd-8e24-70383fbc9ce0.png)

To verify if the AWS CLI is well installed, go to the main menu, open cmd and after the command prompt, use **aws --version**













            
            
