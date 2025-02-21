AWS Lambda Claims API

Overview

This AWS Lambda function retrieves customer claim details from a DynamoDB table named Claims. It takes a customer_id as input and returns the total claim cover used by the customer.

Prerequisites

Ensure you have the following before deploying the function:

An AWS account with permissions to create and invoke Lambda functions.

A DynamoDB table named Claims with a primary key customer_id.

The AWS SDK for Python (boto3).

Dependencies

This function uses the following libraries:

boto3: AWS SDK for Python

json: For handling JSON data

decimal: To handle Decimal type returned by DynamoDB

Installation

Install dependencies:

pip install boto3

Deploy the Lambda function using AWS CLI or AWS Console.

Usage

The Lambda function expects an event input containing customer_id. It performs the following actions:

Checks if customer_id is provided, otherwise returns a 400 Bad Request.

Queries the DynamoDB Claims table for the given customer_id.

If no record is found, returns a 404 Not Found response.

If found, retrieves fixed_cover and used_cover values.

Returns a JSON response with total claim coverage.

Example Request

{
  "customer_id": "12345"
}

Example Response

{
  "customer_id": "12345",
  "total_cover": "$5000/$10000"
}

Error Handling

400 Bad Request: If customer_id is missing.

404 Not Found: If the customer does not exist in the database.

Deployment

To deploy the Lambda function, package it into a ZIP file and upload it to AWS Lambda:

zip function.zip lambda_function.py
aws lambda update-function-code --function-name MyLambdaFunction --zip-file fileb://function.zip

Notes

Ensure the Lambda function has the necessary IAM permissions to access DynamoDB (dynamodb:GetItem).

Modify the DynamoDB table name in the script if necessary.

Author

Sanjay Chauhan
