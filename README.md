# Direct Edge MQTT Ingestion to AWS RDS (PostgreSQL)

This project demonstrates a **secure, production-grade pipeline** for ingesting MQTT telemetry data from edge devices and storing it in **AWS RDS (PostgreSQL)** using managed AWS services.

The architecture follows AWS best practices: **private networking, no direct database exposure, and service-to-service communication**.

---

## High-Level Architecture

**Data Flow**

Edge Device / MQTTX  
→ AWS IoT Core  
→ IoT Rule  
→ AWS Lambda (Parse & Transform)  
→ Amazon RDS (PostgreSQL)

The database is deployed in a **private subnet** and is **never exposed to the public internet**.

---

## Core Components

### AWS IoT Core
- Receives MQTT messages from edge devices
- Uses certificates for secure authentication
- Routes messages using IoT Rules

### AWS Lambda
- Triggered by IoT Rules (service invocation)
- Parses and validates incoming MQTT payloads
- Runs inside a VPC with a private IP
- Initiates outbound connections to the database

### Amazon RDS (PostgreSQL)
- Deployed in private subnets
- Listens on TCP port 5432
- Accepts connections **only from Lambda Security Group**
- Stores telemetry data in structured tables

### VPC & Security Groups
- Lambda and RDS run inside the same VPC
- Lambda Security Group allows outbound traffic
- RDS Security Group allows inbound PostgreSQL traffic **only from Lambda**
- No public access to the database

---

## Connection Models Explained

### MQTTX → RDS (Production Path)
- MQTTX connects **only to AWS IoT Core**
- IoT Core invokes Lambda
- Lambda writes data to RDS
- MQTTX never connects to the database directly

### Laptop → RDS (Debug Path)
- Direct laptop access is blocked
- RDS has no public IP and lives in a private subnet
- This ensures database security and compliance

---

## Security Principles

- No inbound access to Lambda
- No public access to RDS
- Least-privilege Security Group rules
- Private subnet isolation
- Stateful firewall behavior via Security Groups

---

## Why This Architecture

- Scales to thousands of devices
- Follows AWS Well-Architected Framework
- Prevents accidental database exposure
- Suitable for production IoT workloads

---

## Use Cases

- IoT telemetry ingestion
- Edge-to-cloud data pipelines
- Secure industrial monitoring systems
- Time-series data storage

---

## Notes

This repository focuses on **architecture clarity and secure data flow**, not UI or visualization.  
Dashboards, analytics, and scaling strategies can be layered on top of this foundation.

---

## Author

**Sony Sunny**  
Embedded Systems | Cloud | IoT Architecture
