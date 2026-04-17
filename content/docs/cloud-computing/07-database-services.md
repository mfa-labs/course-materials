# Pertemuan 7: Database Services

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami relational databases di cloud
- Menggunakan NoSQL databases
- Memahami data warehouse solutions
- Mengimplementasikan backup dan recovery
- Memilih database yang tepat

## Materi Pembelajaran

### 1. Relational Databases (RDS)
- Supported engines: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server
- Multi-AZ deployments
- Read replicas
- Automated backups
- Parameter groups dan option groups
- Database subnet groups
- Cost optimization

### 2. NoSQL Databases
- DynamoDB: Key-value store
  - Tables, items, attributes
  - Primary keys (partition + sort)
  - Provisioned vs on-demand capacity
  - Global secondary indexes
  - Streams dan triggers
- DocumentDB: MongoDB compatible
- ElastiCache: In-memory caching
  - Redis vs Memcached
  - Use cases untuk caching

### 3. Data Warehouse Solutions
- Amazon Redshift
  - Cluster architecture
  - Node types
  - Columnar storage
  - Data loading
  - Query performance
- AWS Glue untuk ETL

### 4. Analytics Databases
- Amazon Athena: Query S3 dengan SQL
- AWS Lake Formation
- BigQuery alternatives

### 5. Database Migration
- AWS DMS (Database Migration Service)
- Schema conversion
- Minimal downtime migration
- Validation dan testing

## Aktivitas Praktik
1. Create RDS MySQL instance
2. Connect dan create database/tables
3. Setup read replica
4. Configure automated backups
5. Create DynamoDB table
6. Put/Get items operations
7. Query dengan DynamoDB

## Assignment
1. Design database schema untuk aplikasi
2. Create RDS instance dan setup multi-AZ
3. Load sample data
4. Create read replica di different AZ
5. Test failover scenario
6. DynamoDB table untuk user sessions
7. Performance testing dan optimization

## Referensi
- RDS User Guide
- DynamoDB Developer Guide
- Choosing Right Database
- AWS Database Migration Best Practices
- Performance Tuning Guide
- Cost Optimization for Databases

## Penilaian
- RDS setup dan configuration: 30%
- DynamoDB implementation: 30%
- Migration scenario: 20%
- Documentation: 20%