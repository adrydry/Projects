In this project, we will learn how to host a static website in AWS using S3 bucket, route 53, Certificate manager and cloudfront. 

![1](https://github.com/adrydry/Cloud_Devops_Projects2023/assets/102819001/ca27871d-b90c-44c4-a601-b2e727849d01)


**Description of the Architecture of the project**: When a user acces a website, it should be resolved to an endpoint from Route 53. The endpoint will redirect to the cloudfront to rebalance the global audience and reduce the latency and give a better user experience to customers. The certificate manager will be issued the website to use https protocolinstead of http which will actually make the website more secure and lastly, cloudfront will reach out to AWS s3 to serve users 
with the contents.

**AWS Services to use for this project** :
- **Amazon S3**: is an object storage service offering industry-leading scalability, data availability, security, and performance. Customers of all sizes and industries can store and protect any amount of data for virtually any use case, such as data lakes, cloud-native applications, and mobile apps. This means users can store and retrieve any amount of data, at any time, from anywhere on the web. With cost-effective storage classes and easy-to-use management features, you can optimize costs, organize data, and configure fine-tuned access controls to meet specific business, organizational, and compliance requirements.

- **Amazon route 53** is a highly available and scalable Domain Name System (DNS) web service. Route 53 connects user requests to internet applications running on AWS or on-premises. It is the easiest way to manage Domain names and DNS routing for websites and applications, which helps to ensure a fast and reliable user experience

- **Amazon cloudfront**: is a content delivery Network (CDN) offered by AWS. It speeds up distribution of your static and dynamic web content, such as .html, .css, .js, and image files, videos, and API to the end users. CloudFront delivers your content through a worldwide network of data centers called edge locations. When a user requests content that you're serving with CloudFront, the request is routed to the edge location that provides the lowest latency (time delay), so that content is delivered with the best possible performance. If the content is already in the edge location with the lowest latency, CloudFront delivers it immediately. If the content is not in that edge location, CloudFront retrieves it from an origin that you've defined—such as an Amazon S3 bucket, a MediaPackage channel, or an HTTP server (for example, a web server) that you have identified as the source for the definitive version of your content.

- **Amazon Certificate Manager**: AWS Certificate Manager (ACM) handles the complexity of creating, storing, and renewing public and private SSL/TLS X.509 certificates and keys that protect your AWS websites and applications. The most common application of this kind is a secure public website with significant traffic requirements. ACM also simplifies security management by automating the renewal of expiring certificates. So, the ACM is a service that lets you easily manage and deploy SSL/TLS certificate for your websites and applications. With ACM, we have https which is more secure for our application than http.


## Step 1: Connect to our EC2 instances and create a S3 bucket






































