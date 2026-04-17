# Pertemuan 12: Backup, Disaster Recovery, dan Business Continuity

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami backup strategies
- Mengimplementasikan disaster recovery plans
- Memahami RTO dan RPO
- Melakukan multi-region deployment
- Testing disaster recovery

## Materi Pembelajaran

### 1. Backup Fundamentals
- Backup types: Full, incremental, differential
- Backup frequency
- Retention policies
- Backup location dan redundancy
- Backup automation
- Backup validation

### 2. AWS Backup Service
- Centralized backup management
- Backup plans
- Cross-region backup
- Backup compliance
- Cost tracking

### 3. Disaster Recovery Concepts
- RTO (Recovery Time Objective)
- RPO (Recovery Point Objective)
- DR strategies: Backup & restore, Pilot light, Warm standby, Active-active
- DR architecture
- Failover procedures
- Failback procedures

### 4. Multi-Region Deployment
- Active-active vs active-passive
- Route 53 health checks dan failover
- Cross-region replication (S3, RDS)
- DynamoDB global tables
- Database replication

### 5. Backup for Different Services
- EC2 snapshots
- RDS automated backups dan snapshots
- EBS snapshots
- S3 versioning dan cross-region replication
- DynamoDB backups
- ElastiCache backups

### 6. DR Testing
- Test plans
- Failover testing
- Failback testing
- Documentation
- Post-incident review

## Aktivitas Praktik
1. Create EBS snapshots dan restore volume
2. Setup RDS automated backups
3. Enable cross-region replication (S3)
4. Create DynamoDB backup
5. Setup Route 53 failover routing
6. Test failover scenario
7. Create DR runbook

## Assignment
1. Design DR plan untuk multi-tier application
2. Calculate RTO dan RPO requirements
3. Implement multi-region setup
4. Setup automated backups
5. Create S3 cross-region replication
6. Setup RDS read replica di different region
7. Perform DR testing
8. Create runbook dan procedures

## Referensi
- AWS Backup User Guide
- Disaster Recovery Strategies
- AWS Well-Architected - Reliability
- RDS Backup and Recovery
- EBS Snapshots
- Multi-Region Architecture
- DR Testing Best Practices

## Penilaian
- Backup strategy design: 25%
- Multi-region setup: 25%
- DR implementation: 25%
- Testing dan validation: 15%
- Documentation: 10%