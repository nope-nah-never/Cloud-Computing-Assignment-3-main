# Cloud-Computing-Assignment-3

Perfect — below is a **clean, polished RELEASE section** written exactly in a format meant for **README.md**.
You can copy-paste this directly into your project’s README file.

It is concise, professional, GitHub-ready, and contains all the key deliverables of the final assignment.

---

# **Release – Smart Photo Album (CS-GY 9223 Assignment 3)**

This release contains the complete implementation of the **Smart Photo Album** project, including backend Lambdas, API Gateway integration, OpenSearch indexing, Rekognition-based labeling, Lex keyword extraction, S3 static frontend hosting, CloudFormation stack deployment, and CI/CD automation.

---

## **Project Overview**

The Smart Photo Album allows users to:

* Upload photos via a web interface
* Automatically extract labels using **Amazon Rekognition**
* Store metadata and labels in **OpenSearch Serverless (AOSS)**
* Search for photos using natural language keywords interpreted by **Amazon Lex V2**
* Retrieve matching photos through **presigned URLs**
* Access the entire system through **API Gateway (REST)**
* Interact using a **fully deployed S3-hosted frontend**

The architecture is fully deployed and managed using **AWS CloudFormation** and **CodePipeline**.

---

## **Architecture Summary**

**AWS Services Used**

| Category | Services                                          |
| -------- | ------------------------------------------------- |
| Compute  | AWS Lambda                                        |
| Storage  | S3 (image bucket + static frontend bucket)        |
| AI/ML    | Rekognition (labels), Lex V2 (keyword extraction) |
| Search   | OpenSearch Serverless                             |
| API      | API Gateway REST API                              |
| IAM      | Execution roles, resource policies                |
| DevOps   | CodeBuild + CodePipeline                          |
| IaC      | CloudFormation                                    |

**Pipeline Overview**

* **Backend Pipeline:**
  GitHub → CodeBuild → Upload zipped Lambdas → Deploy to Lambda
* **Frontend Pipeline:**
  GitHub → CodeBuild → `aws s3 sync` → S3 Website Bucket

---

## 🧩 **Lambda Functions**

### **1 index-photos (PUT /upload)**

* Accepts image + optional custom labels
* Uploads file to S3
* Extracts automatic labels via Rekognition
* Stores metadata in OpenSearch
* Returns success JSON

**Handler:** `LF1.lambda_handler`

---

### **2 search-photos (GET /search?q=...)**

* Sends query to Lex for keyword extraction
* Falls back to raw text if Lex finds no slots
* Searches OpenSearch for matching images
* Generates presigned URLs
* Returns list of `{url, labels}`

**Handler:** `lambda_function.lambda_handler`

---

## **REST API Endpoints**

### **`PUT /upload`**

Accepts binary image file + optional header:

```
x-amz-meta-customLabels: Sam, birthday, beach
```

### **`GET /search?q=cat`**

Returns:

```json
{
  "results": [
    { "url": "<presigned-url>", "labels": ["cat", "animal"] }
  ]
}
```

---

## **Frontend (S3 Website)**

Frontend includes:

* `index.html` – Search & upload interface
* `style.css` – Styled card-based UI
* `app.js` – Integrates with API using the generated SDK
* `/sdk/` – API Gateway JS client (auto-generated)

Features:

* Search bar with live result grid
* Upload form with custom labels
* Styled error/success messages
* Responsive grid layout

---

## 📁 **Repository Structure**

```
Cloud-Computing-Assignment-3-main/
│
├── photos-backend/
│   ├── index-photos/
│   ├── search-photos/
│   ├── buildspec.yml           #buildspec file for pipeline functioning
│   ├── requirements.txt
│
├── photos-frontend/
│   ├── index.html
│   ├── style.css
│   ├── app.js
│   ├── sdk/                    #generated API Gateway client
│   └── buildspec.yml           #buildspec file for pipeline functioning
│
└── cloudformation/
    ├── template.yml            #cloudformation source template file
```

---

## 🚀 **Deployment Summary**

✔ CloudFormation stack created successfully
✔ API Gateway with Lambda Proxy Integration
✔ Two Lambda functions deployed
✔ S3 buckets provisioned
✔ Bucket public access configured correctly
✔ OpenSearch Serverless index & policy configured
✔ Lex bot variables used through Env Vars
✔ CI/CD pipelines (backend + frontend) fully operational
✔ Frontend auto-deploys to S3 on every commit
✔ Entire system tested end-to-end

---

## 🧪 **Test Scenarios Completed**

### Upload Path

* JPEG upload ✔
* PNG upload ✔
* Custom labels ✔
* Rekognition auto-labeling ✔
* OpenSearch indexing ✔

### Search Path

* Lex extracts slots ✔
* Fallback to raw search ✔
* Deduplication ✔
* Presigned URL generation ✔
* Correct display in grid ✔

### Frontend

* Search errors displayed
* Upload errors displayed
* S3 website loads all assets
* SDK loads without errors

---

## 🏁 **Final Status**

**All functional requirements, architectural requirements, and deployment requirements have been fully implemented.**

This release represents a complete, production-ready implementation of **Smart Photo Album** for the assignment.

---
