# Creating a Static Website with S3 and CloudFront on AWS

## Part 1: Set up S3 Bucket for Static Website Hosting

1. **Create an S3 Bucket:**
   - Log in to the AWS Management Console.
   - Navigate to the S3 service.
   - Click on "Create bucket" and follow the wizard to create a new bucket.

2. **Configure the S3 Bucket for Static Website Hosting:**
   - Select your newly created bucket.
   - Go to the "Properties" tab and choose "Static website hosting."
   - Enable static website hosting and specify the index document (e.g., `index.html`).

3. **Upload Your Website Files:**
   - Upload your HTML, CSS, JavaScript, and other static files to the S3 bucket.

## Part 2: Set Up CloudFront Distribution

4. **Create a CloudFront Distribution:**
   - Go to the CloudFront service in the AWS Management Console.
   - Click on "Create Distribution" and choose the Web distribution type.

5. **Configure CloudFront Settings:**
   - In the distribution settings, set the "Origin Domain Name" to the S3 bucket endpoint.
   - Configure other settings such as caching behavior and distribution settings.

6. **Deploy CloudFront Distribution:**
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
