In this project, we will learn how to host a static website in AWS using S3 bucket, route 53, Certificate manager and cloudfront. 

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/ca27871d-b90c-44c4-a601-b2e727849d01)


**Description of the Architecture of the project**: When a user acces a website, it should be resolved to an endpoint from Route 53. The endpoint will redirect to the cloudfront to rebalance the global audience and reduce the latency and give a better user experience to customers. The certificate manager will be issued the website to use https protocolinstead of http which will actually make the website more secure and lastly, cloudfront will reach out to AWS s3 to serve users 
with the contents.

**AWS Services to use for this project** :
- **Amazon S3**: is an object storage service offering industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can store and protect any amount of data for virtually any use case, such as data lakes, cloud-native applications, and mobile apps. This means users can store and retrieve any amount of data, at any time, from anywhere on the web. With cost-effective storage classes and easy-to-use management features, you can optimize costs, organize data, and configure fine-tuned access controls to meet specific business, organizational, and compliance requirements.

- **Amazon route 53** is a highly available and scalable Domain Name System (DNS) web service. Route 53 connects user requests to internet applications running on AWS or on-premises. It is the easiest way to manage Domain names and DNS routing for websites and applications, which helps to ensure a fast and reliable user experience

- **Amazon cloudfront**: is a content delivery Network (CDN) offered by AWS. It speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files, videos, and API to the end users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the request is routed to the edge location that provides the lowest latency (time delay), so that content is delivered with the best possible performance. If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately. If the content is not in that edge location, CloudFront retrieves it from an origin that you've defined—such as an Amazon S3 bucket, a MediaPackage channel, or an HTTP server (for example, a web server) that you have identified as the source for the definitive version of your content.

- **Amazon Certificate Manager**: AWS Certificate Manager (ACM) handles the complexity of creating, storing, and renewing public and private SSL/TLS X.509 certificates and keys that protect your AWS websites and applications. The most common application of this kind is a secure public website with significant traffic requirements. ACM also simplifies security management by automating the renewal of expiring certificates. So, the ACM is a service that lets you easily manage and deploy SSL/TLS certificate for your websites and applications. With ACM, we have https which is more secure for our application than http.


## Step 1: Connect to our AWS Console, create a S3 bucket

Give a name to the S3 bucket and make it public

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/1567a466-fcb2-4a17-a58e-6fd9e4677081)

## Step 2: Host a website inside the S3 bucket

We can use our own domain name but for the purpose of this project, we will use a free website template of https://www.free-css.com/free-css-templates/page291/hightech. Download the content of this website and save it. Click on the new S3 bucket and upload the folder or the files contents of your website

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/c7a4e00d-ac6e-417f-b786-ba705a55cbb1)


## Step 3: Enable the host static of this website

- Go on propertiess

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/79d05e4a-859e-47f0-87d6-0bd80e65e630)

- Scroll down and click on **static website hosting**, edit and select enable

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/8d84fd80-5f97-462a-a959-bffdf32219ef)

## Define the entrypoint of our website/ the default page

After enabling Stati website hosting, go to index document and give the name index.html. Save all changes

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/b001096f-f79f-4c7f-96d1-291584425ae7)

At the end of the page, we have the url of our s3 bucket

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/9aba66d4-60fa-46bd-bec3-96d63fdddc6f)


## Access our s3 bucket from the browser

Take the url of the s3 bucket and paste in the browser

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/5134354f-9153-46b6-8b4c-1a0b6c1bdd5e)

We noticed that we cannot access our website

## 
Even if we have make our content public, we are not able to access our website from the browser. To troubleshoot that, we need to verify that

- Go 




