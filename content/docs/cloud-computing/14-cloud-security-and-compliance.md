# Pertemuan 14: Cloud Security dan Compliance

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami cloud security best practices
- Mengimplementasikan data encryption
- Memahami compliance frameworks
- Melakukan security auditing
- Merencanakan security strategy

## Materi Pembelajaran

### 1. Cloud Security Fundamentals
- Shared responsibility model
- Defense in depth
- Security by design
- Zero trust architecture
- Least privilege principle
- Encryption

### 2. Data Encryption
- Encryption at rest
  - S3 encryption (SSE-S3, SSE-KMS, SSE-C)
  - EBS encryption
  - RDS encryption
  - DynamoDB encryption
- Encryption in transit
  - TLS/SSL
  - HTTPS
  - VPN
- Key management
  - AWS KMS
  - Customer-managed keys
  - Key rotation

### 3. Network Security
- VPC isolation
- Security groups dan NACLs
- Private subnets
- VPN dan Direct Connect
- Web Application Firewall (WAF)
- DDoS protection (Shield)
- GuardDuty untuk threat detection

### 4. Compliance Frameworks
- HIPAA (healthcare)
- PCI-DSS (payment cards)
- GDPR (data protection)
- SOC 2 (security controls)
- FedRAMP (government)
- ISO 27001 (information security)

### 5. AWS Compliance Services
- AWS Config
- AWS Audit Manager
- AWS Security Hub
- CloudTrail
- Trusted Advisor

### 6. Security Incident Response
- Incident response plan
- Detection
- Containment
- Eradication
- Recovery
- Lessons learned

## Aktivitas Praktik
1. Enable CloudTrail logging
2. Setup AWS Config rules
3. Enable encryption (S3, RDS, EBS)
4. Configure KMS keys
5. Setup GuardDuty
6. Enable AWS Security Hub
7. Create security dashboard

## Assignment
1. Design security architecture
2. Implement encryption strategy
3. Create security group rules
4. Setup IAM least privilege
5. Compliance checklist untuk GDPR/PCI-DSS
6. Security incident response plan
7. Create security runbook
8. Security assessment report

## Referensi
- AWS Security Best Practices
- AWS KMS User Guide
- AWS WAF Developer Guide
- AWS Config User Guide
- Compliance Frameworks Documentation
- AWS Well-Architected - Security
- OWASP Top 10
- Incident Response Best Practices

## Penilaian
- Security design: 20%
- Encryption implementation: 25%
- Compliance planning: 25%
- Monitoring setup: 20%
- Documentation: 10%