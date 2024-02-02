hcl
```
# S3 bucket for website.
resource "aws_s3_bucket" "www-ipgame_bucket" {
  bucket = "www-ipgame"

  tags = {
    Name = "www-ipgame"
    Environment = "Dev"
    }
  }

resource "aws_s3_bucket_website_configuration" "www-ipgame_website" {
  bucket = aws_s3_bucket.www-ipgame_bucket.id

  index_document {
    suffix = "index.html"
  }

  error_document {
    key = "error.html"
  }
}



# S3 Allow Public read access as data object
# secure the bucket that you are creating from public acess

resource "aws_s3_bucket_public_access_block" "wwww-ipgame_bucket" {
    bucket = aws_s3_bucket.www-ipgame_bucket.bucket
    block_public_acls = true #prevents adding objects to buckets
    block_public_policy = true #bucket rejects policies that allow public access
    ignore_public_acls = true #if public access is granted by an acl it will be ignored
    restrict_public_buckets = true #only aws pricipals and authorized users can access bucket
}

# Server side encryption allows you to protect your data at rest ("at rest" means on a stable medium such as a HD, USB stick..etc)
# If your data is not encrypted at rest, and someone obtains the medium, they can potentially have acess to all your data
# AWS offers three types of encryption on S3:  SSE AES256, SSE KMS, SSE w/ customer managed keys

resource "aws_s3_bucket_server_side_encryption_configuration" "wwww-ipgame_bucket" {
    bucket = aws_s3_bucket.www-ipgame_bucket.bucket
    rule {
        apply_server_side_encryption_by_default {
            sse_algorithm = "AES256"
        }
    }
}

# Note: Versioning does not secure your bucket
# Versioning secures your objects from accidental deletion or override

resource "aws_s3_bucket_versioning" "www-ipgame_bucket" {
  bucket = aws_s3_bucket.www-ipgame_bucket.bucket
  versioning_configuration {
    status = "Enabled"
  }
}

# this resource will upload the website html to the bucket

resource "aws_s3_object" "content" {
# this object cannot be uploaded until the bucket is established first
  depends_on = [
    aws_s3_bucket.www-ipgame_bucket
  ]

  bucket = aws_s3_bucket.www-ipgame_bucket.bucket
  key    = "index.html" # specifices the name of the resource
  source = "./index.html" # specifies the path to the file that is being uplaoded
  server_side_encryption = "AES256" #  match the bucket encryption method
  content_type = "text/html" # if you don't specifcy the content otherwise aws will ask you download the html file
}


resource "aws_s3_object" "international_women" {
  depends_on = [
    aws_s3_bucket.www-ipgame_bucket
  ]

  bucket = aws_s3_bucket.www-ipgame_bucket.bucket
  key    = "internationalwomen.gif"
  source = "./internationalwomen.gif"
  server_side_encryption = "AES256"
  content_type = "image/gif"

}

```
