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

<img width="765" alt="Screenshot 2025-03-02 at 8 23 41 AM" src="https://github.com/user-attachments/assets/3103916f-caf3-43c1-ae62-b135f34b8cc7" />

## Create Lambda Function
## To create the function

## 1.Click "Create function" in AWS Lambda Console
  ![image](https://github.com/user-attachments/assets/5cfca87a-fd6e-4e2b-89e7-32b679a7a5ff)
## 2.Select "Author from scratch". Use name LambdaFunctionOverHttps , select Python 3.7 as Runtime. Under Permissions, select "Use an existing role", and select lambda-apigateway-role that we created, from the drop down
## 3.Click "Create function"
![image](https://github.com/user-attachments/assets/8b61f45d-711f-4e12-a666-06813383087d)
## 4.Replace the boilerplate coding with the following code snippet and click "Save"
## Example Python Code
![Screenshot 2025-03-02 at 10 40 07 AM](https://github.com/user-attachments/assets/082aab98-4881-44a3-adb1-1f301e1409d1)
![image](https://github.com/user-attachments/assets/1f223641-b9cb-47ef-87d7-9a235b0d4e4c)

## Test Lambda Function
Let's test our newly created function. We haven't created DynamoDB and the API yet, so we'll do a sample echo operation. The function should output whatever input we pass.

1. Click the arrow on "Select a test event" and click "Configure test events"
   ![image](https://github.com/user-attachments/assets/4e6f2fd6-57ee-4ad0-941a-3f5a0b9e86e8)

2. Paste the following JSON into the event. The field "operation" dictates what the lambda function will perform. In this case, it'd simply return the payload from input event as output. Click "Create" to save
![image](https://github.com/user-attachments/assets/7f9d1ee5-4a5e-4a2f-b95e-448fe294d267)
![image](https://github.com/user-attachments/assets/a00825ec-dc59-451d-b14b-93fea59163db)

3. Click "Test", and it will execute the test event. You should see the output in the console
![image](https://github.com/user-attachments/assets/cb84f4a6-a584-4f66-a039-f17b99e50b8d)

We're all set to create DynamoDB table and an API using our lambda as backend!
## Create DynamoDB Table  
Create a DynamoDB table that the Lambda function uses.  

### To create a DynamoDB table  

- Open the **DynamoDB** console.  
- Choose **Create table**.  
- Create a table with the following settings:  
  - **Table name** – `lambda-apigateway`  
  - **Primary key** – `id` (String)  
- Choose **Create**.  

![image](https://github.com/user-attachments/assets/dec4d04e-a625-4128-9d7a-7d85878a8149)

## Create API  
Create an API using API Gateway.  

### To create the API  

- Go to the **API Gateway** console.  
- Click **Create API**.
  ![image](https://github.com/user-attachments/assets/802c2211-ec93-47c0-9aff-5a2002a2f5d4)
- Click **Scroll down and select "Build" for REST API**.
  ![image](https://github.com/user-attachments/assets/d053a4af-6670-49f4-9c27-55d87d71b9ae)

- Click **Give the API name as "DynamoDBOperations", keep everything as is, click "Create API"**.
  ![image](https://github.com/user-attachments/assets/60342c9f-5f0b-4c1f-b127-2e6e9bbd8297)

  



      















