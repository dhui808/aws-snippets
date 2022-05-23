### Deploying a Hello World application
    use Python 3.9 and Windows Command Prompt, not Weindows Terminal
    Step 1: Download a sample AWS SAM application
        sam init
        choose AWS Quick Start Templates, the Zip package type
    Step 2: Build your application
        sam build
        aws configure --profile sam-user
        setx AWS_PROFILE sam-user
    Step 3: Deploy your application to the AWS Cloud
        sam deploy --guided
    Test:
        https://91zg07safk.execute-api.us-east-1.amazonaws.com/Prod/hello
        
    Resources created:
        IAM Role
        ApiGateway
        Lambda
        S3
        ClounFormation Stack
    
    When deleting CloudFormation, have to manually empty and delete the sam cli managed s3 bucket and CloudFormation
    
### Process DynamoDB events
    sam init  --location gh:aws-samples/cookiecutter-aws-sam-dynamodb-python  --no-input
    Step 3: Package the application
        
        aws s3 mb s3://my-dynamodb-event-bucket
        sam package --template-file template.yaml --output-template-file packaged.yaml --s3-bucket my-dynamodb-event-bucket
        
