# Pertemuan 10: Auto Scaling dan Orchestration

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami auto scaling concepts
- Mengimplementasikan auto scaling policies
- Menggunakan containers: Docker dan Kubernetes
- Infrastructure as Code dengan Terraform
- Orchestration patterns

## Materi Pembelajaran

### 1. Auto Scaling Fundamentals
- Scaling policies: Horizontal vs Vertical
- Scaling triggers dan cooldown
- Scaling metrics
- Predictive scaling

### 2. EC2 Auto Scaling
- Launch templates
- Auto Scaling Groups (ASG)
- Lifecycle hooks
- Scaling policies: Target tracking, step, simple
- Health check types
- Termination policies

### 3. Container Basics
- Docker fundamentals
  - Images dan containers
  - Dockerfile
  - Container registries: ECR, Docker Hub
- Kubernetes basics
  - Pods, Services, Deployments
  - StatefulSets
  - Ingress

### 4. AWS Container Services
- ECS (Elastic Container Service)
  - Task definitions
  - Services
  - EC2 vs Fargate launch types
- EKS (Elastic Kubernetes Service)
- App Runner

### 5. Infrastructure as Code
- Terraform fundamentals
  - HCL syntax
  - State management
  - Modules
  - Remote backend
- AWS CloudFormation
  - Templates (JSON/YAML)
  - Stacks
  - Change sets

### 6. CI/CD Integration
- CodeCommit, CodeBuild, CodeDeploy, CodePipeline
- Automated deployments
- Blue/green deployments

## Aktivitas Praktik
1. Create Dockerfile untuk aplikasi
2. Build dan push image ke ECR
3. Create ECS task definition
4. Deploy ECS service
5. Setup auto scaling
6. Terraform: Create VPC dan subnets
7. Terraform: Deploy EC2 instances

## Assignment
1. Containerize aplikasi dengan Docker
2. Setup ECR repository
3. Create ECS cluster dengan Fargate
4. Implement auto scaling untuk ECS service
5. Write Terraform code untuk infrastructure
6. Setup CI/CD pipeline
7. Performance testing dan optimization

## Referensi
- Docker Documentation
- Kubernetes Official Documentation
- AWS ECS User Guide
- AWS EKS User Guide
- Terraform AWS Provider
- AWS Well-Architected - Reliability
- Infrastructure as Code Best Practices

## Penilaian
- Docker containerization: 20%
- ECS/EKS deployment: 25%
- Auto scaling setup: 25%
- Terraform/IaC: 20%
- CI/CD integration: 10%