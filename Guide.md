# Creating a Static Website with S3 and CloudFront on AWS

## Part 1: Set up S3 Bucket for Static Website Hosting

1. **Create an S3 Bucket:**
   - Log in to the AWS Management Console.
   - Navigate to the S3 service.
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/7f57fb52-e8a3-4c21-a750-357d8d12d54c)
   - Click on "Create bucket" and follow the wizard to create a new bucket.
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/1ffae19d-8e11-4a3d-92bc-9467334b5d9a)
   - Create a globally unique bucket name:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/df379199-799d-416a-8a85-f6d000727fcb)
   - Leave all default settings as is and simply create the bucket


2. **Configure the S3 Bucket for Static Website Hosting:**
   - Select your newly created bucket.
   - - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/6fea72fc-718d-4513-9f97-f5d7a7dbc7b8)
   - Go to the "Properties" tab and choose "Static website hosting."
   - Enable static website hosting and specify the index document (e.g., `index.html`).

3. **Upload Your Website Files:**
   - Upload your HTML, CSS, JavaScript, and other static files to the S3 bucket.
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/874d82f5-21f1-4d99-9de7-de718549392e)
   - Example file set:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/73bdd4eb-7c2a-49a5-9eec-f61aa056ec25)
   - Ensure that yor files are uploaded properly:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/0d666d57-4994-4d9f-866b-87c7b353f887)
   - Click on an individual file to view details:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/d5f0fb5d-59e8-4fd0-a453-87f1e5dd80a8)
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/a51b14a3-b65a-43b2-8769-035cb23cac3a)


***If you attempt to select an object URL, you will recieve the following error message:***
![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/83ffd5ea-8805-47a8-b1d9-251a39c0e3b7)
***Addtionally, If you select "OPEN" you will access your object via pre signed url however, you wont see any images:***
![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/fa4ab5d2-5938-4172-be9b-af1ee7915477)


## Part 2: Set Up CloudFront Distribution
Cloudfront will make your files accessible WITHOUT making them public!

4. **Create a CloudFront Distribution:**
   - Go to the CloudFront service in the AWS Management Console.
   - Click on "Create Distribution" and choose the Web distribution type.
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/691c8588-19ad-4cf9-ba3f-d51639db8637)\\
   - Choose from a list of origin domains:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/501060b1-8f18-4032-a23a-41de8a5a83e4)
   - We will select Origin Access Control:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/8695e8e3-64f9-4d6e-96db-a9837acb20de)
   - Create "Control Setting":
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/58a4cd1c-7687-4622-831c-45b0dcbdb43a)
   - You MUST update the bucket policy!
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/03e7d539-6a3a-47f0-acf8-8a76009210ba)
   - Do NOT enable WAF:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/cef7f4aa-1b2c-4f96-a3fd-d4e23f8e944c)
   - Set "Default Root Object" to your index.html file:
   - ![image](https://github.com/mindmotivate/S3_Cloudfront/assets/130941970/a1e43a86-5570-4695-a5ba-4401c31933d9)
   - 






6. **Configure CloudFront Settings:**
   - In the distribution settings, set the "Origin Domain Name" to the S3 bucket endpoint.
   - Configure other settings such as caching behavior and distribution settings.

7. **Deploy CloudFront Distribution:**
   - Wait for the CloudFront distribution to deploy (this may take some time).

## Part 3: Add Custom Domain and SSL Certificate

7. **Purchase or Use Existing Domain:**
   - Purchase a domain through Route 53 or use an existing domain registered with AWS.

8. **Create or Import SSL Certificate:**
   - Go to the AWS Certificate Manager (ACM) and request a new SSL certificate for your domain.
   - You can also import an existing SSL certificate.

9. **Associate SSL Certificate with CloudFront:**
   - In the CloudFront distribution settings, under the "General" tab, click on "Edit."
   - Choose the custom SSL certificate from ACM in the "SSL Certificate" section.

10. **Update DNS Records:**
    - In Route 53 or your domain registrar, update the DNS records to point to the CloudFront distribution.

11. **Wait for DNS Propagation:**
    - DNS changes may take some time to propagate. Be patient until your domain is associated with the CloudFront distribution.

## Part 4: Testing

12. **Test Your Website:**
    - Access your website using the custom domain over HTTPS to ensure everything is set up correctly.

Now, your static website should be served securely through CloudFront with a custom domain. Keep in mind that setting up SSL certificates may incur costs, and you should regularly monitor your AWS resources for any changes or updates.
