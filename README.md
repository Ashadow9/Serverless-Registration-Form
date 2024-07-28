# Serverless-Registration-Form

Step 1: Create DynamoDB Table
Table Name: registration-form-table
Partition key: email

Step 2: Create IAM Role for Lambda Function
IAM Role Name: RegistrationFormRole

Permissions:
1. CloudWatch Full Access
2. DynamoDB Full Access

Step 3: Create Lambda Function
Function Name: register-function
Runtime: Python 3.9

Step 4: Write Lambda Function
import json
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('registration-form-table')

def lambda_handler(event, context):
    # Get request body
    print(event)

    # Create new item in DynamoDB table
    response = table.put_item(
        Item={
            'email': event['email'],
            'name': event['name'],
            'phone': event['phone'],
            'password': event['password']
        }
    )

    # Return response
    return {
        'statusCode': 200,
        'headers': {
            'Content-Type': 'application/json',
            'Access-Control-Allow-Origin': '*'
        },
        'body': json.dumps({'message': "You've succesfully registered"})
    }


Step 5: Create API Gateway and Enable CORS and Deploy API
Enable CORS:
Access-Control-Allow-Origin: '*'
Access-Control-Allow-Headers: Content-Type,X-Amz-Date,Authorization,X-Api-Key,X-Amz-Security-Token
Access-Control-Allow-Methods: POST
Access-Control-Allow-Methods: GET

Step 6: Test the Project
