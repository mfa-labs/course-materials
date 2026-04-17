# Pertemuan 4: Virtual Machines dan Compute Services

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami konsep virtual machines
- Membedakan jenis instance dan sizing
- Launch dan configure virtual machine
- Memahami elastic computing dan auto-scaling
- Menggunakan load balancing

## Materi Pembelajaran

### 1. Konsep Virtual Machines
- Hypervisor dan virtualization
- VM vs container
- Benefits dan use cases
- VM lifecycle

### 2. AWS EC2 (Elastic Compute Cloud)
- EC2 instances dan families
- Instance types: t2, t3, m5, c5, r5, p3, etc.
- AMI (Amazon Machine Image)
- Key pairs dan security groups
- Pricing: On-demand, Reserved, Spot, Dedicated

### 3. Instance Configuration
- Choosing appropriate instance size
- Storage options: EBS, instance store, EFS
- Network configuration
- IAM roles dan instance profiles
- User data dan bootstrapping

### 4. Elastic Scaling
- Auto Scaling Groups (ASG)
- Scaling policies: Target tracking, step, simple
- Health checks
- Load Balancing: ALB, NLB, CLB
- CloudWatch metrics

### 5. Cost Optimization
- Right-sizing instances
- Reserved instances vs On-demand
- Spot instances
- Cost monitoring

## Aktivitas Praktik
1. Hands-on: Launch EC2 instance (Linux/Windows)
2. Connect: SSH/RDP connection
3. Configure: Install software, configure security groups
4. Monitor: CloudWatch monitoring
5. Scale: Create auto-scaling group

## Assignment
1. Launch dan konfigurasi 2 EC2 instances berbeda OS
2. Konfigurasi security group dan SSH access
3. Install web server dan verify access
4. Create ASG dengan minimum 1, desired 2, maximum 3
5. Documentation: Screenshot dan penjelasan

## Referensi
- AWS EC2 Documentation
- EC2 Instance Types Guide
- Best Practices for Security Groups
- EC2 Auto Scaling User Guide
- AWS Well-Architected Framework

## Penilaian
- Hands-on exercises: 40%
- Configuration correctness: 30%
- Documentation quality: 30%