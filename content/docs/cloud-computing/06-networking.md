# Pertemuan 6: Networking dalam Cloud

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami Virtual Private Cloud (VPC)
- Mengkonfigurasi subnets dan routing
- Menggunakan security groups dan NACLs
- Mengimplementasikan load balancing
- Memahami CDN dan edge locations

## Materi Pembelajaran

### 1. Virtual Private Cloud (VPC)
- VPC basics dan architecture
- CIDR blocks dan IP addressing
- Public vs private subnets
- NAT gateways dan NAT instances
- VPC peering dan transit gateway
- VPC endpoints

### 2. Subnets dan Routing
- Subnet design best practices
- Route tables
- Internet Gateway
- NAT Gateway vs NAT Instance
- Custom routes
- Route 53 DNS service

### 3. Security Groups dan Network ACLs
- Security Groups: stateful firewall
- NACLs: stateless firewall
- Inbound vs outbound rules
- Security best practices
- Common ports dan protocols
- Debugging network connectivity

### 4. Load Balancing
- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Classic Load Balancer (CLB)
- Health checks
- Sticky sessions
- SSL/TLS termination
- Path-based routing

### 5. Content Delivery Network (CDN)
- CloudFront architecture
- Distribution creation
- Cache behaviors
- Origin types
- Geo-restriction
- DDoS protection

### 6. VPN dan Direct Connect
- VPN connections
- AWS Direct Connect
- Hybrid networking

## Aktivitas Praktik
1. Create VPC dengan public dan private subnets
2. Configure NAT Gateway untuk private subnet
3. Create dan configure Security Groups
4. Launch EC2 instances di berbagai subnets
5. Setup Application Load Balancer
6. Create CloudFront distribution

## Assignment
1. Design network architecture untuk e-commerce platform
2. Implement VPC dengan 2 public dan 2 private subnets di 2 AZs
3. Configure security groups untuk multi-tier application
4. Setup ALB dengan health checks
5. Test load balancing dan failover

## Referensi
- AWS VPC Documentation
- VPC Architecture Best Practices
- Security Groups and NACLs
- Elastic Load Balancing Guide
- CloudFront Developer Guide
- AWS Well-Architected - Networking

## Penilaian
- VPC configuration: 25%
- Security setup: 25%
- Load balancing: 25%
- Testing dan documentation: 25%