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
    Step 4: Deploy the application
        sam deploy --template-file packaged.yaml --stack-name sam-dynamodb-app --capabilities CAPABILITY_IAM --region us-east-1
        The --capabilities parameter allows AWS CloudFormation to create an IAM role.
    To test the serverless application in the AWS Cloud, Insert a record into the table that you just created.
        Go to the Metrics tab of the table, and choose View all CloudWatch metrics. 
        In the CloudWatch console, choose Logs to be able to view the log output.
        
### Build a Serverless Web Application
    aws.amazon.com/getting-started/hands-on/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/
    aw configure
    Create Git Repository "wildrydes-site"
    Populate Git repo
        cd wildrydes-site
        aws s3 cp s3://wildrydes-us-east-1/WebApplication/1_StaticWebHosting/website ./ --recursive
    Enable web hosting with AWS Amplify Console
    
    User Management
    Create Cognito User Pool: WildRydes
        Pool Id us-east-1_8YflySxfd
    Create app client "WildRydesWebApp" and add it to the user pool
        App client id: 2q17qvf55mbal7uvlgbp81cs0h
    Update the website config
        userPoolId
        userPoolClientId
        region
    Validate the config changes:
        Visit /register.html 
        Register email
        Verify email
        Sign in
        Also needs ArcGIS account
    
    Serverless Service Backend
    Create a new DynamoDB table: Rides
        Partition key: RideId
    Create an IAM role for the Lambda function: WildRydesLambda
        grants your Lambda function permission to write logs to Amazon CloudWatch Logs 
        and access to write items to your DynamoDB table.
        policy:AWSLambdaBasicExecutionRole
        Create inline policy: DynamoDBWriteAccess
            Choose a service: DynamoDB
            add actions: PutItem
            Resources: Add ARN
    Create a Lambda for Handling Requests: RequestUnicorn, use the WildRydesLambda IAM role
    Validate the Lambda function
        Test -> Configure test event -> TestRequestEvent
        Copy and paste the sample test event into the editor
        Test
    
    Deploy a RESTful API
    Create a New REST API from API Gateway: WildRydes
        Edge optimized selected in the Endpoint Type
    Create a Cognito User Pools Authorizer: WildRydes
        API: WildRydes -> Authorizers -> Create New Authorizer
        Type: Cognito
        Cognito User Pool: WildRydes
        Authorization for the Token Source
        Verify your authorizer configuration
    Create a new resource and method
        Create called a new resource /ride within your API. 
        Then create a POST method for that resource and configure it to use a Lambda proxy integration 
        backed by the RequestUnicorn function
        Select Lambda Function for the integration type
        Check the box for Use Lambda Proxy integration
        RequestUnicorn, for Lambda Function
        o. Choose on the Method Request card.
        p. Choose the pencil icon next to Authorization.
        q. Select the WildRydes Cognito user pool authorizer from the drop-down list, and click the checkmark icon.
    Deploy Your API
        From the Amazon API Gateway console, choose Actions, Deploy API
        Invoke URL becomes available
        Invoke URL: https://zr46gluakl.execute-api.us-east-1.amazonaws.com/prod
    Update the Website Config
        invokeUrl
    Validate the Implementation
        Visit /ride.html
        However, why ArGIS pops up?
        
