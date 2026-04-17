# Pertemuan 5: Storage Services

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami tiga jenis storage cloud
- Menggunakan object storage (S3)
- Menggunakan block storage (EBS)
- Menggunakan file storage (EFS)
- Memilih storage type yang tepat

## Materi Pembelajaran

### 1. Object Storage (S3)
- Konsep object storage
- Buckets, keys, dan objects
- Storage classes: Standard, IA, Glacier, Deep Archive
- Versioning dan lifecycle policies
- Access control: IAM, bucket policies, ACLs
- Static website hosting
- Cost model

### 2. Block Storage (EBS)
- Konsep block storage
- Volume types: gp2, gp3, io1, io2, st1, sc1
- Snapshots dan backups
- Encryption
- Attachment ke instances
- Performance optimization

### 3. File Storage (EFS)
- Konsep file storage
- Mounting ke multiple instances
- Performance modes dan throughput modes
- Access points
- Lifecycle management
- Use cases

### 4. S3 Advanced Features
- Versioning dan MFA delete
- Server-side encryption
- Server access logging
- CloudFront integration
- S3 Intelligent-Tiering
- S3 Select dan S3 Batch Operations

### 5. Data Transfer dan Migration
- AWS DataSync
- AWS Storage Gateway
- Direct Connect
- Snowball/Snowmobile untuk large-scale transfer

## Aktivitas Praktik
1. Create S3 bucket dan upload objects
2. Configure bucket policies dan versioning
3. Create EBS volume dan attach ke instance
4. Configure file permissions dan encryption
5. Lifecycle policy configuration
6. CloudFront distribution setup

## Assignment
1. Create S3 bucket untuk web application
2. Upload multiple files dengan versioning
3. Configure public read access dengan bucket policy
4. Setup lifecycle policy: 30 hari ke IA, 90 hari ke Glacier
5. Create EBS snapshot dan restore volume

## Referensi
- AWS S3 Documentation
- EBS User Guide
- EFS User Guide
- AWS Storage Comparison
- S3 Best Practices
- Storage Security Best Practices

## Penilaian
- S3 hands-on: 25%
- EBS configuration: 25%
- Lifecycle policy: 25%
- Documentation: 25%