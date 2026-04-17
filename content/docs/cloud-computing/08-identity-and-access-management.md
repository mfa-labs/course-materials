# Pertemuan 8: Identity and Access Management (IAM)

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami IAM konsep dan best practices
- Membuat users, groups, dan roles
- Membuat dan attach policies
- Mengimplementasikan multi-factor authentication
- Melakukan access auditing

## Materi Pembelajaran

### 1. IAM Fundamentals
- Identity vs Access management
- Principal, Identity, Resource, Action, Effect
- Account root user
- IAM users, groups, roles
- Credentials: Access keys, passwords
- Trust relationships

### 2. Users dan Groups
- Creating IAM users
- Password policies
- Access keys dan secrets
- Group management
- Best practices untuk user management
- Temporary credentials dengan STS

### 3. Policies dan Permissions
- Policy structure dan syntax
- Managed policies: AWS-managed vs customer-managed
- Inline policies
- Policy simulator
- Permission boundaries
- Principal-based policies

### 4. Roles dan Temporary Credentials
- Role creation
- Trust policies
- Assume role
- Cross-account roles
- Service roles untuk EC2, Lambda, RDS, etc.
- Federation dengan external IdP

### 5. Multi-Factor Authentication (MFA)
- MFA devices: Virtual MFA, Hardware MFA
- Enabling MFA
- Enforcing MFA di policies
- MFA untuk root user

### 6. Security Monitoring dan Auditing
- CloudTrail: API logging
- IAM Access Analyzer
- Credential report
- CloudWatch untuk IAM events
- AWS Config untuk compliance

## Aktivitas Praktik
1. Create IAM users dan groups
2. Attach policies ke users/groups
3. Create custom policies
4. Test permissions dengan policy simulator
5. Setup MFA untuk user
6. Create service role untuk EC2
7. Review CloudTrail logs

## Assignment
1. Design IAM structure untuk organization (dev, staging, prod)
2. Create users untuk berbagai roles (developer, admin, read-only)
3. Create custom policy untuk development team
4. Implement MFA untuk sensitive operations
5. Create cross-account roles
6. Audit dengan IAM Access Analyzer
7. Documentation: Least privilege principle

## Referensi
- IAM User Guide
- IAM Best Practices
- Policy Examples
- CloudTrail User Guide
- AWS Well-Architected - Security
- IAM Access Analyzer Documentation

## Penilaian
- Users dan groups setup: 20%
- Policy creation dan management: 30%
- MFA implementation: 20%
- Auditing dan monitoring: 20%
- Documentation: 10%