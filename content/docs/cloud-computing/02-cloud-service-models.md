# Modul 2: Cloud Service Models (IaaS, PaaS, SaaS)

## Pendahuluan

Cloud computing services dapat dikategorikan ke dalam tiga model utama: Infrastructure as a Service (IaaS), Platform as a Service (PaaS), dan Software as a Service (SaaS). Setiap model memberikan level abstraksi yang berbeda dan transfer tanggung jawab yang berbeda antara customer dan provider. Modul ini menjelaskan masing-masing model secara detail beserta use cases dan implikasi praktisnya.

## 1. Infrastructure as a Service (IaaS)

### 1.1 Definisi dan Karakteristik

Infrastructure as a Service (IaaS) adalah cloud computing model dimana provider menyediakan virtualized computing resources melalui internet. Customers mengakses cloud computing resources seperti server virtual (instances), storage, dan networking melalui dashboard atau API.

**Karakteristik Utama IaaS:**

- **Virtualized Resources:** Customer menerima virtualized compute, storage, dan networking resources bukan physical infrastructure
- **On-Demand Access:** Resources dapat diakses kapan saja sesuai kebutuhan
- **Scalability:** Dapat dengan mudah menambah atau mengurangi resources
- **Self-Service Provisioning:** Customer dapat provision resources sendiri tanpa menghubungi provider
- **Metered Usage:** Customer hanya membayar resources yang digunakan
- **API Access:** Resources dikelola melalui API atau dashboard

### 1.2 Komponen IaaS

**Compute (Komputasi):**
Virtualized computing power. Customer dapat memilih:
- CPU cores: Jumlah processors
- Memory (RAM): Jumlah memory
- Operating system: Linux, Windows, dll
- Custom configurations

Contoh: AWS EC2 instances, Azure Virtual Machines, Google Compute Engine

**Storage (Penyimpanan):**
Cloud-based storage resources:
- **Object Storage:** Untuk unstructured data, accessed via API (S3, Azure Blob Storage)
- **Block Storage:** Untuk databases dan file systems yang need high IOPS (EBS, Azure Managed Disks)
- **Archive Storage:** Untuk long-term retention dengan lower cost (Glacier, Archive Storage)

**Networking (Jaringan):**
Virtual networking infrastructure:
- Virtual Private Cloud (VPC): Isolated network environments
- Load balancers: Distribute traffic
- Firewalls: Network security
- DNS services: Domain name resolution
- VPN: Secure connectivity

### 1.3 Control dan Tanggung Jawab

Dalam IaaS model, distribution of responsibility antara provider dan customer:

**Provider Responsible:**
- Physical infrastructure (building, cooling, power)
- Hypervisor dan virtualization layer
- Network infrastructure
- Physical security
- Hardware maintenance
- Disaster recovery (untuk provider infrastructure)

**Customer Responsible:**
- Operating system selection dan management
- Application installation dan configuration
- Data management
- Network configuration (security groups, ACLs)
- Backup dan disaster recovery untuk data
- Security updates dan patches
- User access control

### 1.4 Contoh IaaS Providers

**AWS (Amazon Web Services):**
- EC2: Virtual machines
- S3: Object storage
- EBS: Block storage
- VPC: Networking
- RDS: Managed databases (borderline dengan PaaS)

**Microsoft Azure:**
- Virtual Machines
- Azure Storage
- Virtual Networks
- App Service (borderline dengan PaaS)
- Azure SQL Database

**Google Cloud Platform:**
- Compute Engine: Virtual machines
- Cloud Storage: Object storage
- Cloud SQL: Managed databases
- Persistent Disks: Block storage
- Virtual Private Cloud: Networking

**Other Providers:**
- DigitalOcean (simple compute dan storage)
- Linode
- IBM Cloud
- Rackspace

### 1.5 Use Cases IaaS

**Development dan Testing:**
- Developers dapat quickly spin up test environments
- Tidak perlu worry tentang hardware provisioning
- Easy teardown setelah testing selesai
- Cost-effective karena pay-per-use

**High-Performance Computing:**
- Heavy computational workloads dapat distribute across many instances
- Can scale up resources sebagai needed
- Auto-scaling untuk handle spikes

**Web Hosting:**
- Host websites dan web applications
- Easy to scale dengan traffic growth
- Global data centers untuk low latency
- Built-in CDN dan load balancing

**Backup dan Disaster Recovery:**
- Store backups di cloud storage
- Geographic redundancy built-in
- Easy recovery dari failures

**Big Data Analysis:**
- Provision large clusters untuk data processing
- Only pay untuk computing time
- Can process petabytes of data

### 1.6 Keuntungan dan Kekurangan IaaS

**Keuntungan:**
- **Flexibility:** Full control atas infrastructure
- **Scalability:** Easily scale resources up atau down
- **Cost-Effective:** Pay only untuk resources yang digunakan
- **Reliability:** Built-in redundancy dan disaster recovery
- **Performance:** State-of-the-art infrastructure
- **Global Reach:** Data centers di multiple regions

**Kekurangan:**
- **Complexity:** Requires technical expertise untuk manage
- **Operational Overhead:** Need to manage OS, security updates, patches
- **Security Responsibility:** Customer bertanggung jawab untuk application dan OS security
- **Learning Curve:** Different providers memiliki different tools dan interfaces
- **Vendor Lock-In:** Difficult untuk migrate antara providers

## 2. Platform as a Service (PaaS)

### 2.1 Definisi dan Karakteristik

Platform as a Service (PaaS) adalah cloud computing model dimana provider menyediakan complete development dan deployment environment di cloud. Developers dapat develop, run, dan manage applications tanpa complexity dari building dan maintaining infrastructure.

**Karakteristik Utama PaaS:**

- **Development Framework:** Pre-built frameworks dan libraries untuk development
- **Integrated Tools:** IDE, testing tools, deployment tools built-in
- **Middleware:** Messaging, caching, database middleware provided
- **Database Services:** Managed databases yang readily available
- **Scalability:** Auto-scaling built-in
- **Focus on Development:** Developers focus pada code bukan infrastructure

### 2.2 Komponen PaaS

**Development Environment:**
- Pre-configured dengan popular languages dan frameworks
- Version control integration
- Testing frameworks
- Debugging tools

**Runtime Environment:**
- Operating system abstracted away
- Managed runtime untuk specific languages
- Auto-patching dan updates
- Performance monitoring

**Middleware Services:**
- Message queues
- Caching layers
- Logging dan monitoring
- Authentication services
- API management

**Database Services:**
- Managed relational databases
- NoSQL databases
- Backup dan recovery automated
- Scaling handled automatically

**Development Tools:**
- IDE atau web-based editors
- Source code repositories
- CI/CD pipelines
- Testing frameworks
- Performance monitoring

### 2.3 Control dan Tanggung Jawab

**Provider Responsible:**
- Infrastructure (servers, storage, networking)
- Operating system
- Middleware dan runtime
- Database engine
- Scaling dan load balancing
- Backup dan disaster recovery
- Security patching

**Customer Responsible:**
- Application code
- Data management
- User access control
- Application configuration
- Testing
- Deployment procedures
- Business logic

### 2.4 Contoh PaaS Providers

**Heroku:**
- Simple deployment dari Git repositories
- Supports multiple languages (Ruby, Python, Node, Java, etc.)
- Add-ons untuk databases, caching, monitoring
- Good untuk rapid development dan prototyping

**AWS Services:**
- Elastic Beanstalk: Application platform
- AppSync: GraphQL backend
- Amplify: Front-end dan backend

**Microsoft Azure:**
- App Service: Hosting untuk web apps
- Azure Functions: Serverless (borderline)
- Azure App Configuration: Configuration management

**Google Cloud:**
- App Engine: Application platform
- Cloud Functions: Serverless (borderline)
- Firebase: Backend for mobile/web apps

**Specialized PaaS:**
- Salesforce: CRM platform
- Shopify: E-commerce platform
- Slack: Communication platform

### 2.5 Use Cases PaaS

**Rapid Application Development:**
- Quick prototyping
- Built-in tools untuk development
- No infrastructure setup required
- Focus pada features bukan infrastructure

**Microservices Architecture:**
- Deploy microservices easily
- Built-in load balancing
- Service discovery automated
- Auto-scaling untuk each service

**API Development:**
- Create RESTful atau GraphQL APIs quickly
- Built-in authentication
- API versioning
- Rate limiting

**IoT Applications:**
- Collect data dari IoT devices
- Process streaming data
- Store time-series data
- Built-in analytics

**Multi-Tenant Applications:**
- Single application melayani multiple customers
- Tenant isolation handled by platform
- Billing per tenant
- Multi-version management

### 2.6 Keuntungan dan Kekurangan PaaS

**Keuntungan:**
- **Developer Productivity:** Focus pada coding bukan infrastructure
- **Built-In Tools:** Everything needed untuk development sudah tersedia
- **Scalability:** Auto-scaling transparent kepada developer
- **Cost Effective:** Lower total cost of ownership
- **Time to Market:** Faster deployment
- **Collaboration:** Built-in features untuk team collaboration

**Kekurangan:**
- **Less Control:** Limited customization atas infrastructure
- **Vendor Lock-In:** Difficult untuk move aplikasi antara PaaS platforms
- **Limited Flexibility:** Constraints dari platform
- **Performance Limitations:** May not suitable untuk high-performance workloads
- **Security Concerns:** Less control atas security configuration
- **Compliance Issues:** May not meet specific regulatory requirements

## 3. Software as a Service (SaaS)

### 3.1 Definisi dan Karakteristik

Software as a Service (SaaS) adalah cloud computing model dimana applications dihost dan dikelola oleh provider dan diakses oleh customers melalui web browser atau API. Customers tidak perlu install atau maintain software.

**Karakteristik Utama SaaS:**

- **Browser-Based:** Accessible melalui web browser
- **Multi-Tenant:** Satu instance melayani multiple customers
- **Automatic Updates:** Updates dan patches applied automatically
- **Accessibility:** Accessible dari anywhere dengan internet connection
- **Subscription-Based:** Typically pay per month atau per year
- **Data Managed:** Provider manage semua data dan security

### 3.2 Tipe Aplikasi SaaS

**Productivity dan Collaboration:**
- Email: Gmail, Outlook
- Office suite: Microsoft 365, Google Workspace
- Project management: Asana, Monday.com
- Note-taking: Evernote, Notion
- File sharing: Dropbox, Google Drive

**Customer Relationship Management:**
- Salesforce: Enterprise CRM
- HubSpot: Marketing CRM
- Pipedrive: Sales CRM

**Human Resources:**
- Workday: HR dan payroll
- BambooHR: HR management
- Zenefits: Benefits management

**Accounting dan Finance:**
- QuickBooks Online: Accounting
- Xero: Accounting
- SAP Concur: Expense management

**Marketing dan Analytics:**
- Google Analytics: Web analytics
- Mixpanel: Product analytics
- Segment: Customer data platform

**E-Commerce dan Retail:**
- Shopify: E-commerce platform
- WooCommerce: Shopping cart
- Square: Point of sale

**Communication:**
- Slack: Team communication
- Zoom: Video conferencing
- Microsoft Teams: Communication platform

**Other Specialized SaaS:**
- Zendesk: Customer support
- Jira: Issue tracking
- Figma: Design tool
- Adobe Creative Cloud: Design software

### 3.3 Control dan Tanggung Jawab

**Provider Responsible:**
- Entire application
- Infrastructure dan platform
- Operating system
- Database
- Scaling
- Backup dan disaster recovery
- Security
- Compliance
- Availability
- Updates dan patches

**Customer Responsible:**
- User account management
- Data entry
- Usage policies
- Password management
- Basic configuration sesuai allowed options
- Compliance atas regulations yang specifically aplikasi

### 3.4 Deployment Models untuk SaaS

**Public SaaS:**
- Shared infrastructure untuk multiple customers
- Single instance shared
- Most cost-effective
- Examples: Gmail, Salesforce, Slack

**Private SaaS:**
- Dedicated instance untuk single customer
- Higher cost
- More customization possible
- Better untuk large enterprises

**Hybrid SaaS:**
- Mix dari public dan private deployment
- Some components shared, some dedicated

### 3.5 Use Cases SaaS

**Small Business Management:**
- Limited IT resources
- Need untuk complete business solutions
- SaaS provides integrated systems
- Low upfront cost

**Enterprise Applications:**
- Large scale operations
- Integration dengan existing systems
- Specialized applications
- Global accessibility

**Collaboration:**
- Teams dalam multiple locations
- Need untuk real-time collaboration
- Remote work support

**Temporary Needs:**
- Projects that need specific software temporarily
- Easier than purchasing licenses
- Quick setup dan cancellation

**Software as Commodity:**
- Email, storage, office tools
- Standard requirements across organizations
- SaaS perfect untuk commoditized software

### 3.6 Keuntungan dan Kekurangan SaaS

**Keuntungan:**
- **No Installation:** Access immediately dari browser
- **No Maintenance:** Provider handle updates
- **Low Cost:** No upfront investment, pay-as-you-go
- **Accessibility:** Access dari anywhere
- **Collaboration:** Built-in collaboration features
- **Automatic Backups:** Data backed up automatically
- **Scalability:** Auto-scales untuk user growth
- **Security:** Professional managed security

**Kekurangan:**
- **No Control:** Cannot customize atau control underlying infrastructure
- **Limited Customization:** Functionality terbatas pada apa yang provided
- **Data Security:** Data di provider servers
- **Internet Dependency:** Need reliable internet connection
- **Subscription Costs:** Recurring costs dapat add up
- **Data Migration:** Difficult untuk move data out
- **Performance:** Performance depends pada internet connection
- **Compliance Issues:** May not meet regulatory requirements untuk sensitive data

## 4. Perbandingan Model Layanan

### 4.1 Shared Responsibility Model

| Responsibility | On-Premises | IaaS | PaaS | SaaS |
|---|---|---|---|---|
| Applications | Customer | Customer | Customer | Provider |
| Data | Customer | Customer | Customer | Provider |
| Runtime | Customer | Customer | Provider | Provider |
| Middleware | Customer | Customer | Provider | Provider |
| Operating System | Customer | Customer | Provider | Provider |
| Virtualization | Customer | Provider | Provider | Provider |
| Servers | Customer | Provider | Provider | Provider |
| Storage | Customer | Provider | Provider | Provider |
| Networking | Customer | Provider | Provider | Provider |

### 4.2 Control vs Convenience

```
              Control
                ↑
                |
On-Premises ----+---- IaaS
                |
                +---- PaaS
                |
                +---- SaaS
                |
                +---- Convenience
```

**On-Premises:** Maximum control, maximum responsibility dan cost
**IaaS:** More control than PaaS/SaaS, moderate responsibility
**PaaS:** Balance antara control dan convenience
**SaaS:** Minimal control, minimal responsibility, maximum convenience

### 4.3 Perbandingan Cost

**On-Premises:**
- High upfront CapEx
- Ongoing operational costs
- High initial investment

**IaaS:**
- Lower upfront investment
- Pay for resources used
- Flexible scaling reduces waste

**PaaS:**
- Lower operational overhead
- Pay for development platform
- Reduced developer costs

**SaaS:**
- Subscription per user atau usage
- No upfront investment
- Predictable costs

**Example Cost Comparison untuk hosting website:**
- On-Premises: $50K upfront + $10K/year operational = expensive
- IaaS (AWS): $100/month scaling based on traffic = flexible, lower cost
- PaaS (Heroku): $200/month untuk same workload = simpler
- SaaS (Wix): $300/year untuk basic website = extremely simple dan cheap

### 4.4 Selection Criteria

**Choose IaaS jika:**
- Need untuk high control atas infrastructure
- Have specific hardware requirements
- Want flexibility untuk customize
- Have expertise untuk manage infrastructure

**Choose PaaS jika:**
- Want faster development cycles
- Don't have extensive infrastructure expertise
- Need scalability tanpa management overhead
- Want to focus pada application development

**Choose SaaS jika:**
- Need untuk complete application solution
- Don't have specific customization needs
- Want minimal operational overhead
- Need untuk quick deployment

## 5. Shared Responsibility Model Dalam Detail

### 5.1 Security Implications

**On-Premises:**
- 100% customer responsibility
- Complete control tetapi full burden

**IaaS:**
- Provider: Physical security, hypervisor, network security
- Customer: OS security, application security, data security, user management
- Common mistakes: Misconfigured security groups, unpatched OS

**PaaS:**
- Provider: Infrastructure, platform security
- Customer: Application security, data management, user access
- Common mistakes: Insecure code, insufficient testing

**SaaS:**
- Provider: Almost everything
- Customer: User account management, data governance
- Common mistakes: Weak passwords, oversharing data

### 5.2 Compliance Responsibility

**Regulatory Compliance:**
- Data protection: GDPR, data residency
- Industry-specific: HIPAA (healthcare), PCI-DSS (payments)
- Financial: SOX (public companies)
- Security: ISO 27001

**Provider Responsibilities:**
- Maintain infrastructure security
- Provide compliance documentation
- Audit trails
- Encryption

**Customer Responsibilities:**
- Data classification
- Access control policies
- Usage monitoring
- Incident response
- Vendor assessment
- Contract negotiations

## 6. Hybrid Models dan Emerging Trends

### 6.1 DBaaS (Database as a Service)

Service untuk managed databases dapat dianggap sebagai hybrid antara IaaS dan PaaS:
- Provider manage infrastructure dan database engine
- Customer manage data dan queries
- Examples: AWS RDS, Google Cloud SQL, Azure SQL Database

### 6.2 Containerization sebagai PaaS Alternative

Docker dan Kubernetes menyediakan middle ground antara IaaS dan PaaS:
- More control daripada traditional PaaS
- Less operational overhead daripada IaaS
- Portability across cloud providers

### 6.3 Serverless / Functions as a Service

Lambda functions borderline antara PaaS dan utility computing:
- Customer hanya write functions
- Provider manage everything lainnya
- Pay per invocation
- Extreme abstraction dari infrastructure

## Kesimpulan

Tiga service models IaaS, PaaS, dan SaaS masing-masing melayani kebutuhan berbeda:

- **IaaS:** Untuk organizations yang need control dan flexibility
- **PaaS:** Untuk development teams yang want faster development
- **SaaS:** Untuk organizations yang need complete solutions dengan minimal overhead

Kebanyakan organizations menggunakan kombinasi dari ketiga models ini untuk different workloads dan needs.

## Pertanyaan Review

1. Jelaskan perbedaan antara IaaS, PaaS, dan SaaS dalam hal control dan responsibility
2. Berikan contoh use case untuk masing-masing service model
3. Apa keuntungan dan kekurangan dari masing-masing model?
4. Bagaimana shared responsibility model berbeda antara IaaS dan SaaS?
5. Untuk organisasi Anda, identifikasi mana yang lebih cocok dan mengapa?

## Referensi Lebih Lanjut

- AWS Service Models: https://aws.amazon.com/types-of-cloud-computing/
- Microsoft Azure: Types of Cloud Computing: https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/
- Google Cloud: Cloud Computing Models: https://cloud.google.com/learn/what-is-saas
- Shared Responsibility: https://aws.amazon.com/compliance/shared-responsibility-model/
- NIST Cloud Service Models: https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-145.pdf