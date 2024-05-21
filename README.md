# Static Website Hosting on S3 Bucket with Cloudfront Distribution 

## Project Description

The goal of this project is to create a static website hosted in an Amazon S3 bucket with CloudFront distribution to ensure high availability, performance, and content delivery optimization. The website will be public, allowing anyone to access its content.

## Architectural Diagram:

![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/634cb5bd-bc20-4ecf-b580-4b6c3fb27f94)


## Prerequisites

Before starting this project, ensure you have the following:

* [AWS Account](https://github.com/aniwardhan/Getting-Started-with-Terraform.git): If you don't have one, create an AWS account at aws.amazon.com
* [Terraform Environment](https://github.com/aniwardhan/Getting-Started-with-Terraform.git)
* [AWS CLI](https://github.com/aniwardhan/Getting-Started-with-Terraform.git): Install and configure the AWS Command Line Interface with appropriate permissions to interact with AWS services. 
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

* Create a file named [providers.tf](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/blob/main/provider.tf) to configure the specific cloud providers or services that your Terraform configuration will interact with.

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/18b3f111-8253-44b7-a7d1-6a7213878285)

  Once File created run the terraform init command so that Terraform downloads necessary plugins and resources required for connecting to AWS and managing your infrastructure.
 
  Run the following command to initialize your Terraform environment
  ```hcl
  terraform init
  ```

  ![image](https://github.com/aniwardhan/Host-a-static-website-in-S3-using-Terraform/assets/80623694/41915893-cbfb-4a70-a4bd-d00926f6edbb)

  ### Step 3: Create S3 bucket and add your static content ([createbucket.tf](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/blob/main/createbucket.tf))
  
  Here's a basic Terraform configuration to create an S3 bucket and configure it for static website hosting:
  
  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/5c257f44-2541-4d8a-ad3f-b6d7f9956b79)

  #### Upload files to your bucket

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/157851e7-0778-44b9-85fc-f822f2824983)

  #### If you want to upload entire folder use the code below:

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/946ac7e4-fb93-47ae-b3d6-e214882739eb)

  ### Step 4: Create policy to allow CloudFront to reach S3 bucket

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/0d415011-470e-4175-9357-4c4e0434552c)

  Assign policy to allow CloudFront to reach S3 bucket
  
  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/686feb84-9b90-4189-8187-fe46803f0df6)

  ### Step5: Configure Cloudfront Distribution ([cloudfront.tf](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/blob/main/cloudfront.tf))

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

  ### Step 6: Create [output.tf](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/blob/main/output.tf)

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/63c5d8ac-c626-44b7-9d8d-ca59bc696753)

  ### Step 7: Create [variable.tf](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/blob/main/variable.tf)

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

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/fd792560-8794-4151-97b9-553f3eb9f615)

  Check in AWS Management Console
  
  S3 Bucket Creation 

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/a00cbd71-043c-4f08-8272-fe319772668b)


  Static file "[index.html](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/blob/main/index.html)" is added to S3 bucket

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/027054ed-6612-47f3-abd2-2084d7aebd62)

  Cloudfront Distribution is Created with default root object as index.html

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/e008e0d3-dbf8-4a69-abfa-141db367053b)

  CloudFront geographic restrictions added

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/dab463b8-5c51-4e4d-a2d8-fb82020cc3cf)

  CloudFront Origin added

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/9fe2581c-ecb4-452b-ab57-e325b75ad81f)

  Copy the domain name of Cloudfront and check the output

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/fcb342db-5883-490d-b24f-287c936fa894)

  #### Step 10: Clean up Resources

  ```hcl
  terraform destroy -auto-approve
  ```

  ![image](https://github.com/aniwardhan/Cloudfront-and-S3-Website-Hosting/assets/80623694/0ec853c2-f11f-473a-bdd4-05d8856c4103)



      



