In this project, we will learn how a EC2 instances can access a S3 bucket

**Step1: Install AWS CLI. Go on AWSCLI and copy the command to install the Awscli**

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/d73901a2-a10d-4894-9b91-16b69dcddaac)

**Step2: Go to the console and create a new role with full access on s3
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/b46db73d-6c4b-4bd5-bae3-c5aabf1a5398)

**Step3: Go to the instances, selection the instance, click on actions, security groups and attach to the instance the role created**
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/271fc9c6-5157-45eb-a7d1-2fb563a50191)

Now our access has a full access to the s3 bucket
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/b2a8ed4e-ccfb-4c07-8549-c4c17aa2a675)

**Step4: connect on the terminal with aws cli, use the command aws s3 ls. the new s3 bucket will be visible
