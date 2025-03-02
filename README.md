# Serverless-Design
Let's start with the High Level Design. 


<img width="853" alt="Screenshot 2025-03-02 at 7 38 58 AM" src="https://github.com/user-attachments/assets/87292ff6-ac8a-4e13-9c38-7add07b44b09" />


An Amazon API Gateway is a collection of resources and methods. For this, you create one resource (DynamoDBManager) and define one method (POST) on it. The method is backed by a Lambda function (LambdaFunctionOverHttps). That is, when you call the API through an HTTPS endpoint, Amazon API Gateway invokes the Lambda function.

The POST method on the DynamoDBManager resource supports the following DynamoDB operations:

Create, update, and delete an item.
Read an item.
Scan an item.
Other operations (echo, ping), not related to DynamoDB, that you can use for testing.
The request payload you send in the POST request identifies the DynamoDB operation and provides necessary data. For example:

The following is a sample request payload for a DynamoDB create item operation:

<img width="788" alt="image" src="https://github.com/user-attachments/assets/c8b09e1e-a771-457e-8ffd-19748af06261" />

The following is a sample request payload for a DynamoDB read item operation:

<img width="786" alt="image" src="https://github.com/user-attachments/assets/7dbc059c-173d-42a8-93cc-44ccc782b364" />

Creating an Execution Role

Create Lambda IAM Role
Create the execution role that gives your function permission to access AWS resources.

## Setup
## Creating an Execution Role  

- Open the **Roles** page in the IAM console.  
- Choose **Create role**.  
- Create a role with the following properties:  
  - **Trusted entity** – Lambda  
  - **Role name** – `lambda-apigateway-role`  
  - **Permissions** – Custom policy with permission to:  
    - Read/Write data to **DynamoDB**  
    - Upload logs to **CloudWatch Logs**  






