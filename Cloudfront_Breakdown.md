
- **AWS CloudFront Distribution: site_access**

  - **Origin Configuration:**
    - Configures the CloudFront distribution to use an S3 bucket named "www-ipgame_bucket" as the origin.
    - Specifies the regional domain name of the S3 bucket and assigns the origin ID as "s3."
    - Sets up S3 origin configuration with an access identity for added security.
```
  resource "aws_cloudfront_distribution" "site_access" {
    # Origin configuration for S3 bucket
    origin {
      domain_name = aws_s3_bucket.www-ipgame_bucket.bucket_regional_domain_name
      origin_id   = "s3"

      # S3 origin configuration with access identity
      s3_origin_config {
        origin_access_identity = aws_cloudfront_origin_access_identity.OAI.cloudfront_access_identity_path
      }
    }

```

  - **Settings:**
    - Enables the CloudFront distribution.
    - Sets the default root object to "index.html."
```
    # Enable the CloudFront distribution
    enabled             = true
    # Set default root object to "index.html"
    default_root_object = "index.html"


```   



  - **Default Cache Behavior:**
    - Defines the default cache behavior for the distribution.
    - Allows "GET" and "HEAD" methods.
    - Caches responses for "GET" and "HEAD" methods.
    - Configures forwarding settings for query strings and cookies.
    - Sets the viewer protocol policy to "https-only."

```

    # Default cache behavior settings
    default_cache_behavior {
      allowed_methods  = ["GET", "HEAD"]
      cached_methods   = ["GET", "HEAD"]
      target_origin_id = "s3"

      # Forwarding settings
      forwarded_values {
        query_string = false
        cookies {
          forward = "none"
        }
      }

      # Viewer protocol policy set to "https-only"
      viewer_protocol_policy = "https-only"
    }

```


  - **Price Class:**
    - Sets the price class to "PriceClass_All," including all CloudFront edge locations.

```
    # Set the price class to "PriceClass_All"
    price_class = "PriceClass_All"

```


  - **Restrictions:**
    - Configures geo-restriction to whitelist access from the United States (US) and Canada (CA).
   
  ```
    # Geo-restriction settings (whitelist US and CA)
    restrictions {
      geo_restriction {
        restriction_type = "whitelist"
        locations        = ["US", "CA"]
      }
    }

```

  - **Viewer Certificate:**
    - Configures the viewer certificate to use the CloudFront default certificate for HTTPS.
```
   # Configure viewer certificate to use CloudFront default certificate for HTTPS
    viewer_certificate {
      cloudfront_default_certificate = true
    }

```
  - 

  - **Dependencies:**
    - Specifies a dependency on the existence of the CloudFront Origin Access Identity (OAI).

  ```
      # Dependency on CloudFront Origin Access Identity (OAI)
    depends_on = [aws_cloudfront_origin_access_identity.OAI]
  }

  ```
  
  
  
  
  
  
  
  
  
  
  hcl
  ```
  
  resource "aws_cloudfront_distribution" "site_access" {
    # Origin configuration for S3 bucket
    origin {
      domain_name = aws_s3_bucket.www-ipgame_bucket.bucket_regional_domain_name
      origin_id   = "s3"

      # S3 origin configuration with access identity
      s3_origin_config {
        origin_access_identity = aws_cloudfront_origin_access_identity.OAI.cloudfront_access_identity_path
      }
    }

    # Enable the CloudFront distribution
    enabled             = true
    # Set default root object to "index.html"
    default_root_object = "index.html"

    # Default cache behavior settings
    default_cache_behavior {
      allowed_methods  = ["GET", "HEAD"]
      cached_methods   = ["GET", "HEAD"]
      target_origin_id = "s3"

      # Forwarding settings
      forwarded_values {
        query_string = false
        cookies {
          forward = "none"
        }
      }

      # Viewer protocol policy set to "https-only"
      viewer_protocol_policy = "https-only"
    }

    # Set the price class to "PriceClass_All"
    price_class = "PriceClass_All"

    # Geo-restriction settings (whitelist US and CA)
    restrictions {
      geo_restriction {
        restriction_type = "whitelist"
        locations        = ["US", "CA"]
      }
    }

    # Configure viewer certificate to use CloudFront default certificate for HTTPS
    viewer_certificate {
      cloudfront_default_certificate = true
    }

    # Dependency on CloudFront Origin Access Identity (OAI)
    depends_on = [aws_cloudfront_origin_access_identity.OAI]
  }
```
