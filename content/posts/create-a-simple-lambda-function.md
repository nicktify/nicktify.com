+++
title = 'Create a Simple Lambda Function'
date = 2024-02-25T00:17:23-03:00
draft = false
+++

### Create a Lambda Function


```python
import json
import boto3

def lambda_handler(event, context):
    # TODO implement
    return {
        'statusCode': 200,
        'body': json.dumps('Hello from Lambda!')
    }
```

### Create the template.yaml for SAM

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: An AWS Serverless Application that uses the AWS SDK for Python (Boto3) to list the current regions.

Resources:
  MyLambdaFunction:
    Type: AWS::Serverless::Function
    Properties:
      Handler: index.lambda_handler
      Runtime: python3.8
      Policies: AmazonEC2ReadOnlyAccess
      Events:
        MyApi:
          Type: Api
          Properties:
            Path: /hello
            Method: get
```

### Deploy the application

```bash
sam deploy --guided
```



