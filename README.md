# Networking in AWS – Load Balancer & ASG

Step-by-step tutorial on VPC, Auto Scaling Group, Bastion Host, and Application Load Balancer.


## Access the walkthrough

[![AWS Load Balancer Tutorial](https://img.youtube.com/vi/betgMcpaHH4/0.jpg)](https://www.youtube.com/embed/betgMcpaHH4?si=lwFyHMhR-eNW_jjH)

[Watch the tutorial on YouTube](https://www.youtube.com/embed/betgMcpaHH4?si=lwFyHMhR-eNW_jjH)
---

## 🏗 Project Architecture
This diagram shows the overall structure of the VPC, private subnets, bastion host, and load balancer setup.

<div align="center">
  <img src="images/aws-loadbalancer/Project Archtecture/vpc-example-private-subnets.png" width="600"/>
</div>

---

## 🛠 Step-by-Step Strategy

### Step 1: Create VPC
Created a VPC named `kaif-demo-project` with 2 private subnets, NAT Gateway (1 per AZ), and no S3 Gateway endpoints.

<div align="center">
  <img src="images/aws-loadbalancer/Step 1 Create VPC/step1_CreateVPC1.png" width="300"/>
  <img src="images/aws-loadbalancer/Step 1 Create VPC/step1_CreateVPC2.png" width="300"/>
  <img src="images/aws-loadbalancer/Step 1 Create VPC/step1_CreateVPC3.png" width="300"/>
  <img src="images/aws-loadbalancer/Step 1 Create VPC/step1_CreateVPC4.png" width="300"/>
  <img src="images/aws-loadbalancer/Step 1 Create VPC/step1_CreateVPC5.png" width="300"/>
  <img src="images/aws-loadbalancer/Step 1 Create VPC/step1_CreateVPC6.png" width="300"/>
  <img src="images/aws-loadbalancer/Step 1 Create VPC/step1_CreateVPC7.png" width="300"/>
</div>

---

### Step 2.1: Create Auto Scaling Group
Named the ASG `kaif-demo-project` and prepared to create a launch template.

<div align="center">
  <img src="images/aws-loadbalancer/Step 2.1 Create Auto Scaling Group/step2.1_createASG.png" width="400"/>
</div>

---

### Step 2.2: Create Launch Template
Configured launch template with Ubuntu AMI, t2.micro, key pair, and SG rules.

<div align="center">
  <img src="images/aws-loadbalancer/Step 2.2 Create Launch Template/step2.2_createASG1.png" width="300"/>
  <!-- continue up to step2.2_createASG8.png -->
  <img src="images/aws-loadbalancer/Step 2.2 Create Launch Template/step2.2_createASG8.png" width="300"/>
</div>

---

### Step 2.3: Configure Auto Scaling Group
Selected VPC, private subnets, and scaling policies.

<div align="center">
  <img src="images/aws-loadbalancer/Step 2.3 Configure ASG/step2.3_createASG1.png" width="300"/>
  <!-- continue up to step2.3_createASG5.png -->
  <img src="images/aws-loadbalancer/Step 2.3 Configure ASG/step2.3_createASG5.png" width="300"/>
</div>

---

### Step 3: Create Bastion Host
Launched Ubuntu t2.micro instance with public IP and SSH SG rule.

<div align="center">
  <img src="images/aws-loadbalancer/Step 3 Create a Bastion Host/step3_bastionhost1.png" width="300"/>
  <!-- continue up to step3_bastionhost8.png -->
  <img src="images/aws-loadbalancer/Step 3 Create a Bastion Host/step3_bastionhost8.png" width="300"/>
</div>

---

### Step 4.1: Secure Copy PEM File
Used `scp` to securely copy the PEM file into the Bastion Host.

```bash
scp -i "C:\Users\DELL\Downloads\kaif-devops-demo.pem" "C:\Users\DELL\Downloads\kaif-devops-demo.pem" ubuntu@15.206.66.138:/home/ubuntu
