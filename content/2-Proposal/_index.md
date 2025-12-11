---
title: "Proposal"
date: "2025-09-08"
weight: 2
chapter: false
pre: " <b> 2. </b> "
---

## 1. EXECUTIVE SUMMARY

### 1.1 Project Overview

NutriChat is an intelligent nutrition assistant web application that helps users build a healthy diet based on personal needs. The application uses the Claude 3 Haiku AI model through the AWS Bedrock service to analyze nutrition data and provide personalized recommendations based on physical condition, health goals, and eating habits.

The system is deployed entirely on AWS with a modern serverless architecture, optimizing costs, increasing scalability, and reducing operational burden. The architecture adheres to the AWS Well-Architected Framework principles: security, performance, reliability, cost optimization, and operational excellence.

### 1.2 Main Objectives

- Build an automated nutrition consultation system.
- Personalize recommendations based on profile, allergies, and health goals
- Deploy on AWS with high availability and auto-scaling
- Ensure user data security.
- Optimize operational costs.

### 1.3 Achievements

**100% Success** - The project has been deployed with all features working stably:

- **Infrastructure**: AWS resources managed with Terraform
- **Authentication**: AWS Cognito with JWT, email verification
- **AI Integration**: Claude 3 Haiku with streaming responses
- **Database**: PostgreSQL Multi-AZ with automated backups
- **Frontend**: Vue.js responsive UI on CloudFront CDN
- **Monitoring**: CloudWatch with logs, metrics, alerts

**Production URL**: https://d13s9jdjslcf4.cloudfront.net



---

## 2. PROBLEM STATEMENT

### 2.1 What'"'"'s the Problem?

#### Current Issues in Nutrition Consultation

**1. High Consultation Costs**
- One-on-one nutrition consultation with experts
- Not everyone can afford the fees
- Long waiting times for appointments (1-2 weeks)

**2. Lack of Personalization**
- Online nutrition information is generic
- Does not consider personal allergies and preferences
- Does not match individual health goals

**3. Difficult to Access 24/7**
- Experts only work during business hours
- No immediate support when needed
- Difficult to track progress continuously

**4. Language and Cultural Barriers**
- Lack of Vietnamese-language consultation
- Does not fit Vietnamese food culture
- Difficult to apply advice from abroad

### 2.2 The Solution

#### NutriChat Solution

**1. AI-Powered Chatbot**

- Uses Claude 3 Haiku - an advanced AI model
- Instant responses, no waiting
- Available 24/7, unlimited consultations
- Low cost: ~$0.002/conversation

**2. Personalization Engine**

- Stores detailed profile: height, weight, goals
- Tracks food allergies
- Considers dietary preferences (vegetarian, vegan, keto, etc.)
- Adjusts recommendations based on physical activity level

**3. Cloud-Native Architecture**

- Deployed on AWS with high availability
- Auto-scaling based on usage
- Multi-AZ deployment for 99.9% uptime
- Global CDN for fast access speed

**4. Security & Privacy**

- AWS Cognito for authentication
- JWT tokens with expiration
- Encryption at rest and in transit



### 2.3 Benefits and Return on Investment

#### User Benefits

**1. Convenience**
- Access anytime, anywhere
- Instant responses (< 3 seconds)
- Save conversation history for review
- No need to travel, saves time

**2. Personalization**
- Recommendations tailored to personal profile
- Avoid allergenic foods
- Match health goals

**3. Privacy**
- No need for face-to-face meetings
- Data encrypted and secure


#### ROI for Investors

- NutriChat is currently in MVP development phase and has not implemented any paid plans for users. The product is open to the community for free use to gather feedback, evaluate usefulness, and refine the user experience. This phase helps the development team understand real needs, adjust features, and shape an appropriate business model.
- Although there is no revenue at the current time, survey results and user feedback allow for preliminary forecasts about commercialization potential in the future.

**Operating Costs (Estimated)**: $86/month (~$1,032/year) (costs may vary based on actual usage)

**Revenue Model Forecast (at official launch)**:
If the product reaches 1,000 active users after full development, the proposed pricing model could include:
  - Freemium: 70% of users (free to attract community)
  - Basic Plan: 25% of users, estimated ~ $5/month
  - Premium Plan: 5% of users, estimated ~ $15/month

**Long-term Business Benefits**
- Operation Optimization: Using serverless architecture provides flexible costs based on user count, saving more than traditional fixed infrastructure.
- Scalability: Cloud architecture allows scaling and adding advanced features without changing infrastructure.
- Improved User Experience: Reduced downtime and faster AI responses → better user retention, increased likelihood of upgrading to paid plans.
- Reusability: AI platform & nutrition data can expand to many new products (meal plans, coaching, nutrition insights).



---

## 3. SOLUTION ARCHITECTURE

### 3.1 AWS Services Used

#### Compute & Container
**Amazon ECS Fargate**
- Serverless container platform
- Auto-scaling 1-4 tasks
- 0.5 vCPU, 1GB RAM per task
- Cost: $30-50/month

**Application Load Balancer (ALB)**
- Distributes traffic to ECS tasks
- Automatic health checks
- SSL/TLS termination
- Cost: Included in ECS

#### Storage & Database
**Amazon RDS PostgreSQL**
- db.t3.micro instance
- Multi-AZ deployment
- 20GB storage with auto-scaling
- Automated backups (7 days retention)
- Cost: $15-25/month

**Amazon S3**
- Static website hosting
- Versioning enabled
- Lifecycle policies
- Cost: $1/month

#### Networking & Content Delivery
**Amazon CloudFront**
- Global CDN with 200+ edge locations
- HTTPS termination
- Cache optimization
- DDoS protection
- Cost: $0 free

**Amazon VPC**
- Public subnets (2 AZs)
- Private subnets (2 AZs)
- Internet Gateway
- NAT Gateway (optional)
- Security Groups & NACLs
- Cost: $3.25/day

**VPC Endpoints**
- Bedrock endpoint
- Secrets Manager endpoint
- Private connectivity
- Cost: $7/month

#### API & Authentication
**Amazon API Gateway**
- HTTP API (cheaper than REST API)
- JWT Authorizer with Cognito
- Rate limiting & throttling
- CORS configuration
- Cost: $3-10/month

**Amazon Cognito**
- User Pool for authentication
- Email verification with OTP
- Password policies
- MFA support
- JWT token issuance
- Cost: Free (first 50,000 MAU)

#### AI & Machine Learning
**Amazon Bedrock**
- Claude 3 Haiku model
- Streaming responses
- VPC endpoint connectivity
- Cost: $2-10/month
  - Input: $0.00025/1K tokens
  - Output: $0.00125/1K tokens

#### Security & Secrets
**AWS Secrets Manager**
- Database credentials
- API keys
- Automatic rotation
- Cost: $0.40/20 secrets/month

**AWS IAM**
- Roles for ECS tasks
- Policies with least privilege
- Service-to-service authentication
- Cost: Free

#### Monitoring & Logging
**Amazon CloudWatch**
- Logs: ECS, ALB, RDS DB
- Metrics: CPU, Memory, Latency
- Alarms: Auto-scaling triggers
- Dashboards: Real-time monitoring
- Cost: $5-10/month (5GB free tier)

**AWS CloudTrail**
- API call auditing
- Compliance logging
- Cost: Free (management events)



### 3.2 Component Design

#### High-Level Architecture
![image architech](/images/Proposal/Containerized-and-Scalable-Web-Application.drawio.png)

#### Component Interactions

**1. Authentication Flow**
```
User → CloudFront → Cognito: Sign Up/In
Cognito → User: JWT Tokens (Access, ID, Refresh)
User → API Gateway: Request + JWT
API Gateway → Cognito: Verify JWT
API Gateway → ALB → Django: Forward (if valid)
Django → RDS: Query user data
Django → User: Response
```

**2. Chat Flow**
```
User → API Gateway: POST /api/chat/ + JWT
API Gateway → Django: Forward
Django → RDS: Get user profile
Django → RDS: Save user message
Django → Bedrock: Call Claude 3 + profile context
Bedrock → Django: Stream response (SSE)
Django → User: Stream tokens
Django → RDS: Save AI response
```

**3. Profile Management**
```
User → API Gateway: PUT /api/users/profile/ + JWT
API Gateway → Django: Forward
Django → RDS: Update user profile
Django → User: Success response
```



#### Security Layers

**Layer 1: API Gateway**
- Verify JWT before request reaches backend
- Rate limiting: 1000 requests/second
- Throttling: 500 requests/second per user
- CORS configuration

**Layer 2: Django Backend**
- User authorization checks
- Input validation
- Business logic enforcement
- SQL injection prevention (ORM)

**Layer 3: VPC Network**
- Private subnets for backend
- No public IPs for ECS tasks
- Security Groups: Only allow necessary traffic
- NACLs: Network-level firewall

**Layer 4: Database**
- RDS in private subnet
- Encryption at rest (AES-256)
- Encryption in transit (TLS)
- Automated backups
- IAM database authentication

#### Data Flow

**User Data Storage**
```
AWS Cognito User Pool
    ↓ (cognito_sub)
users_userprofile (RDS)
    ↓ (cognito_sub)
chat_conversation (RDS)
    ↓ (conversation_id)
chat_message (RDS)
```

**Data Encryption**
- **At Rest**: RDS encryption, S3 encryption
- **In Transit**: TLS 1.2+ for all connections
- **Application**: Django password hashing (PBKDF2)



---

## 4. TECHNICAL IMPLEMENTATION

### 4.1 Implementation Phases

#### Phase 1: Research & Planning (Week 7)

**Objective**: Determine what the project is about, clarify project purpose, and identify problems to solve.

**Tasks**:
- Determine what the project is about
- Identify user base, needs, and pain points
- Proposed solution and value delivered
- Gather and consolidate requirements from documentation and mentors
- Review main use cases of the application

---

#### Phase 2: Research & Architecture Planning (Week 8)

**Objective**: Clarify project purpose, identify problems to solve, project scope, and design system architecture.

**Tasks**:
- Research appropriate cloud architecture for the product
- Design preliminary system architecture on AWS
- Consult with mentors
- Update design based on feedback
- Prepare architecture diagram
- Draft project plan & timeline

---

#### Phase 3: Build FE and BE (Week 9)

**Objective**: Build user interface (UI) with Vue.js and build backend API with Django

**Tasks**:
- Build web pages (Landing Page, Sign Up, Sign In, Verify Email, Forgot Password)
- Create personal information management interface (Profile Management)
- Build Chat interface
- Handle error states in interface
- Set up Django REST Framework
- Create User Profile model
- Build Authentication API (JWT) using Amazon Cognito
- Build Profile management API (GET/PUT)
- Build API to create conversations & send messages

#### Phase 4: Set up Infrastructure and Deploy Application (Week 10)

**Objective**: Set up AWS infrastructure with Terraform and deploy to AWS

**Tasks**:
- Write Terraform modules for VPC, subnets, security groups
- Deploy frontend to S3 bucket
- Create CloudFront distribution for frontend (S3 + CDN)
- Set up AWS Cognito User Pool and App Client
- Containerize Django backend with Docker
- Set up ECS Fargate cluster with auto-scaling (1-4 tasks)
- Set up API Gateway with JWT Authorizer (Cognito integration)
- Configure Application Load Balancer
- Configure VPC Endpoints
- Configure CORS for API Gateway and Django
- Set up CloudWatch Logs and Alarms
- Test end-to-end authentication flow

---

#### Phase 5: AI & Database Integration (Week 11)

**Objective**: Integrate AWS Bedrock (Claude 3 Haiku) for AI chat feature and set up PostgreSQL database on AWS RDS

**Tasks**:
- Set up AWS Bedrock and request model access (Claude 3 Haiku)
- Build Bedrock client supporting streaming (SSE)
- Integrate AI into Chat API with conversation context awareness
- Set up PostgreSQL database on AWS RDS (Multi-AZ)
- Create database models (UserProfile, Conversation, Message)
- Test AI responses based on user profile
- Optimize prompt engineering for nutrition advice

---

#### Phase 6: Testing and Report Writing (Week 12)

**Objective**: Comprehensive testing and project documentation

**Tasks**:
- Integration testing for authentication flow
- End-to-end testing for chat functionality
- Load testing and stress testing
- Cross-browser testing (Chrome, Firefox, Safari, Edge)
- Responsive testing on mobile devices (iOS, Android)
- Write project report




### 4.2 Technical Deployment

*Deployment Process*: The project is deployed in 6 phases over 6 weeks to build a complete AI nutrition assistant platform.

- Week 7 – Research & Planning
- Week 8 – Architecture Planning
- Week 9 – Frontend & Backend Development
- Week 10 – Infrastructure & Deployment
- Week 11 – AI & Database Integration
- Week 12 – Testing & Documentation

*Technical Requirements*

System deployment will follow each layer: Networking (VPC, Subnets, VPC Endpoints) → Security (Cognito, IAM, Secrets Manager) → Compute (ECS Fargate) → Load Balancing (ALB, API Gateway) → Storage & Database (S3, RDS PostgreSQL) → AI Integration (Bedrock) → Logging/Monitoring (CloudWatch) → CDN & Optimization (CloudFront).

AI Nutrition Platform: Practical knowledge of CloudFront (distributing Vue.js frontend), S3 (storing static assets), API Gateway (HTTP API with JWT Authorizer), ECS Fargate (running Django backend with 1-4 task auto-scaling), RDS PostgreSQL (Multi-AZ, 20GB), Bedrock (Claude 3 Haiku for AI chat), Cognito (managing user authentication), and VPC Endpoints (6 endpoints: Bedrock, Secrets Manager, ECR, CloudWatch, S3). Use Terraform for infrastructure as code management (e.g., VPC endpoints for Bedrock, ECS task definitions, API Gateway routes). Django REST Framework handles business logic and minimizes Lambda dependencies. Vue.js + Vite for fullstack web application with real-time streaming.

## 5. Project Timeline and Milestones

## Project Timeline (6 Weeks)

| Week | Phase                       | Main Content                                                                 |
|------|----------------------------------|---------------------------------------------------------------------------------|
| 7    | Research & Planning              | - Determine project objectives<br>- Identify users & pain points<br>- Gather requirements<br>- Identify main use cases |
| 8    | Architecture Planning            | - Research AWS architecture<br>- Design system architecture<br>- Review with mentors<br>- Finalize architecture diagram<br>- Draft deployment plan |
| 9    | FE & BE Development              | - Build UI (Landing, Sign Up, Sign In, Verify Email, Forgot Password)<br>- Profile Management UI<br>- Chat UI with error handling<br>- Set up Django REST Framework<br>- User Profile Model<br>- Auth API (Cognito + JWT)<br>- Profile API (GET/PUT)<br>- Chat & Conversation API |
| 10   | Infrastructure & Deployment     | - Write Terraform for VPC, Subnets, Security Groups<br>- Deploy frontend S3 + CloudFront<br>- Set up Cognito User Pool<br>- Containerize backend<br>- ECS Fargate + Auto-scaling<br>- API Gateway + JWT Authorizer<br>- Configure ALB and VPC Endpoints<br>- Set up CloudWatch Logs & Alarms<br>- Test end-to-end |
| 11   | AI & Database Integration       | - Set up AWS Bedrock & model access<br>- Bedrock client + SSE streaming<br>- Integrate AI into Chat API<br>- Context-aware conversation<br>- Set up PostgreSQL RDS (Multi-AZ)<br>- Database models & migration<br>- Test AI based on user profile<br>- Optimize prompt engineering |
| 12   | Testing & Report                | - Integration testing<br>- End-to-end testing<br>- Load & stress testing<br>- Cross-browser testing<br>- Responsive test (iOS, Android)<br>- Write project report |



---

## 6. BUDGET ESTIMATION

### 6.1 Infrastructure Costs

#### Monthly Recurring Costs

| Service | Configuration | Cost/Month | Notes |
|---------|--------------|------------|-------|
| **ECS Fargate** | 1-4 tasks, 0.5 vCPU, 1GB RAM | $15-30 | Auto-scaling based on load |
| **RDS PostgreSQL** | db.t3.micro, Multi-AZ, 20GB | $15-25 | Includes automated backups |
| **API Gateway** | HTTP API, ~1M requests | $3-10 | $1/million requests |
| **CloudFront** | ~100GB transfer | $1-5 | First 1TB free tier |
| **S3** | ~5GB storage, ~10K requests | $1 | Static website hosting |
| **VPC Endpoints** | 2 endpoints (Bedrock, Secrets) | $7 | $0.01/hour per endpoint |
| **Secrets Manager** | 2 secrets | $1 | $0.40/secret/month |
| **CloudWatch** | Logs, Metrics, Alarms | $5-10 | 5GB free tier |
| **Bedrock AI** | Claude 3 Haiku | $2-10 | Usage-based pricing |

#### AI Usage Costs (Bedrock)

| Usage Level | Messages/Day | Input Tokens | Output Tokens | Cost/Month |
|-------------|--------------|--------------|---------------|------------|
| **Low** | 100 | 50K | 100K | $0.40 |
| **Medium** | 500 | 250K | 500K | $2.00 |
| **High** | 2,000 | 1M | 2M | $8.00 |
| **Very High** | 10,000 | 5M | 10M | $40.00 |

**Pricing**:
- Input: $0.00025 per 1K tokens
- Output: $0.00125 per 1K tokens

### 6.2 Cost Optimization Strategies

#### Immediate Optimizations

**1. Reserved Instances** (-30% RDS cost)
- 1-year commitment: 30% reduction
- 3-year commitment: 50% reduction
- Apply when traffic is stable

**2. S3 Lifecycle Policies** (-50% storage cost)
- Move old logs to S3 Glacier after 30 days
- Delete logs after 90 days
- Reduce storage cost

---

## 7. RISK ASSESSMENT

### 7.1 Risk Matrix

| Risk                          | Probability | Impact | Severity | Mitigation |
|-------------------------------|----------|-----------|---------------------|-----------------------|
| AWS Service Outage            | Low     | High       | Medium         | Deploy Multi-AZ, setup monitoring |
| Database Error                | Low     | High       | Medium         | RDS Multi-AZ, automated backups |
| Security Risk                 | Low     | Very High  | High                | Multi-layer security, data encryption |
| Budget Overrun                | Medium  | Medium     | Medium         | Setup CloudWatch billing alarms, budget limits |
| Performance Issues            | Medium  | Medium     | Medium         | Load testing, auto-scaling |
| Data Loss                     | Low     | Very High  | High                | Automated backups, Point-in-time Recovery |

**Severity Rating Scale**
- Low: Minor impact, easy to handle
- Medium: Moderate impact, requires monitoring and handling
- High: Serious impact, requires immediate action


### 7.2 Risk Mitigation Strategies

#### Technical Risks

**1. AWS Service Outage**

- **Mitigation**:
  - Deploy Multi-AZ for RDS and ECS
  - Set up CloudWatch alarms to monitor service status
  - Enable automatic failover

**2. Database Error**

- **Mitigation**:
  - Use RDS Multi-AZ with automatic failover
  - Support Point-in-time Recovery (7 days)
  - Snapshot database before each deployment

**3. Security Risk**

- **Mitigation**:
  - Apply multi-layer security (API Gateway, Django, VPC)
  - Encrypt data at rest and in transit
  - Conduct regular security checks
  - CloudTrail for audit logging

**4. Performance Degradation**

- **Mitigation**:
  - Setup auto-scaling for ECS tasks (1-4 tasks)
  - CloudWatch alarms for high CPU/memory
  - Load testing before launch
  - CDN caching for static assets
  - Optimize database queries

#### Business Risks

**1. Budget Overrun**

- **Mitigation**:
  - Setup CloudWatch billing alarms
  - Configure AWS Budget alerts
  - Review costs monthly
  - Use Reserved Instances when traffic stabilizes
  - Regular cost analysis and optimization

**2. Low User Adoption**

- **Mitigation**:
  - Launch MVP with core features
  - Gather user feedback
  - Continuous improvement cycles
  - Simple marketing campaigns
  - Free tier to attract users

**3. Poor AI Quality**

- **Mitigation**:
  - Optimize prompt engineering and testing
  - User feedback mechanism
  - A/B testing with different prompts
  - Manual support fallback if needed
  - Continuous improvement

### 7.3 Contingency Plans

#### Plan A: Normal Operation

- All services operating stably
- Auto-scaling handling load
- Alert system functioning properly


#### Plan B: High Traffic

**Triggered when**: > 500 concurrent users
- Increase number of ECS tasks
- Upgrade RDS
- Enable strong caching on CloudFront


#### Plan C: Service Degradation

**Triggered when**: AWS service encounters issues
- Activate Multi-AZ failover
- Shift traffic to working AZ
- Display system status page


#### Plan D: Complete Outage

**Triggered when**: Regional AWS outage
- Activate disaster recovery plan
- Restore from backups
- Deploy to another region


#### Plan E: Budget Overrun

**Triggered when**: Cost > budget
- Review and optimize resources
- Reduce number of ECS tasks
- Disable non-essential features
- Implement strict rate limiting

---

## 8. EXPECTED OUTCOMES

### 8.1 Technical Improvements

#### Performance Metrics

**Availability**

- Target: 99.9% uptime (maximum 43 minutes downtime/month)
- Multi-AZ deployment
- Automatic failover
- Health checks
- Reduced response time

**Scalability**

- Auto-scaling: 1-4 ECS tasks
- Support 1,000 concurrent users
- 10,000 requests/minute
- 100 concurrent database connections

**Security**

- No security incidents reported
- 100% HTTPS traffic
- Data encrypted at rest and in transit

### 8.2 Long-term Value

#### Technical Value

**Reusable Infrastructure**

- Terraform modules reusable for other projects
- CI/CD pipeline templates
- Monitoring system templates
- Security best practices library

**Knowledge Documentation**

- AWS architecture patterns
- AI integration experience
- Performance optimization lessons
- Cost optimization strategies

**Team Skills**

- AWS expertise
- AI/ML integration in products
- Modern web development experience

#### Strategic Value

**Foundation for Expansion**

- Can expand to:
  - Meal plan service
  - Recipe marketplace
  - Fitness tracking application
  - Telemedicine integration


**Data Assets**

- User nutrition preferences
- Frequently asked food questions
- Effective meal plans
- Market insights


---

## 9. CONCLUSION

### 9.1 Summary

**Technical Aspects**

- Modern cloud-native architecture
- Ensures high availability and scalability
- Adheres to security standards
- Ready for real-world product deployment

**Business Aspects**

- Reduced operational costs
- Scalable business model

**User Value**

- AI-powered nutrition consultation
- Personalized recommendations based on nutrition profile
- Simple, easy-to-use, accessible interface
