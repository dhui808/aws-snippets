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
    
    Create bucket: These bucket names must match your domain name or subdomain name exactly.
    
    Step 11: Add alias records for your domain and subdomain
    
### Speeding up your website with Amazon CloudFront
    
    https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-to-cloudfront-distribution.html
    
    Step 1: Create a CloudFront distribution
        Need to specify Default root object - optional. If not psecified, the user has to enter the file name  
        for the root object (index.html).
        404 error from the origin (and potentially other non-200 statuses, are not supported?)
    Step 2: Update the alias record in Route 53 to point to the new CloudFront distribution.
        Under Records, select the A record that you created for your subdomain.
        Under Record details, choose Edit record.
        Under Route traffic to, choose Alias to CloudFront distribution.
        Under Choose distribution, choose the CloudFront distribution.
            Does not work. 
            The distribution must include an alternate domain name that matches the domain name that you want 
            to use for your URLs instead of the domain name that CloudFront assigned to your distribution.
            Also CloudFront needs a SSL cert for this domain name.
        Choose Save.
        
### Automating static website setup with an AWS CloudFormation template
    Deploying the solution
        Use the AWS CloudFormation console to deploy the solution with default content, then upload your website content 
            to Amazon S3.
        Clone the solution to your computer to add your website content. Then, deploy the solution with the AWS CLI.

    Samples:
        https://s3.amazonaws.com/solution-builders-us-east-1/amazon-cloudfront-secure-static-site/latest/main.yaml
        
