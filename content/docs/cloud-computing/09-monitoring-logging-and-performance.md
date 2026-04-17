# Pertemuan 9: Monitoring, Logging, dan Performance

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Menggunakan CloudWatch untuk monitoring
- Setup logging untuk berbagai services
- Membuat alarms dan notifications
- Melakukan performance analysis
- Troubleshooting dengan logs

## Materi Pembelajaran

### 1. CloudWatch Fundamentals
- Metrics: Dimana metrics disimpan
- Dashboards untuk visualization
- Custom metrics
- Metric math
- Retention periods

### 2. CloudWatch Logs
- Log groups dan log streams
- Log insights untuk queries
- Log retention
- Filtering dan patterns
- Logs from EC2, RDS, Lambda
- VPC Flow Logs

### 3. Alarms dan Events
- Alarm creation
- Alarm states: OK, ALARM, INSUFFICIENT_DATA
- Alarm actions: SNS, Auto Scaling, EC2
- Composite alarms
- Anomaly detection

### 4. CloudWatch Events / EventBridge
- Event patterns
- Targets: Lambda, SNS, SQS, EC2, etc.
- Scheduled rules (cron)
- Event routing

### 5. Application Performance Monitoring
- X-Ray untuk distributed tracing
- Service map
- Sampling
- Annotations dan metadata
- Performance insights

### 6. Logging Best Practices
- Centralized logging
- Log aggregation
- Structured logging
- Log analysis dan insights
- Retention policies
- Cost optimization

## Aktivitas Praktik
1. Create CloudWatch dashboard
2. Setup custom metrics
3. Create alarms dengan SNS notifications
4. Query logs dengan Insights
5. Setup VPC Flow Logs
6. X-Ray tracing untuk Lambda
7. Performance analysis

## Assignment
1. Design monitoring strategy untuk web application
2. Create dashboard untuk real-time monitoring
3. Setup alarms untuk critical metrics
4. Implement centralized logging
5. Create custom metric untuk business KPI
6. Query logs untuk troubleshooting
7. Create runbook untuk common alerts

## Referensi
- CloudWatch User Guide
- CloudWatch Logs Insights Query Syntax
- X-Ray Developer Guide
- Monitoring Best Practices
- AWS Well-Architected - Operational Excellence
- Troubleshooting Guide

## Penilaian
- Dashboard creation: 20%
- Logs configuration: 25%
- Alarms setup: 25%
- Queries dan analysis: 20%
- Documentation: 10%