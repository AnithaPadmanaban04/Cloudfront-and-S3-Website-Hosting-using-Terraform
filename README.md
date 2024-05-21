# Static Website Hosting on S3 Bucket with Cloudfront Distribution 

## Project Description

The goal of this project is to create a static website hosted in an Amazon S3 bucket with CloudFront distribution to ensure high availability, performance, and content delivery optimization. The website will be public, allowing anyone to access its content.

## Architectural Diagram:

![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/1e30f86e-564a-4fe7-85e8-d6fea01e5c5f)

## Prerequisites

Before starting this project, ensure you have the following:

* [AWS Account](https://github.com/AnithaPadmanaban04/Getting-Started-with-Terraform.git): If you don't have one, create an AWS account at aws.amazon.com
* [Terraform Environment](https://github.com/AnithaPadmanaban04/Getting-Started-with-Terraform.git)
* [AWS CLI](https://github.com/AnithaPadmanaban04/Getting-Started-with-Terraform.git): Install and configure the AWS Command Line Interface with appropriate permissions to interact with AWS services. 
* Static Website Content: Prepare the content you want to host, typically HTML, CSS, JavaScript, and images.
* Domain Name (optional): If you have a domain, you can configure CloudFront to use it. Otherwise, you can use the default CloudFront domain.

## Key Components
* Amazon S3: Amazon Simple Storage Service, used to store your static website content.
* CloudFront: AWS's content delivery network (CDN) that provides content caching and distribution.
* IAM Role/Policy: Permissions for S3 and CloudFront.
* Route 53 (optional): AWS's domain name service for domain management (if using a custom domain).

## Steps by Step Process
### Step 1: Setting up Terraform Environment
* Install Terraform and the AWS Command Line Interface (CLI) on your local machine. Configure your AWS credentials by running aws configure and provide your AWS access key and secret key.
* Create a working directory in your local machine and open the folder in MS Visual Code Editor to start the project
  
### Step 2: Initialize the Terraform Environment

* Create a file named [providers.tf](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/blob/main/provider.tf) to configure the specific cloud providers or services that your Terraform configuration will interact with.

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/f92c5ac1-2115-4285-9fc0-4e144ce7a318)

  Once File created run the terraform init command so that Terraform downloads necessary plugins and resources required for connecting to AWS and managing your infrastructure.
 
  Run the following command to initialize your Terraform environment
  ```hcl
  terraform init
  ```

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/33a2a6d0-af7f-4a26-b5cf-dbf4186cff4a)


  ### Step 3: Create S3 bucket and add your static content ([createbucket.tf](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/blob/main/createbucket.tf))
  
  Here's a basic Terraform configuration to create an S3 bucket and configure it for static website hosting:
  
 ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/7f14feb1-8415-454d-abad-d0492856f0fa)

  #### Upload files to your bucket

 ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/937eee3e-add9-44a4-a127-db6972188656)

  #### If you want to upload entire folder use the code below:

 ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/820f1004-cbf8-4228-b587-a8101c68f69f)

  ### Step 4: Create policy to allow CloudFront to reach S3 bucket

 ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/9e2ee175-b722-44f5-a190-48a5a8656394)

  Assign policy to allow CloudFront to reach S3 bucket
  
 ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/335b074a-006f-4f21-a8d1-269472f48c77)

  ### Step5: Configure Cloudfront Distribution ([cloudfront.tf](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/blob/main/cloudfront.tf))

  Here are the key configuration parameters and components used in setting up a CloudFront distribution for an S3-backed static website.

  * **Origin:** This section specifies the source for the content, indicating the S3 bucket, along with its ID, domain name, and any specific options like HTTP/HTTPS port configurations, the expected origin protocol policy, and supported SSL 
      settings.
  * **Enabled:** This parameter controls whether the CloudFront distribution is active.
  * **IPv6 Support:** This setting allows IPv6 traffic to be served by CloudFront.
  * **Default Root Object:** This option determines the default file or page to be served when the root URL is accessed.
  * **Aliases:** This configuration allows you to specify additional domain names, or CNAMEs, that CloudFront should respond to, in addition to the default AWS domain.
  * **Custom Error Response:** Defines the behavior for handling specific HTTP error codes, such as 404 (Not Found), including which page to display and the response cache duration.
  * **Default Cache Behavior:** This section outlines the default caching strategy for CloudFront, detailing the HTTP methods that are allowed, the targeted origin ID, whether query strings and cookies are forwarded, the protocol policy (like 
      HTTP to HTTPS), and the caching duration.
  * **Restrictions:** This block describes any specific restrictions for the CloudFront distribution, such as geographical or IP-based boundaries.

  These settings work together to create a high-performance content distribution network for your static website hosted on S3, with flexible options for handling errors, security, and caching.

  ### Step 6: Create [output.tf](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/blob/main/output.tf)

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/f4bde49e-23c2-46f2-af90-5a2924882ca3)

  ### Step 7: Create [variable.tf](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/blob/main/variable.tf)

  ### Step 8: Apply Terraform Configuration

  After creating all the necessary files execute the following Terraform commands 

  ```hcl
  terraform fmt

  terraform validate

  terraform plan

  terraform apply -auto-approve
  ```

  ### Step 9: Verify the Output

  Output in Terraform Environment

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/be41cd81-5698-4d9b-8d4e-a92b5157ad79)

  Check in AWS Management Console
  
  S3 Bucket Creation 

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/9a73d753-8648-45b7-ab81-a2832ad54908)

  Static file "[index.html](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/blob/main/index.html)" is added to S3 bucket

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/fdb05d94-8b0c-4a29-a22e-0fa9ec63c1f2)

  Cloudfront Distribution is Created with default root object as index.html

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/2bddde61-7e4c-4b60-8218-a343cfb051c5)

  CloudFront geographic restrictions added

 ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/914c4510-b2a5-4cc6-aaf5-770a50836580)

  CloudFront Origin added

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/0db17a77-7de5-4400-b913-bed3a8410a5f)

  Copy the domain name of Cloudfront and check the output

  ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/22fec53f-f5d8-40a6-bb7b-058cdaeb3f9e)


  #### Step 10: Clean up Resources

  ```hcl
  terraform destroy -auto-approve
  ```

 ![image](https://github.com/AnithaPadmanaban04/Cloudfront-and-S3-Website-Hosting-using-Terraform/assets/170385807/7125e690-d34e-4399-9170-072c55d707d0)




      



