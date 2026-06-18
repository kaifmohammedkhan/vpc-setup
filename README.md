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


scp -i "C:\Users\DELL\Downloads\kaif-devops-demo.pem" "C:\Users\DELL\Downloads\kaif-devops-demo.pem" ubuntu@15.206.66.138:/home/ubuntu
<div align="center">
<img src="images/aws-loadbalancer/Step 4.1 Create Bastion and SCP .pem/Step4.1_BastionHost_Copy1.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.1 Create Bastion and SCP .pem/Step4.1_BastionHost_Copy2.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.1 Create Bastion and SCP .pem/Step4.1_BastionHost_Copy3.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.1 Create Bastion and SCP .pem/Step4.1_BastionHost_Copy4.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.1 Create Bastion and SCP .pem/Step4.1_BastionHost_Copy5.png" width="300"/>
</div>

### Step 4.2: SSH Connect to Bastion Host
bash
ssh -i kaif-devops-demo.pem ubuntu@15.206.66.138
<div align="center">
<img src="images/aws-loadbalancer/Step 4.2 SSH Connect Bastion/step4.2_sshConnect_Bastion1.png" width="400"/>
<img src="images/aws-loadbalancer/Step 4.2 SSH Connect Bastion/step4.2_sshConnect_Bastion2.png" width="400"/>
</div>

### Step 4.3: Connect to Private Subnet via Bastion
bash
ssh -i kaif-devops-demo.pem ubuntu@10.0.140.20
chmod 600 ~/kaif-devops-demo.pem
<div align="center">
<img src="images/aws-loadbalancer/Step 4.3 Connect Private Subnet from Bastion Host/step4.3_ConnectPrivateSubnet1.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.3 Connect Private Subnet from Bastion Host/step4.3_ConnectPrivateSubnet2.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.3 Connect Private Subnet from Bastion Host/step4.3_ConnectPrivateSubnet3.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.3 Connect Private Subnet from Bastion Host/step4.3_ConnectPrivateSubnet4.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.3 Connect Private Subnet from Bastion Host/step4.3_ConnectPrivateSubnet5.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.3 Connect Private Subnet from Bastion Host/step4.3_ConnectPrivateSubnet6.png" width="300"/>
</div>

### Step 4.4: Serve index.html on Port 8000
Created `index.html` using Vim, then served it:

python3 -m http.server 8000
<div align="center">
<img src="images/aws-loadbalancer/Step 4.4 Index.html on Port 8000 in private subnet/step4.4_html_port1.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.4 Index.html on Port 8000 in private subnet/step4.4_html_port2.png" width="300"/>
<img src="images/aws-loadbalancer/Step 4.4 Index.html on Port 8000 in private subnet/step4.4_html_port3.png" width="300"/>
</div>

### Step 5.1: Create Application Load Balancer
Name: kaif-demo-project

VPC: kaif-demo-project-vpc

Subnets: 2 public subnets

SG: allows port 80

<div align="center">
<img src="images/aws-loadbalancer/Step 5.1 Create Application Load Balancer/step5.1_createALB1.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.1 Create Application Load Balancer/step5.1_createALB2.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.1 Create Application Load Balancer/step5.1_createALB3.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.1 Create Application Load Balancer/step5.1_createALB4.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.1 Create Application Load Balancer/step5.1_createALB5.png" width="300"/>
</div>

### Step 5.2: Create Target Group
Target type: Instances

Name: kaif-devops-demo

Protocol: HTTP, Port: 80

Registered targets: private subnet instances

<div align="center">
<img src="images/aws-loadbalancer/Step 5.2 Create Taget Group/step5.2_targetgroup1.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.2 Create Taget Group/step5.2_targetgroup2.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.2 Create Taget Group/step5.2_targetgroup3.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.2 Create Taget Group/step5.2_targetgroup4.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.2 Create Taget Group/step5.2_targetgroup5.png" width="300"/>
</div>

### Step 5.3: Attach Target Group to ALB
Added the created target group to the ALB and completed setup.

<div align="center">
<img src="images/aws-loadbalancer/Step 5.3 Add the Target Group in ALB/step5.3_addTGinALB1.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.3 Add the Target Group in ALB/step5.3_addTGinALB2.png" width="300"/>
<img src="images/aws-loadbalancer/Step 5.3 Add the Target Group in ALB/step5.3_addTGinALB3.png" width="300"/>
</div>

### Step 6: Access via ALB DNS
Copied the ALB DNS name and opened it in the browser to access index.html served on port 80.

<div align="center">
<img src="images/aws-loadbalancer/Step 6 ALB DNS Name to open the index.html on port 80/step6_AlbDns1.png" width="300"/>
<img src="images/aws-loadbalancer/Step 6 ALB DNS Name to open the index.html on port 80/step6_AlbDns2.png" width="300"/>
<img src="images/aws-loadbalancer/Step 6 ALB DNS Name to open the index.html on port 80/step6_AlbDns3.png" width="300"/>
</div>

---

### 📝 Notes

VPC: Isolated networking with private subnets and NAT gateways.

ASG: Provides scalability and resilience.

Bastion Host: Secure entry point to private instances.

ALB: Distributes traffic across targets.

Target Groups: Define routing rules for ALB.

Demo: Showed secure access and scaling of workloads via ALB DNS.
