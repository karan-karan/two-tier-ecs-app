# 🚀 Two-Tier Application Deployment on AWS ECS (Fargate) with RDS

[![AWS](https://img.shields.io/badge/AWS-ECS%20%7C%20RDS-orange)]()
[![Docker](https://img.shields.io/badge/Container-Docker-blue)]()
[![Node.js](https://img.shields.io/badge/Backend-Node.js-green)]()
[![Architecture](https://img.shields.io/badge/Architecture-Two--Tier-informational)]()

---

## 📌 Project Overview

This project demonstrates the deployment of a **containerized two-tier web application** on **Amazon ECS Fargate**, integrated with **Amazon RDS (MySQL)** as the backend database.

The application is fully Dockerized, stored in **Amazon ECR**, and deployed using serverless containers on AWS.

This project highlights hands-on experience with:

- Containerization
- Cloud networking
- ECS service lifecycle
- Security group configuration
- Cloud-based database integration
- Debugging production container failures

---

## 🏗 Architecture

            ┌────────────────────┐
            │      Internet      │
            └─────────┬──────────┘
                      │
                      ▼
           ┌─────────────────────┐
           │ ECS Fargate Task    │
           │ (Node.js Container) │
           │ Port 3000           │
           └─────────┬───────────┘
                     │
                     ▼
           ┌─────────────────────┐
           │ Amazon RDS MySQL    │
           │ Database: employees │
           └─────────────────────┘

---

## 🛠 Technology Stack

| Layer | Technology |
|--------|------------|
| Backend | Node.js, Express |
| Database | MySQL (Amazon RDS) |
| Containerization | Docker |
| Container Registry | Amazon ECR |
| Orchestration | Amazon ECS (Fargate) |
| Networking | AWS VPC, Security Groups |
| Logging | CloudWatch Logs |

---

## 📂 Repository Structure
```
two-tier-ecs-app/
│
├── backend/
│ ├── db.js
│ ├── server.js
│ ├── package.json
│
├── frontend/
│ └── public/
│
├── Dockerfile
└── README.md
```

---

## ⚙️ Application Features

- Add employee (Name & Role)
- Fetch employee list
- RESTful API implementation
- Health check endpoint (`/health`)
- Automatic table creation if not exists

---

## 🔐 Environment Variables

The application uses environment variables for secure database connectivity:

| Variable | Description |
|-----------|-------------|
| DB_HOST | RDS endpoint |
| DB_USER | Database username |
| DB_PASSWORD | Database password |
| DB_NAME | Database name (`employees`) |

---

## ☁️ AWS Deployment Steps
### 1️⃣ Create RDS (MySQL)

- Engine: MySQL
- Initial database name: employees
- Security Group: Allow MySQL (3306) from ECS Security Group

### 2️⃣ Create ECS Cluster
- Launch type: Fargate
- VPC: Default VPC

### 3️⃣ Create Task Definition
- Image: ECR Image URI
- Port mapping: 3000
- Environment variables configured
- Logging enabled (CloudWatch)

### 4️⃣ Create ECS Service
- Launch type: Fargate
- Public IP: Enabled
- Load Balancer: None
- Security Group: Allow inbound TCP 3000

### 5️⃣ Access Application
```
http://<ecs-public-ip>:3000
```

---

## 🔒 Security Configuration
### ECS Security Group
- Inbound: TCP 3000 from 0.0.0.0/0
- Outbound: Allow all

### RDS Security Group
- Inbound: MySQL (3306) from ECS Security Group only
- This ensures database access is restricted to the application layer.

---
## 🧪 Troubleshooting & Debugging

During deployment, the following issues were identified and resolved:
❌ Container crash due to missing database

❌ Incorrect DB configuration

❌ Security group misconfiguration

❌ Task exit due to runtime errors

✅ Used CloudWatch logs for root cause analysis

✅ Implemented proper task redeployment


## 📈 Key DevOps Learnings

ECS task lifecycle & failure analysis

CloudWatch logging and debugging

Networking validation in VPC

Security Group referencing

Database initialization handling

Container image versioning & deployment

## 👨‍💻 Author
Karan

