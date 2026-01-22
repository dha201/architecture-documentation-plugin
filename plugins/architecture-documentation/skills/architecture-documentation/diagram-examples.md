# Eraser Diagram Examples

Real-world diagram examples demonstrating Eraser's diagram-as-code syntax.

**Official Examples:** https://docs.eraser.io/docs/examples

## Example 1: AWS Three-Tier Web Application

```
direction right
colorMode bold

// External users
Users [icon: users, label: "Web Users"]

// AWS Infrastructure
AWS Cloud [icon: aws-cloud] {

  VPC [icon: aws-vpc, label: "Production VPC"] {

    // Web Tier (Public)
    Public Subnet [icon: aws-public-subnet, color: green] {
      ALB [icon: aws-elb, label: "Application Load Balancer"]
      NAT Gateway [icon: aws-nat-gateway]
    }

    // App Tier (Private)
    Private Subnet [icon: aws-private-subnet, color: blue] {
      Web Server 1 [icon: aws-ec2, label: "EC2 (Web)"]
      Web Server 2 [icon: aws-ec2, label: "EC2 (Web)"]

      App Server 1 [icon: aws-lambda, label: "Lambda (API)"]
      App Server 2 [icon: aws-lambda, label: "Lambda (API)"]

      Cache [icon: aws-elasticache, shape: cylinder]
    }

    // Data Tier (Private)
    Database Subnet [icon: aws-private-subnet, color: red] {
      Primary DB [icon: aws-rds, label: "RDS Primary"]
      Replica DB [icon: aws-rds, label: "RDS Replica"]
    }
  }

  // Static assets
  S3 [icon: aws-s3, label: "Static Assets"]
  CloudFront [icon: aws-cloudfront, label: "CDN"]
}

// Connection flows
Users > CloudFront: HTTPS
CloudFront > S3: Static Files
CloudFront > ALB: API Requests

ALB > Web Server 1, Web Server 2: Distribute Load

Web Server 1, Web Server 2 > App Server 1, App Server 2: Process

App Server 1, App Server 2 > Cache: Cache Lookup
App Server 1, App Server 2 > Primary DB: Read/Write
Primary DB > Replica DB: Replicate
```

**Use case:** Standard web application with load balancing, caching, and database replication.

---

## Example 2: Microservices Architecture

```
direction down
styleMode shadow

// API Gateway
API Gateway [icon: aws-api-gateway, color: purple]

// Microservices
Services [color: blue] {
  User Service [icon: docker, label: "User Service\n(Node.js)"]
  Order Service [icon: docker, label: "Order Service\n(Java)"]
  Payment Service [icon: docker, label: "Payment Service\n(Python)"]
  Notification Service [icon: docker, label: "Notification Service\n(Go)"]
}

// Databases per service
Databases [color: green] {
  User DB [icon: postgres, shape: cylinder, label: "PostgreSQL"]
  Order DB [icon: mongodb, shape: cylinder, label: "MongoDB"]
  Payment DB [icon: mysql, shape: cylinder, label: "MySQL"]
}

// Message Queue
Message Bus [icon: kafka, shape: queue, label: "Kafka Event Bus"]

// Service Registry
Service Registry [icon: kubernetes, label: "Kubernetes"]

// Connections
API Gateway > User Service, Order Service, Payment Service: REST

User Service > User DB
Order Service > Order DB
Payment Service > Payment DB

Order Service > Message Bus: Publish OrderCreated
Payment Service < Message Bus: Subscribe
Notification Service < Message Bus: Subscribe

Service Registry > User Service, Order Service, Payment Service, Notification Service: Service Discovery
```

**Use case:** Event-driven microservices with database-per-service pattern.

---

## Example 3: Data ETL Pipeline

```
direction right
colorMode pastel

// Data Sources
Sources [color: blue, label: "Data Sources"] {
  Oracle DB [icon: oracle, label: "Oracle\nTransactional DB"]
  REST API [icon: rest-api, label: "External API"]
  CSV Files [icon: csv, label: "CSV Uploads"]
}

// Ingestion Layer
Ingestion [color: green, label: "Data Ingestion"] {
  Kafka [icon: kafka, shape: queue, label: "Kafka Streams"]
  S3 Raw [icon: aws-s3, label: "S3 Raw Zone"]
}

// Processing Layer
Processing [color: orange, label: "Data Processing"] {
  Spark [icon: spark, label: "Spark ETL"]
  Databricks [icon: databricks, label: "Databricks\nTransform"]
  S3 Processed [icon: aws-s3, label: "S3 Processed"]
}

// Analytics Layer
Analytics [color: purple, label: "Analytics & BI"] {
  Snowflake [icon: snowflake, shape: cylinder, label: "Snowflake\nData Warehouse"]
  Tableau [icon: tableau, label: "Tableau\nDashboards"]
}

// Machine Learning
ML [color: red, label: "ML Pipeline"] {
  SageMaker [icon: aws-sagemaker, label: "SageMaker\nTraining"]
  Model Registry [icon: database, shape: cylinder]
}

// Connections
Oracle DB, REST API, CSV Files > Kafka: Stream Data
Kafka > S3 Raw: Land Data

S3 Raw > Spark: Batch Processing
Spark > Databricks: Transform
Databricks > S3 Processed: Clean Data

S3 Processed > Snowflake: Load
Snowflake > Tableau: Visualize
Snowflake > SageMaker: ML Features
SageMaker > Model Registry: Store Models
```

**Use case:** Modern data platform with streaming ingestion, batch processing, and analytics.

---

## Example 4: Kubernetes Cluster Architecture

```
direction down

// Control Plane
Control Plane [icon: kubernetes, color: blue, label: "Kubernetes Control Plane"] {
  API Server [icon: k8s-service, label: "API Server"]
  Scheduler [icon: k8s-deployment, label: "Scheduler"]
  Controller Manager [icon: k8s-deployment, label: "Controller Manager"]
  etcd [icon: database, shape: cylinder, label: "etcd (State)"]
}

// Worker Nodes
Worker Nodes [color: green] {

  Node 1 [icon: k8s-node, label: "Worker Node 1"] {
    Kubelet 1 [icon: k8s-pod]
    Pods 1 [icon: k8s-pod, label: "Application Pods"]
  }

  Node 2 [icon: k8s-node, label: "Worker Node 2"] {
    Kubelet 2 [icon: k8s-pod]
    Pods 2 [icon: k8s-pod, label: "Application Pods"]
  }

  Node 3 [icon: k8s-node, label: "Worker Node 3"] {
    Kubelet 3 [icon: k8s-pod]
    Pods 3 [icon: k8s-pod, label: "Application Pods"]
  }
}

// External Components
Ingress Controller [icon: k8s-ingress, label: "Nginx Ingress"]
Persistent Storage [icon: k8s-persistent-volume, shape: cylinder]

// Cloud Providers
Cloud Providers [color: orange] {
  AWS [icon: aws-cloud]
  Azure [icon: azure-cloud]
  GCP [icon: gcp-cloud]
}

// Connections
API Server > etcd: Store State
API Server > Scheduler, Controller Manager
Scheduler > API Server: Watch Pods
Controller Manager > API Server: Reconcile

Kubelet 1, Kubelet 2, Kubelet 3 > API Server: Report Status
API Server > Kubelet 1, Kubelet 2, Kubelet 3: Deploy Pods

Ingress Controller > Pods 1, Pods 2, Pods 3: Route Traffic
Pods 1, Pods 2, Pods 3 > Persistent Storage: Read/Write

Cloud Providers > Worker Nodes: Provision Infrastructure
```

**Use case:** Complete Kubernetes cluster showing control plane, workers, and cloud integration.

---

## Example 5: Serverless Event-Driven Architecture

```
direction right
colorMode bold

// Event Sources
Sources [color: blue, label: "Event Sources"] {
  S3 Upload [icon: aws-s3, label: "S3 Bucket"]
  API Gateway [icon: aws-api-gateway, label: "API Gateway"]
  Schedule [icon: clock, label: "CloudWatch Events"]
  DynamoDB Stream [icon: aws-dynamodb, label: "DynamoDB Stream"]
}

// Event Bus
Event Bus [icon: aws-eventbridge, shape: queue, label: "EventBridge"]

// Lambda Functions
Functions [color: green, label: "Lambda Functions"] {
  Image Processor [icon: aws-lambda, label: "Image\nProcessor"]
  Data Validator [icon: aws-lambda, label: "Data\nValidator"]
  Report Generator [icon: aws-lambda, label: "Report\nGenerator"]
  Email Sender [icon: aws-lambda, label: "Email\nSender"]
}

// Storage & Databases
Storage [color: orange] {
  Images [icon: aws-s3, label: "Processed\nImages"]
  Database [icon: aws-dynamodb, shape: cylinder, label: "DynamoDB"]
  Archive [icon: aws-glacier, shape: cylinder, label: "Glacier\nArchive"]
}

// Notification
Notification [icon: aws-sns, label: "SNS Topic"]

// Connections
S3 Upload > Event Bus: File Uploaded
API Gateway > Event Bus: API Request
Schedule > Event Bus: Scheduled Event
DynamoDB Stream > Event Bus: Data Changed

Event Bus > Image Processor: Process Image
Event Bus > Data Validator: Validate Data
Event Bus > Report Generator: Generate Report

Image Processor > Images: Save
Data Validator > Database: Store
Report Generator > Archive: Archive Report

Image Processor, Data Validator, Report Generator > Notification: Success
Notification > Email Sender: Send Email
```

**Use case:** Fully serverless architecture with event-driven processing.

---

## Example 6: Multi-Region High Availability

```
direction down

// Global Load Balancer
Global LB [icon: aws-route-53, label: "Route 53\nGeoDNS"]

// Primary Region
Region US East [icon: aws-region, color: green, label: "us-east-1 (Primary)"] {
  VPC East [icon: aws-vpc] {
    ALB East [icon: aws-elb]
    Servers East [icon: aws-ec2, label: "EC2 Auto Scaling"]
    RDS East [icon: aws-rds, label: "RDS Primary"]
  }
  S3 East [icon: aws-s3, label: "S3 Bucket"]
}

// Secondary Region
Region US West [icon: aws-region, color: orange, label: "us-west-2 (DR)"] {
  VPC West [icon: aws-vpc] {
    ALB West [icon: aws-elb]
    Servers West [icon: aws-ec2, label: "EC2 Auto Scaling"]
    RDS West [icon: aws-rds, label: "RDS Read Replica"]
  }
  S3 West [icon: aws-s3, label: "S3 Bucket (Replica)"]
}

// Connections
Global LB > ALB East, ALB West: Route Traffic
ALB East > Servers East
ALB West > Servers West
Servers East > RDS East
Servers West > RDS West
Servers East, Servers West > S3 East, S3 West

RDS East > RDS West: Cross-Region Replication
S3 East > S3 West: Cross-Region Replication
```

**Use case:** Active-passive multi-region setup with disaster recovery.

---

## Example 7: CI/CD Pipeline

```
direction right

// Source Control
Source [icon: github, label: "GitHub\nRepository"]

// CI/CD Pipeline
Pipeline [color: blue, label: "CI/CD Pipeline"] {
  Build [icon: jenkins, label: "Jenkins\nBuild"]
  Test [icon: pytest, label: "Automated\nTests"]
  Security Scan [icon: security, label: "Security\nScan"]
  Package [icon: docker, label: "Docker\nBuild"]
}

// Artifact Storage
Registry [icon: docker, shape: cylinder, label: "Container\nRegistry"]

// Deployment Stages
Environments [color: green, label: "Deployment Stages"] {
  Dev [icon: kubernetes, label: "Dev\nCluster"]
  Staging [icon: kubernetes, label: "Staging\nCluster"]
  Production [icon: kubernetes, label: "Production\nCluster"]
}

// Monitoring
Monitoring [color: orange] {
  Logs [icon: elasticsearch, label: "ELK Stack"]
  Metrics [icon: prometheus, label: "Prometheus"]
  Alerts [icon: grafana, label: "Grafana"]
}

// Connections
Source > Build: Webhook
Build > Test: Compile
Test > Security Scan: Pass
Security Scan > Package: Pass
Package > Registry: Push Image

Registry > Dev: Auto Deploy
Dev > Staging: Manual Approve
Staging > Production: Manual Approve

Dev, Staging, Production > Logs: Send Logs
Dev, Staging, Production > Metrics: Send Metrics
Metrics > Alerts: Alert Rules
```

**Use case:** Complete CI/CD pipeline with automated testing and progressive deployment.

---

## Tips for Creating Effective Diagrams

### 1. Start Simple
Begin with major components, then add detail:
```
// Start with this
Frontend > Backend > Database

// Then expand
Frontend [icon: react]
Backend [icon: nodejs]
Database [icon: postgres]

// Finally add details
Frontend [icon: react, label: "React SPA\nv18.2"]
Backend [icon: nodejs, label: "Express API\nPort 3000"]
Database [icon: postgres, shape: cylinder, label: "PostgreSQL 15"]
```

### 2. Use Consistent Colors
Color code by tier, environment, or responsibility:
```
colorMode bold

// By tier
Web Tier [color: green] { ... }
App Tier [color: blue] { ... }
Data Tier [color: red] { ... }

// By environment
Dev [color: yellow] { ... }
Staging [color: orange] { ... }
Prod [color: red] { ... }
```

### 3. Add Meaningful Labels
Include versions, ports, instance counts:
```
API [icon: nodejs, label: "Express API\nv4.18\nPort: 8080"]
Database [icon: postgres, label: "PostgreSQL 15\n(3 replicas)"]
Cache [icon: redis, label: "Redis 7\n16GB RAM"]
```

### 4. Show Data Transformations
Label connections with what flows:
```
Client > API: HTTP POST /orders
API > Queue: OrderCreated Event (JSON)
Queue > Worker: Message (Protobuf)
Worker > Database: INSERT order (SQL)
```

### 5. Group Logically
Use groups to show boundaries:
```
AWS Account [icon: aws-account] {
  Production VPC [icon: aws-vpc] {
    Public Subnet { ... }
    Private Subnet { ... }
  }

  DR VPC [icon: aws-vpc] {
    ...
  }
}
```

## Common Patterns

### Load Balancer + Auto Scaling
```
LoadBalancer [icon: aws-elb]
Server1, Server2, Server3 [icon: aws-ec2]
LoadBalancer > Server1, Server2, Server3
```

### Primary-Replica Database
```
Primary [icon: postgres, label: "Primary"]
Replica1, Replica2 [icon: postgres, label: "Read Replica"]
Primary > Replica1, Replica2: Replication
```

### Cache-Aside Pattern
```
App > Cache: Check Cache
Cache --> App: Cache Miss
App > Database: Query DB
App > Cache: Update Cache
```

### Pub/Sub Messaging
```
Publisher1, Publisher2 > Topic
Topic > Subscriber1, Subscriber2, Subscriber3
```

## References

- **Official Examples:** https://docs.eraser.io/docs/examples
- **Syntax Guide:** https://docs.eraser.io/docs/syntax
- **Icon Reference:** See icon-reference.md in this directory
