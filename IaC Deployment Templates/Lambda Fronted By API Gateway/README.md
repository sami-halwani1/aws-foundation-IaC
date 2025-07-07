# Lambda Function with API Gateway – CloudFormation Template

This CloudFormation template provisions an AWS Lambda function fronted by a REST API using Amazon API Gateway. The function is configured with basic logging permissions and returns the received request body as a JSON response.

## What It Does

- Creates a Lambda function using Python 3.11
- Attaches a basic IAM role with CloudWatch logging permissions
- Sets up an API Gateway REST API with a `/hello` endpoint
- Configures an HTTP POST method to proxy requests to the Lambda function
- Outputs the fully qualified API endpoint URL after deployment

## Tech Stack

- AWS Lambda
- Amazon API Gateway (REST API)
- IAM (Execution Role and Invoke Permissions)
- Python 3.11
- CloudFormation (YAML)

## Parameters

| Name           | Type   | Default         | Description                              |
|----------------|--------|-----------------|------------------------------------------|
| `FunctionName` | String | `MyLambdaFunction` | Name to assign to the deployed Lambda function |


## Example Response
```json
{
  "statusCode": 200,
  "headers": {
    "Content-Type": "application/json"
  },
  "body": "{...your original request body...}"
}
```

## Notes
- The Lambda function uses an inline ZipFile definition with a basic handler in Python.
- The endpoint only supports the POST method at /hello.
- Logging is enabled via CloudWatch Logs permissions on the IAM role.
- You must manually test the endpoint using tools like Postman, curl, or Invoke-RestMethod.

# Output
| Name          | Description                               |
| ------------- | ----------------------------------------- |
| `ApiEndpoint` | The URL of the deployed REST API endpoint |
