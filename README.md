# kindergarten-website-template
Hello. My name is Haripriya. I am an AWS Cloud Enthusiast and am writing this blog as a part of the #10weeksofcloudops challenge, created by Piyush Sachdeva, which I recently came across. This is the #week1 challenge, which is to host a static website in the cloud, using the CICD Pipeline.
Project 1:
The project involves hosting a static website on AWS S3, utilizing AWS CloudFront as a Content Delivery Network (CDN) to enhance website performance, creating a Continuous Integration and Continuous Deployment (CI/CD) pipeline for automated deployments, and enabling SSL with a custom domain name for secure connections.
1. GitHub is a web-based platform and service that provides a version control repository hosting service for software development projects. In short, it is a code hosting platform that allows developers to collaborate, manage, and track changes to their code, making it easier to work on projects as a team and maintain a history of code revisions.
2. AWS CodePipeline is an AWS service for continuous integration and continuous delivery (CI/CD). It automates the process of building, testing, and deploying applications, enabling faster and reliable software delivery.
3. AWS S3, short for Amazon Simple Storage Service, is a scalable and secure cloud-based storage service provided by Amazon Web Services (AWS).S3 is widely used for various purposes, including hosting static websites, storing and backing up data, and serving as a content delivery network (CDN) for distributing content globally.
4. Amazon Route 53 is a scalable and highly available Domain Name System (DNS) web service provided by AWS. It translates human-readable domain names into IP addresses and efficiently routes internet traffic to AWS resources and other endpoints.
5. Amazon CloudFront is a fast and secure content delivery network (CDN) service provided by AWS. It distributes content globally, reducing latency and improving the performance of websites, applications, and media by caching data at edge locations closer to users.
6. AWS Certificate Manager (ACM) is a managed service provided by Amazon Web Services (AWS) that allows you to easily provision, manage, and deploy SSL/TLS certificates for use with AWS services and external resources.
Services I have used
1. Version Control: GitHub 2. CICD Pipeline: AWS Code Pipeline 3. Static Website hosting: Amazon S3, Amazon Route53, Amazon CloudFront, AWS Certificate Manager.
Architecture Diagram:

![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/740a5f8f-dd78-41e1-9553-1d6a82f6745c)

All you need to start building this project:
* AWS Account
* GitHub Account
* A Domain( from Route53, GoDaddy, Hostinger etc
* Basic Website/HTML Template
* Project Steps:
* ✅ Step 1:Creating S3 bucket
* ✅ Step 2: Create a Hosted Zone [ You need to replace the NS records from your domain provider with the NS records from your hosted zone after creating it ]
* ✅ Step 3: Request / Import a Certificate (SSL/TLS) for secure HTTP communication for your domain and all subdomain from Amazon Certificate Manager (ACM)
* ✅ Step 4:Create a CloudFront Distribution
* ✅ Step 5:Connect Cloudfront distribution Domain name
* ✅ Step 6:AWS Code Pipeline
* Step 1: Create an S3 Bucket from which the static files will be hosted on our personal domain using Cloudfront and Route53.
  * Step 1.1: Log into AWS Management Console. Search for Amazon S3 in the search box. Click on create bucket.
  * Step 1.2: The bucket name will be www.<domainname>. Here it is www.priyagh13.tk any region. I will be going for us-east-1.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/b17d808e-b3dd-4338-8b6d-40ba65f3a4c6)

  * Step 1.3: Leave the other settings to Default, scroll down and click on create bucket.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/3185965d-a45c-4b00-9edc-bf56473236a4)

  * Step 1.4: Click on the bucket name. Go to the Properties tab and scroll down. Click on the edit button for Static Web Hosting.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/de8b1f41-8227-4449-95b0-60b4753f5702)
  * Step 1.5: Now change it to enable. Place the name of the index document, which we will upload in s3 for static web hosting later. Usually, it is index .html.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/d14dd891-90d8-46b4-bf24-d866cdf7ef02)

  * Step 1.6: Scroll down and save changes. 
* Step 2:Create a Hosted Zone Step

  * 2.1:Goto Amazon Route53→ Hosted Zone. Enter Domain name and select Type as Public Hosted zone then click on create hosted zone. 

![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/c15df18e-97eb-4552-9338-8182bc43912e)
  * Step2.2: You need to replace the NS records from your domain provider with the NS records from your hosted zone after creating it.

![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/95afeec9-95ea-4429-be6e-c27efcbfa52a)
* Step 3:  In this step, we will be securing our domain name by using an SSL certificate generated by ACM( AWS certificate manager).
  * Step 3.1: Go to AWS Certificate Manager—> Request Certificate.[Ensure that the region selected is N.Virginia].
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/af409356-7f82-4998-9dd2-a72be5e8bb26)

  * Step 3.2: Under fully qualified domain names, mention your domain name in the below format.
*.<domain_name>
<domain_name>
Let the validation method be DNS Validation.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/8afe03c5-d6d6-4535-8cc9-5b58ac8cc3cd)

  * Step 3.3: While the Status for the certificate changes to Issued, create the records for Certificate Manager in Route53.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/92b5b092-7d9d-4d17-b6d5-f6cb9d389a42)
  * Step 3.4: Once you refresh, the status for the certificate will change to Issued.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/4b64cb96-c32d-47f4-8dab-8f7e5a0f1ebc)

* Step 4: Building a Content Delivery Network using CloudFront. This will connect to the s3 bucket we created earlier, and provide a distribution domain name that will be accessible from multiple edge locations.
  * Step 4.1:Goto Amazon Cloudfront→ Create a CloudFront Distribution. Under Origin Domain, select the s3 static website URL.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/f9a63a35-6c5e-4fa5-8d4a-3c606eb5e69d)

  * Step 4.2: Under Origin Access—> Legacy access identities—>Click on create new OAI.
Select your Bucket URL.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/10bc3666-62c9-44ee-94e2-7bfea23fbcd3)

  * Step 4.3- Scroll down to the viewer Protocol policy and choose” Redirect HTTP over HTTPS”
<img width="329" alt="image" src="https://github.com/priya241302/kindergarten-website-template/assets/119650186/cf0133ea-7a0c-4a2e-b27e-9ae3b7fd5b35">


  * Step 4.4: Enable Security Protection under WAF. Scroll down to settings. Add the alternate domain name as “priyagh13.tk.”
Add the SSL Certificate from the Dropdown.
  * Step 4.5: For Default root Object→ index.html.Scroll down and click on Create Distribution.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/206a18cd-ac03-4a17-b668-ea0bf19f441a)

![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/064541ba-6422-486a-bb42-7718943fc115)

* Step 5: Connect Cloudfront distribution Domain name to domain name., This will help us access our domain securely from any edge location, through our domain name.
Instead, you can also use the distribution domain name to access the static website.
  * Step 5.1: Go to Route53→Hosted Zones→Your Domain→Create record.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/16c98749-7561-427b-8b00-f1ce85dc7c49)

  * Step 5.2: Choose Record Name→www Record Type→A. Select Alias. Route traffic to→ CloudFront Distribution. Select the CloudFront distribution and create the record.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/e802dca0-1698-4c1e-ae59-1dbd307b5480)

* Step 6: Now your static website has been successfully created, but the bucket is empty. To send files to s3, we will be creating a CI/CD Pipeline using AWS CodePipeline.
  * Step 6.1: Go to the Search bar in AWS Management Console --> CodePipeline-->Pipelines--> Create Pipeline.
  * Step 6.2: Ensure that the pipeline is being created in the same region as your s3 bucket[Since i created s3 bucket in us-east-1, will be creating the pipeline in the same region].
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/20f38be5-b5fa-426a-b785-85ac7335fcac)

  * Step 6.3: For the Source provider, I have chosen GitHub Version 2. ( as this was recommended over version 1), Click on connect to Git Hub and create the connection.Once the connection has been established, Choose your code repository and branch.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/6b4cb13c-36ea-4b7a-8b04-ddff4da45f1a)

 ![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/9fdf1432-a0bf-4e5d-8919-a9ff629efc58)




  * Step 6.4:We can skip the build stage.
  * Step 6.5: We are in the deployment stage. Under Deploy Provider–Choose Amazon S3, and choose your bucket name under the bucket. Select the checkbox for extract files before Deploy.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/5c5c0092-b60a-4367-9d38-ec83cd397f48)


  * Step 6.6:Review the pipeline and click on Create pipeline.
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/9b38074a-264e-4f7b-af4f-60497c5052e4)


Final Step of Action: Once all the stages turn green, go to your Static Website
![image](https://github.com/priya241302/kindergarten-website-template/assets/119650186/868615f4-1f18-46be-9ee6-0fed412535f1)

Thank you for joining me on this exciting journey through this blog I hope this helps you to build this project.
Also Make sure you clean up your AWS resources, after completing the project, to save costs.
References:
https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html
https://www.youtube.com/playlist?list=PLl4APkPHzsUUc8HOEIwfB3Z2uxRv2SKOG




