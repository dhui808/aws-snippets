### Configuring a static website on Amazon S3
    https://docs.aws.amazon.com/AmazonS3/latest/userguide/HostingWebsiteOnS3Setup.html
    
    Step 1: Create a bucket
    Step 2: Enable static website hosting
    Step 3: Edit Block Public Access settings
    Step 4: Add a bucket policy that makes your bucket content publicly available
    Step 5: Configure an index document
    Step 6: Configure an error document
    Step 7: Test your website endpoint
### Configuring a static website using a custom domain registered with Route 53
    https://docs.aws.amazon.com/AmazonS3/latest/userguide/website-hosting-custom-domain-walkthrough.html
    
    Step 11: Add alias records for your domain and subdomain
    
### Speeding up your website with Amazon CloudFront
    Step 1: Create a CloudFront distribution
        Need to specify Default root object - optional. If not psecified, the user has to enter the file name  
        for the root object (index.html).
        404 error from the origin (and potentially other non-200 statuses, are not supported?)
    Step 2: Update the alias record in Route 53 to point to the new CloudFront distribution.
    
### Automating static website setup with an AWS CloudFormation template
    Create bucket: These bucket names must match your domain name or subdomain name exactly.
