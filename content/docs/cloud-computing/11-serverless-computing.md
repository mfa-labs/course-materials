# Pertemuan 11: Serverless Computing

## Tujuan Pembelajaran
Setelah menyelesaikan pertemuan ini, mahasiswa diharapkan dapat:
- Memahami serverless architecture
- Menggunakan AWS Lambda
- Mengimplementasikan event-driven applications
- Menggunakan API Gateway
- Cost optimization untuk serverless

## Materi Pembelajaran

### 1. Serverless Concepts
- Function as a Service (FaaS)
- Event-driven architecture
- Benefits: No server management, auto-scaling, pay-per-use
- Limitations: Cold starts, timeout limits, statelessness
- Use cases

### 2. AWS Lambda
- Lambda runtime: Python, Node.js, Java, Go, .NET, Ruby
- Lambda function anatomy
- Handler function
- Execution role dan permissions
- Environment variables
- Layers
- Versioning dan aliases
- Concurrency control

### 3. Lambda Triggers
- AWS events: S3, DynamoDB Streams, SQS, SNS
- Scheduled events (EventBridge)
- API Gateway
- Kinesis
- Custom events

### 4. API Gateway
- REST APIs
- HTTP APIs
- WebSocket APIs
- Request/response transformation
- Authentication dan authorization
- Rate limiting dan throttling
- Stages dan deployments
- CORS configuration

### 5. Serverless Application Model (SAM)
- SAM templates
- Local testing
- Deployment
- Debugging

### 6. Cost Optimization
- Compute duration pricing
- Free tier
- Cost estimation
- Optimization strategies
- Comparison: Serverless vs Containers

## Aktivitas Praktik
1. Write Lambda function (Python/Node.js)
2. Create API Gateway REST API
3. Integrate Lambda dengan API Gateway
4. Setup S3 trigger untuk Lambda
5. DynamoDB Streams integration
6. Schedule Lambda dengan EventBridge
7. Test dengan AWS SAM

## Assignment
1. Build serverless API (CRUD operations)
2. Implement Lambda function untuk image processing
3. Create S3 trigger untuk automatic processing
4. API Gateway dengan authentication
5. Error handling dan logging
6. Performance optimization
7. Cost estimation dan optimization

## Referensi
- AWS Lambda Developer Guide
- API Gateway User Guide
- AWS SAM Developer Guide
- Serverless Architecture Best Practices
- AWS Well-Architected - Cost Optimization
- Lambda Performance Optimization

## Penilaian
- Lambda function development: 25%
- API Gateway setup: 25%
- Event-driven implementation: 25%
- Cost optimization: 15%
- Documentation: 10%