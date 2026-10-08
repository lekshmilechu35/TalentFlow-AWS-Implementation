# TalentFlow AI – AWS Cloud Implementation

## Project Overview

**TalentFlow AI** is a recruitment and talent management application designed to manage candidates, job openings, interviews, hiring pipelines, and recruitment analytics.

As part of my AWS Cloud internship at **Davine Technologies**, I worked on the **AWS cloud deployment and infrastructure implementation of the supplied TalentFlow AI application**.

The project focused on deploying and configuring the application infrastructure on AWS, including networking, compute, database, load balancing, security, and application connectivity.

> **Scope Note:** The TalentFlow AI application/source code was supplied as part of the internship project. My work focused on AWS cloud deployment and infrastructure implementation. Development of a production AI/ML recruitment engine was outside the scope of this project.

---

## Project Objectives

The main objectives of the implementation were:

* Deploy the TalentFlow application on AWS.
* Design and configure a suitable AWS network architecture.
* Configure secure access between AWS resources.
* Deploy the application on Amazon EC2.
* Configure an Application Load Balancer for application access.
* Configure Amazon RDS as the application database.
* Implement IAM-based access management.
* Configure security groups and network routing.
* Verify application health and AWS resource connectivity.
* Document the deployed cloud architecture and implementation.

---

## AWS Architecture

The implemented architecture consists of the following major components:

```text
                         Users
                           |
                           v
                +----------------------+
                | Application Load     |
                | Balancer (ALB)       |
                +----------+-----------+
                           |
                           v
                +----------------------+
                | Amazon EC2           |
                | TalentFlow           |
                | Application          |
                +----------+-----------+
                           |
                           v
                +----------------------+
                | Amazon RDS           |
                | TalentFlow Database  |
                +----------------------+

                    AWS VPC
        +-----------------------------------+
        |                                   |
        |  Public / Application Networking  |
        |                                   |
        |  Private Database Networking      |
        |                                   |
        +-----------------------------------+
```

### Architecture Diagram

<img width="1312" height="1199" alt="TalentFlow AI AWS Cloud Architecture" src="https://github.com/user-attachments/assets/89c8e232-9436-4051-a35c-3a36bb707c42" />


---

## AWS Services Implemented

| AWS Service                           | Purpose                                                      |
| ------------------------------------- | ------------------------------------------------------------ |
| **Amazon VPC**                        | Created the networking environment for the application       |
| **Subnets**                           | Separated application/network resources                      |
| **Internet Gateway**                  | Provided internet connectivity for required public resources |
| **Route Tables**                      | Controlled network traffic routing                           |
| **Security Groups**                   | Controlled inbound and outbound access                       |
| **Amazon EC2**                        | Hosted the TalentFlow application                            |
| **Application Load Balancer**         | Provided application traffic distribution and access         |
| **Amazon RDS**                        | Provided the relational database backend                     |
| **AWS IAM**                           | Managed AWS identities and access                            |
| **EC2 Instance Connect / SSH access** | Used for secure instance administration                      |
| **Amazon CloudWatch**                 | Used for application/resource monitoring where configured    |

---

# AWS Implementation

## 1. IAM Configuration

An IAM-based administrative user was configured for AWS resource management instead of relying on the root account for normal operations.

Security considerations included:

* Root account MFA was enabled.
* IAM user access was configured.
* IAM roles and permissions were reviewed.
* AWS resources were managed using the appropriate IAM identity.

---

## 2. VPC Configuration

A dedicated VPC was configured for the TalentFlow environment.

### VPC Configuration

* VPC CIDR: `10.0.0.0/16`
* Internet Gateway configured
* Public and private route configurations
* Application and database networking separated
* Security groups configured for controlled communication

The VPC provided the networking foundation for the TalentFlow application.

---

## 3. Security Groups

Security groups were configured to control communication between the application components.

### TalentFlow ALB Security Group

The Application Load Balancer security group was configured to allow web traffic required for the application.

### TalentFlow EC2 Security Group

The EC2 security group was configured to allow:

* Application traffic from the Application Load Balancer
* Administrative access through the configured EC2 access method
* Required outbound communication

This helped restrict direct access to the application instance.

---

## 4. Amazon EC2

The TalentFlow application was deployed on an Amazon EC2 instance.

### EC2 Configuration

* Instance name: `TalentFlow-EC2`
* Instance type: `t3.micro`
* Availability Zone: `us-east-1a`
* Operating environment configured for application deployment

The application environment was configured with:

* Git
* Python
* pip
* Python virtual environment

A Python virtual environment named:

```text
talentflow-env
```

was created for the application.

---

## 5. TalentFlow Application Deployment

The supplied TalentFlow AI application was deployed to the EC2 environment.

The application was configured and tested using the provided application code.

Application health testing was performed using:

```text
/health
```

The application health check returned a healthy response.

The application API was also tested successfully through the configured application environment.

---

## 6. Application Load Balancer

An Application Load Balancer was configured to provide controlled access to the TalentFlow application.

### Load Balancer Components

* Application Load Balancer
* Target Group
* EC2 target
* Health checks
* Security group configuration

The target group was configured with the TalentFlow EC2 application instances/targets.

Health checks were verified successfully during the implementation.

The ALB provided a more production-oriented architecture than exposing the EC2 instance directly to users.

---

## 7. Amazon RDS

Amazon RDS was configured as the database component for the TalentFlow environment.

### RDS Configuration

* Database identifier: `talentflow-db`
* Instance class: `db.t4g.micro`
* Availability Zone: `us-east-1b`
* Database status: Available

The database was configured as part of the application architecture rather than storing the application's persistent data directly on the EC2 instance.

---

# Application Features

The supplied TalentFlow application provided functionality for:

* Candidate management
* Job openings
* Scheduled interviews
* Hiring pipeline
* Recruitment analytics
* Application settings

The application dashboard provided recruitment-related statistics and workflow information.

---

# Application Verification

The deployed application was tested during implementation.

### Verification performed

* EC2 instance health verified
* Application environment configured
* Application health endpoint tested
* API endpoint tested
* Load Balancer target health checked
* RDS availability verified
* Security group connectivity reviewed
* AWS networking configuration verified

Example application health endpoint:

```text
/health
```

Expected result:

```text
Healthy
```

---

# Project Security

Security considerations implemented during the project included:

* IAM-based AWS access
* Root account MFA
* Security groups for network-level access control
* Restricted EC2 access
* Separate application and database networking
* Load Balancer-based application access
* No AWS access keys or passwords stored in the repository

---

# Project Architecture Flow

```text
User
  |
  v
Application Load Balancer
  |
  v
TalentFlow EC2 Application
  |
  v
Amazon RDS Database
```

All major application resources were deployed within the AWS networking environment configured for the project.

---

# Technologies Used

### Cloud

* Amazon Web Services (AWS)
* Amazon EC2
* Amazon VPC
* Amazon RDS
* Application Load Balancer
* AWS IAM
* Amazon CloudWatch

### Networking

* VPC
* Subnets
* Route Tables
* Internet Gateway
* Security Groups

### Application Environment

* Python
* Flask
* Git
* pip
* Python Virtual Environment

---

# Project Evidence

The repository may contain screenshots demonstrating the implementation, including:

* IAM configuration
* VPC configuration
* Subnets
* Route tables
* Security groups
* EC2 instance
* EC2 application environment
* Application health/API testing
* Application Load Balancer
* Target Group health
* RDS database
* TalentFlow application dashboard

---

# Project Outcome

The TalentFlow AI application was successfully prepared for deployment in an AWS cloud environment with supporting infrastructure for:

* Application hosting
* Database connectivity
* Load balancing
* Network isolation
* Access management
* Security controls
* Application health verification

The project provided practical experience in designing and implementing an AWS-based application infrastructure.

---

# Learning Outcomes

Through this project, I gained practical experience in:

* AWS cloud infrastructure deployment
* VPC and subnet design
* AWS networking
* EC2 application deployment
* Application Load Balancer configuration
* Amazon RDS configuration
* IAM access management
* Security group configuration
* Application health testing
* Cloud architecture documentation
* Troubleshooting AWS application connectivity

---

# Project Scope Disclaimer

This repository documents my **AWS cloud deployment and infrastructure implementation work** for the TalentFlow AI internship project.

The TalentFlow AI application/source code was supplied as part of the project. The project did not involve developing a production-grade AI/ML recruitment engine or training/developing AI models.

---

## Internship

**Domain:** AWS Cloud
**Organization:** Davine Technologies
**Project:** TalentFlow AI – Recruitment & Talent Management Platform
**Focus:** AWS Cloud Deployment & Infrastructure Implementation

---

## Author

**Lekshmi A.**

AWS | Azure | Cloud Engineering

---

### Note

This repository is intended to demonstrate the AWS cloud implementation, architecture, configuration, and learning outcomes associated with the internship project.
