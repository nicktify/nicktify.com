+++
title = 'Create a Simple State Machine'
date = 2024-02-25T00:25:57-03:00
draft = false
+++


### Create a Simple State Machine

```json
{
  "Comment": "A simple AWS Step Functions state machine that automates a task",
  "StartAt": "HelloWorld",
  "States": {
    "HelloWorld": {
      "Type": "Pass",
      "Result": "Hello, World!",
      "End": true
    }
  }
}
```

### Create the template.yaml for SAM

```yaml
AWSTemplateFormatVersion: '2010-09-09'
Transform: AWS::Serverless-2016-10-31
Description: An AWS Serverless Application that uses the AWS SDK for Python (Boto3) to list the current regions.

Resources:
  MyStateMachine:
    Type: AWS::Serverless::StateMachine
    Properties:
      DefinitionString: |
        {
          "Comment": "A simple AWS Step Functions state machine that automates a task",
          "StartAt": "HelloWorld",
          "States": {
            "HelloWorld": {
              "Type": "Pass",
              "Result": "Hello, World!",
              "End": true
            }
          }
        }
      Role: !GetAtt MyStateMachineRole.Arn
  MyStateMachineRole:
    Type: AWS::IAM::Role
    Properties:
      AssumeRolePolicyDocument:
        Version: '2012-10-17'
        Statement:
          - Effect: Allow
            Principal:
              Service: states.amazonaws.com
            Action: sts:AssumeRole
      Policies:
        - PolicyName: MyStateMachinePolicy
          PolicyDocument:
            Version: '2012-10-17'
            Statement:
              - Effect: Allow
                Action:
                  - logs:CreateLogGroup
                  - logs:CreateLogStream
                  - logs:PutLogEvents
                Resource: arn:aws:logs:*:*:*
```

