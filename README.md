# Serverless Student Management Application (AWS)

**Name:** NANNA ABHIRAM
**Roll No:** 2410080032
**Experiment 11:** Develop and Deploy a Serverless Student Management Application

## Overview
A serverless REST API that supports Add, Retrieve, Update and Delete (CRUD) operations on student records, built with Amazon DynamoDB, AWS Lambda (Python) and Amazon API Gateway.

## Architecture
```
Client (Postman) → API Gateway (prod) → AWS Lambda (StudentFunction) → DynamoDB (StudentDB)
```

## AWS Services Used
| Service | Purpose |
|---|---|
| Amazon DynamoDB | Table `StudentDB`, partition key `StudentID` (String) |
| AWS Lambda (Python 3.12) | `StudentFunction`, which holds the CRUD logic |
| AWS IAM | Execution role with `AmazonDynamoDBFullAccess` |
| Amazon API Gateway (REST) | `StudentAPI`, deployed to stage `prod` |
| Postman | API testing |

Region: `us-east-1` (N. Virginia)

## API Endpoints
| Method | Endpoint | Operation |
|---|---|---|
| POST | `/students` | Add a student |
| GET | `/students/{id}` | Retrieve a student by ID |
| PUT | `/students/{id}` | Update a student |
| DELETE | `/students/{id}` | Delete a student |

All methods use **Lambda proxy integration**.

## Sample Requests
**POST /students**
```json
{
  "StudentID": "101",
  "Name": "Abhiram",
  "Department": "AIDS",
  "Year": "2"
}
```

**PUT /students/101**
```json
{
  "Name": "Nanna Abhiram",
  "Year": "3"
}
```

## Responses
| Operation | Status | Message |
|---|---|---|
| POST | 201 | Student added |
| GET | 200 | Student details |
| PUT | 200 | Student updated |
| DELETE | 200 | Student 101 deleted |
| Not found | 404 | Student not found |

## Steps Performed
1. Created the DynamoDB table `StudentDB` with `StudentID` as the partition key.
2. Created the Lambda function `StudentFunction` (Python 3.12).
3. Implemented the Add, Retrieve, Update and Delete operations.
4. Attached `AmazonDynamoDBFullAccess` to the Lambda execution role.
5. Created the REST API `StudentAPI` in API Gateway.
6. Created the resources `/students` and `/students/{id}`.
7. Integrated POST, GET, PUT and DELETE with the Lambda function (proxy integration).
8. Deployed the API to the stage `prod`.
9. Tested all four operations with Postman.
10. Verified the changes in DynamoDB (Explore items → Scan).

## Issue Faced
PUT first returned `"Unsupported route"` because Lambda proxy integration was off for that method. I recreated it with proxy integration ON and redeployed the API.

## Demo Video
YouTube: <paste your video link here>

## Files
- `lambda_function.py`: Lambda source code
