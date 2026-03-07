Product Requirements Document (PRD)
Project Name: Enterprise Loan Management System (ELMS)

## 1.Project Overview

## Objective:
Develop a full-featured, enterprise-level loan management system using open-source technologies, 
Java Spring Boot, Gradle, and DevOps best practices. The system will handle loan applications, approvals, and
reporting for a banking environment while supporting CI/CD, containerization, and cloud orchestration.

## Key Goals:**
1. Enable loan applications, tracking, and approvals
2. Enforce enterprise-grade RBAC and SoD policies
3. Implement CI/CD with Gradle and automated testing
4. Containerized deployment via OpenShift / OKD
5. Ensure observability via logging and monitoring
6. Enable rollback and artifact versioning for safe production releases

## Stakeholders:**
1. Bank customers (loan applicants)
2. Bank administrators and loan officers
3. IT and DevOps teams

## Technology Stack
| #  | Layer / Category          | Technology                              |
|----|---------------------------|-----------------------------------------|
| 1  | Backend                   | Java Spring Boot                        |
| 2  | Frontend                  | React                                   |
| 3  | Database                  | PostgreSQL                              |
| 4  | Identity & Access Mgmt    | Keycloak                                |
| 5  | Workflow Engine           | Camunda BPM                             |
| 6  | Messaging                 | Apache Kafka                            |
| 7  | CI/CD                     | Jenkins / GitHub Actions                |
| 8  | Artifact Repository       | JFrog Artifactory OSS / Nexus           |
| 9  | Containerization          | Docker                                  |
| 10 | Orchestration             | OpenShift / OKD                         |
| 11 | Logging & Monitoring      | ELK Stack + Prometheus / Grafana        |
| 12 | Code Quality              | SonarQube                               |


## 2.Functional Requirements
##### 2.1 User Management
 User registration and login via Keycloak 
 Role-based access control (RBAC) for Admin, Loan Officer, Customer
 Role separation for SoD compliance

##### 2.2 Loan Application
 Submit new loan applications
 View application status
 Attach required documents (PDF, images)
 Automatic validation of application fields

##### 2.3 Loan Approval Workflow
 Multi-level approval workflow via Camunda BPM
 Notifications via Kafka (email / SMS triggers)
 Audit trail of all approval actions

##### 2.4 Reporting
 Generate loan status reports (PDF/CSV)
 Transactional audit reports
 Dashboard metrics for admins (loan count, approvals, pending)

##### 2.5 Security & Compliance
 RBAC and SoD via Keycloak integration
 Secure communication (HTTPS)
 Audit logging of all user and system actions
 Sensitive data encryption at rest and in transit

##### 2.6 DevOps & CI/CD
 Gradle build pipeline
 Automated unit, integration, regression tests
 SonarQube static code analysis
 Artifact repository for JARs and Docker images
 Deployment to OpenShift / OKD with namespaces (DEV/TEST/UAT/PROD)
 Automated rollback support using artifact versioning

##### 2.7 Observability
 Logging: ELK Stack
 Metrics: Prometheus + Grafana
Alerts on system failures or threshold breaches

## 3.Non-Functional Requirements
 Performance: Handle 50,000 concurrent users
 Scalability: Auto-scaling via OpenShift
 Availability: 99.9% uptime SLA for production
 Security: OWASP compliance, SAST via SonarQube, encryption
 Maintainability: Modular microservice architecture
 Auditability: All actions logged for regulatory compliance

## 4.System Architecture
 Microservices deployed in Docker containers
 OpenShift / OKD orchestrates containers across environments
 CI/CD pipeline integrates with artifact repository and SonarQube
 PostgreSQL stores transactional data and audit logs
 Kafka handles messaging and notifications
 Camunda BPM manages approval workflows
 Keycloak enforces authentication, RBAC, and SoD policies
 Logging and monitoring via ELK + Prometheus/Grafana

## 5.Environment Overview
| Environment  | Purpose                            | Access Level   | Monitoring               |
|--------------|------------------------------------|----------------|--------------------------|
| DEV          | Feature development & unit testing | Developers     | Basic logging            |
| TEST         | Integration & regression testing   | QA Team        | Centralized logging      |
| UAT          | Business validation & approval     | Business Users | Monitored                |
| PROD         | Live production services           | Restricted     | Full monitoring & alerts |
 
## 6.CI/CD Pipeline Flow
 Commit code to Git repository
 Gradle build and unit/integration tests
 SonarQube static code analysis
 Build Docker image
 Push artifacts to Artifactory / Nexus
 Deploy container to OpenShift DEV namespace
 Run automated regression tests
 Promote artifact to TEST → UAT → PROD with rollback support

## 7. Testing Strategy
 Unit Tests: JUnit + Mockito
 Integration Tests: Spring Boot Test + Testcontainers
 Regression Tests: Selenium / Cypress
 Performance Tests: JMeter / Gatling 
 Security Tests: OWASP ZAP / SonarQube SAST
 UAT: Manual testing by business users

## 8. Rollback Strategy
 Previous artifact versions stored in Artifactory/Nexus
 OpenShift redeploys previous stable version on failure
 Minimal downtime using rolling updates / blue-green deployment

## 9. Deliverables
 Complete source code repository
 Docker images in artifact repository / container registry
 CI/CD pipeline scripts and configuration
 SonarQube analysis reports
 OpenShift deployment manifests
 User manuals and admin guides
 Test cases and test reports
 Audit and logging configuration

## 10. Optional Enhancements
 Multi-tenant support for multiple banks
 Feature flags for new modules
 Advanced analytics dashboard
 Integration with external banking APIs

## 11. References Documentation
- **Spring Boot Documentation** - https://docs.spring.io/spring-boot/index.html
- **Gradle User Guide** — https://docs.gradle.org/current/userguide/userguide.html
- **OpenShift / OKD Documentation** — https://docs.okd.io/
- **Keycloak Documentation** — https://www.keycloak.org/documentation
- **Camunda BPM Documentation** — https://docs.camunda.io/
- **Nexus Repository Documentation** — https://books.sonatype.com/sonatype-clm-book/1.29/pdf/book-clm.pdf
- **SonarQube Documentation (including IntelliJ setup)** — https://docs.sonarsource.com/