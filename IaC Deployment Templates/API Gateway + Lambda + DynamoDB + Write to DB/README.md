# Lambda to DynamoDB via API Gateway – CloudFormation Template

This CloudFormation template provisions a complete serverless backend that allows external HTTP clients to write data to a DynamoDB table via an AWS Lambda function. The function is exposed through an API Gateway POST endpoint and writes data directly to a DynamoDB table using the AWS SDK.

## What It Does

- Creates a DynamoDB table with a simple `id` primary key
- Deploys a Python-based AWS Lambda function that accepts POST data and writes it to DynamoDB
- Sets up an API Gateway REST endpoint at `/write` to trigger the Lambda
- Provides IAM permissions for logging and DynamoDB access
- Outputs the public API endpoint and resource names

## Tech Stack

- AWS Lambda (Python 3.11)
- Amazon DynamoDB (PAY_PER_REQUEST mode)
- Amazon API Gateway (REST API)
- AWS IAM
- AWS CloudFormation (YAML)

## Parameters

| Name            | Type   | Default                           | Description                                 |
|------------------|--------|-----------------------------------|---------------------------------------------|
| `FunctionName`   | String | `foundation-lambda-writeto-dynamodb` | Name for the Lambda function               |
| `TableName`      | String | `LambdaDynamoDBTable`             | Name for the DynamoDB table                |
| `ApiName`        | String | `FoundationApiGateway-WriteToDynamoDB` | Name for the API Gateway resource     |

## Lambda Behavior

The Lambda function:
- Parses JSON data from the request body
- Expects an object with at least an `id` field and optionally a `data` field
- Inserts the record into the DynamoDB table

## Example Request

```powershell
Invoke-RestMethod `
>>   -Uri "<YourApiEndPoint>/prod/write" `
>>   -Method POST `
>>   -Body '{"id": "0000", "data": "Hello, World!"}' `
>>   -ContentType "application/json"
```

## OutPuts
| Output Name          | Description                            |
| -------------------- | -------------------------------------- |
| `ApiEndpoint`        | POST URL to invoke the Lambda function |
| `DynamoDBTableName`  | Name of the DynamoDB table             |
| `LambdaFunctionName` | Name of the deployed Lambda function   |


## Notes
- DynamoDB is created with on-demand billing mode for cost efficiency.
- The Lambda environment variable TABLE_NAME is automatically injected via CloudFormation.
- IAM permissions are scoped directly to the created DynamoDB table.
- You must handle any required validation or transformation in the Lambda logic as needed.

## Security Considerations
- API Gateway is configured with no authorization for demo/testing purposes. For production, integrate IAM, API keys, or JWT auth.
- Data is not encrypted client-side or validated for structure. Input sanitization and schema enforcement should be added based on the use case.