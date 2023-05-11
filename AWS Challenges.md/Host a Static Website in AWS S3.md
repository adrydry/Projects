HOST A STATIC WEBSITE ON AWS
Static websites deliver HTML, JavaScript, images, video and other files to your website visitors. Static websites are very low cost, provide high-levels of reliability, require almost no IT administration, and scale to handle enterprise-level traffic with no additional work.

What You Will Learn ? Host a static website using AWS Amplify in the AWS console. AWS Amplify provides fully managed hosting for static websites and web apps. Amplify’s hosting solution leverages Amazon CloudFront and Amazon S3 to deliver your site assets via the AWS content delivery network (CDN). Set up continuous deployment: Amplify offers a Git-based workflow with continuous deployment, allowing you to automatically deploy updates to your site on every code commit.

**Create a S3bucket**

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/bb311c13-4685-4278-94b9-95e9726e6539)

**Download a html static file and save**
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/80a35fd3-1157-45bc-831c-f0fc743ed551)
 
 **unzip the folder and upload files through the s3 bucket**
 ![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/a5571057-d6dc-4a58-ac31-485a9ab2242f)

**Go to properties and check "Static website hosting", enable this functionality**
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/62cba897-2476-4414-bf89-a831cf8a3926)

**Define the entrypoint of your s3 bucket and validate**
Most of the times, it's : index.html. After validation, we obtain a link that can be shared to access your s3 bucket

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/c15578a3-22f3-4caf-b7c8-f33c80228fdf)

**Access this url**
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/9e658e1a-52a0-4fa6-bde7-3aa0c73f6b35)
We noticed that the application is not accessible

**Select all the files, choose actions and click on Make public using ACL**
![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/3094e896-528e-4c54-9255-f4414d23b405)

## Now, our application is visible on the browser
