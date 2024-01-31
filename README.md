
# Static Website with S3 and CloudFront on AWS
This guide outlines the steps to create a static website using Amazon S3 for hosting and CloudFront for content delivery. Additionally, it covers adding a custom domain and securing it with an SSL certificate.

## Step-by-Step Overview

### 1: Set up S3 Bucket for Static Website Hosting
Create an S3 Bucket: [create an S3 bucket](https://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html).

### 2: Set Up CloudFront Distribution
**Create a CloudFront Distribution:** [create a CloudFront distribution](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-console.html).

### 3: Add Custom Domain and SSL Certificate
**Purchase or Use Existing Domain:** [Route 53](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-register.html) (or use an existing one)

**Create or Import SSL Certificate:** [AWS Certificate Manager (ACM)](https://docs.aws.amazon.com/acm/latest/userguide/gs-acm-request-public.html).


## Additional Resources

- [Amazon S3 Documentation](https://docs.aws.amazon.com/s3/)
- [Amazon CloudFront Documentation](https://docs.aws.amazon.com/cloudfront/)
- [AWS Certificate Manager Documentation](https://docs.aws.amazon.com/acm/)
- [Amazon Route 53 Documentation](https://docs.aws.amazon.com/Route53/)

***Note:** Be mindful of AWS costs, especially with CloudFront and ACM, and monitor your resources regularly.*

