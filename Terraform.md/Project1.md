## WRITE OUR FIRST TERRAFORM
At the end of this project, we will be able to:
- Install Terraform;
- How a good Terraform set up look like;



**Step 1: Install Terraform**
For this project, we install Terraform on our Windows Powershell. 
1- Verify if Terraform is already installed on our system by using the command **terraform -version**.

![choco 1](https://user-images.githubusercontent.com/102819001/231525907-8b169cf0-675b-45cd-8643-3f20c58cc219.png)

As we see, we have an obsolete version in our system. Because some cloud providers can only communicate with the update version of Terraform, we need to upgrade our Terraform version. The best way to do that is to refer to https://developer.hashicorp.com/terraform/downloads and select the OS on which we want to download Terraform
![choco install](https://user-images.githubusercontent.com/102819001/231536816-45d33217-217c-4be7-98d6-860300440ffb.png)

We download the package, save it, extract the execute file and copy the path. We go to environnement variable and edit the path, so that the program can recognize the location of our terraform executable.

![choco5](https://user-images.githubusercontent.com/102819001/231538250-795bb61f-3281-4e6d-a439-256927581996.png)

Paste the path of our terraform executable and click on ok
![choco6](https://user-images.githubusercontent.com/102819001/231538631-0362c2a1-df97-42f0-9829-3bd5fa4d43ff.png)

When we check the new version of our terraform, we see that we move from terraform **1.3.6  to terraform **1.4.4**

![new](https://user-images.githubusercontent.com/102819001/231539467-8b9e41c3-588e-4eb3-bffb-f5826d522c5a.png)
