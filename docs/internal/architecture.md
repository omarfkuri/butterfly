# Software Architecture Document
**PROJECT:** Butterfly Web Application
**VERSION:** 1.0.0
**DATE:** April 2026

---

# Table of Contents

- [[#1. Introduction]]
	- [[#1.1 Overview]]
	- [[#1.2 Definitions]]
- [[#2. Project Structure]]
- [[#3. High-Level System]]
	- [[#3.1 Diagram]]
	- [[#3.2 Pattern]]
- [[#4. Core Components]]
	- [[#4.1 Frontend]]
	- [[#4.2 Services]]
	- [[#4.3 Infrastructure]]
- [[# 5. Data Stores]]
	- [[#5.1 Users Database]]
	- [[#5.2 Posts Database]]
	- [[#5.3 Interactions Database]]
	- [[#5.4 Projection Database]]
- [[#6. External Integrations]]
	- [[#6.1 Image Storage]]
- [[#7. Deployment & Infrastructure]]
- [[#8. Network Topology & Service Exposure]]
	- [[#8.1 Public Layer]]
	- [[#8.2 Application Layer]]
	- [[#8.3 Data Layer]]
- [[#9. Security]]
- [[#10. Development & Testing]]
	- [[#10.1 Development Strategy]]
	- [[#10.2 Testing Strategy]]
- [[# 11. API Specification]]
	- [[#11.1 HTTP]]
	- [[#11.2 WebSocket]]
	- [[#11.3 Domain Entities]]
	- [[#11.4 Internal Contracts]]

---
# 1. Introduction
## 1.1 Overview
This document defines the structure of the **Butterfly** application. It details how the [[requirements]] are to be implemented.
## 1.2 Definitions
- **DTO:** Data Transfer Object
- **SDK:** Software Development Kit
- **GC:** Google Cloud
- **SSR:** Server Side Renderer
- **CQRS:** Command Query Responsibility Segregation

---
# 2. Project Structure

```
root/
├── libraries/
│   ├── user-contract/
│   ├── post-contract/
│   ├── interaction-contract/
│   └── content-parsing/
│
├── services/
│   ├── api-gateway/
│   ├── user-service/
│   ├── post-service/
│   ├── interaction-service/
│   └── projection-service/
│
├── front/
│   └── web/
│
├── infra/
│   ├── base/
│   │   ├── kafka/
│   │   ├── redis/
│   │   ├── nginx/
│   │   └── observability/
│   │       ├── otel/
│   │       ├── loki/
│   │       ├── grafana/
│   │       ├── tempo/
│   │       └── mimir/
│   │
│   └── environments/
│       ├── local/
│       │   └── k8s/
│       │
│       └── production/
│           └── k8s/
│
├── db/
│   ├── user-db/
│   ├── post-db/
│   ├── interaction-db/
│   └── projection-db/
│
├── docs/
│   ├── user/
│   │   └── functionality.md
│   │
│   └── internal/
│       ├── requirements.md
│       ├── architecture.md
│       └── tasks.md
│
├── contract/
│   ├── domain/
│   │   ├── user.yml
│   │   ├── post.yml
│   │   └── interaction.yml
│   │
│   ├── public/
│   │   ├── rest.yml
│   │   └── events.yml
│   │
│   └── internal/
│       ├── events/
│       │   ├── user.yml
│       │   ├── post.yml
│       │   └── interaction.yml
│       │
│       └── rest/
│           ├── user.yml
│           ├── post.yml
│           └── interaction.yml
│
├── .github/
│   └── workflows/
│       ├── integrate.yml
│       └── deploy.yml
│
├── scripts/
│   ├── tests/
│   │   ├── unit.sh
│   │   ├── integration.sh
│   │   ├── contract.sh
│   │   ├── end-to-end.sh
│   │   └── performance.sh
│   │
│   ├── develop.sh
│   └── deploy.sh
│
├── .gitignore
├── docker-compose.yml
└── README.md
```

---
# 3. High-Level System

## 3.1 Diagram
```
┌──────────┐          ┌───────┐
│ INTERNET ├─ HTTPS ─▶│ NGINX │
└──────────┘          └───┬───┘
						  │
		┌──── HTTPS ──────┴─────┐
		│	                    │
		▼	                    ▼
┌────────────┐           ┌─────────────┐    ┌───────┐
│ SVELTE KIT ├── HTTPS ─▶│ API GATEWAY ├───▶│ REDIS │
└────────────┘           └──────┬──────┘    └───────┘
							    │
	    ┌───────── HTTPS ────┬──┴────────── HTTPS ──────┬──────────┐
        │                    │                          │          │
        ▼                    ▼                          ▼          │
  ┌──────────┐          ┌──────────┐          ┌─────────────────┐  │
  │ USER SVC ├─ Kafka ─▶│ POST SVC ├─ Kafka ─▶│ INTERACTION SVC │  │
  └┬───┬────┬┘          └┬───┬───┬─┘          └─┬──────────┬────┘  │
   │   │    │            │   │   │              │          │       │
   │   │  HTTPS        HTTPS │ HTTPS          HTTPS        │       │
   │   │    │            │   │   │              │          │       │
   │   │    ▼            │   │   ▼              │          │       │
   │   │  ┌───────┐      │   │ ┌────────────┐   │          │       │
 HTTPS │  │ EMAIL │      │   │ │ GC Storage │   │          │       │
   │   │  └───────┘      ▼   │ └────────────┘   ▼          │       │
   ▼   └────┐    ┌─────────┐ │          ┌────────────────┐ │       │
┌─────────┐ │    │ POST DB │ │          │ INTERACTION DB │ │       │
│ USER DB │ │    └─────────┘ │          └────────────────┘ │       │
└─────────┘ │                │                             │       │
            └─── Kafka ──────┴──────────┬──── Kafka ───────┘       │
                                        │                          │
                                        ▼                          │
┌───────────────┐               ┌────────────────┐                 │
│ PROJECTION DB │ ◀─── HTTPS ───┤ PROJECTION SVC │◀─── HTTPS ──────┘
└───────────────┘               └────────────────┘
```

## 3.2 Pattern
- The system follows a CQRS architecture pattern.
- Write operations are handled by domain services (User, Post, Interaction).
- Domain events are published to Kafka and consumed by the Projection Service to maintain read-optimized DTO views.

---
# 4. Core Components
## 4.1 Frontend
### 4.1.1 Web App
- **Responsibilities:** 
	- Serve web application.
	- SSR
- **Technologies:** 
	- SvelteKit
	- NodeJS
	- TypeScript
	- LESS CSS
## 4.2 Services
Services communicate synchronously through REST for command execution and asynchronously through Kafka for event propagation and projection updates.

## 4.2.1 Command Services
Each service independently owns its database schema and publishes domain events to Kafka.
#### 4.2.1.1 User Service
- **Responsibilities:**
	- Create and delete user accounts.
	- Update user account and profile information.
	- Retrieve user information for auth.
	- Verify passwords.
- **Technologies**: Spring Boot, Spring Web
#### 4.2.1.2 Post Service
- **Responsibilities:**
	- Create and delete posts.
	- Update posts.
	- Handle replies.
	- React to user creation and deletion.
- **Technologies:** Spring Boot, Spring Web
#### 4.2.1.3 Interaction Service
- **Responsibilities:**
	- Like and unlike posts.
	- Follow and unfollow users.
	- React to user creation and deletion.
	- React to post creation and deletion.
- **Technologies:** Spring Boot, Spring Web
### 4.2.2 Query Service
- **Responsibilities:**
	- React to user events.
	- React to post events.
	- React to interaction events.
	- Create DTOs for faster reads.
	- Update DTOs from events.
	- Get DTOs for post listings, user listings using pagination.
	- Allow searching for users and posts.
	- Connect with clients to provide real time updates.
- **Technologies:** Spring Boot, Spring Web
## 4.3 Infrastructure
### 4.3.1 API Gateway
- **Responsibilities:**
	- Handles authentication.
	- Connects requests with services.
- **Technologies**: Spring Boot, Spring Cloud Gateway
### 4.3.2 Reverse Proxy
- **Responsibilities:**
	- Primary interface of application to the public.
	- Handles load balancing.
	- Routes requests to website or API gateway.
- **Technologies:** NGINX
### 4.3.3 Distributed Event Streaming Platform
- **Responsibilities:**
	- Gather domain events.
	- Publish domain events to subscribers.
- **Technologies:** Kafka
### 4.3.4 In-Memory Data Store (Redis)
- **Responsibilities:**
	- Distributed rate limiting state for API Gateway.
- **Technologies:**
	- Redis
### 4.3.5 Container Orchestration
- **Responsibilities:**
	- Coordinate containers.
	- Define internal network architecture.
- **Technologies:** Kubernetes, Docker
### 4.3.6 Observability Strategy
The system defines a unified observability strategy based on **traces, metrics, and logs**, ensuring full visibility across synchronous (HTTP) and asynchronous (Kafka) communication.

- **Responsibilities:**
	- Gather logs and metrics from all services.
	- Present them in a graphical interface.
- **Technologies:** 
	- Prometheus
	- Loki
	- OpenTelemetry
	- Grafana
	- Mimir
#### 4.3.6.1 Tracing Strategy (OpenTelemetry)
**Scope of tracing:**
- All incoming HTTP requests at API Gateway
- Inter-service HTTP communication
- Kafka message production and consumption
- Database interactions (queries and transactions)
- External integrations (GC Storage, Email service)

**Trace boundaries:**
- A single trace represents a full user request lifecycle
- Traces originate at the API Gateway
- Trace context is propagated:
	- Via HTTP headers between services
	- Via Kafka message headers for asynchronous flows

**Span structure:**
- Root span: API Gateway request
- Child spans:
	- Service-level request handling
	- Database operations
	- External service calls
	- Kafka publish/consume operations

**Context propagation:**
- Standard W3C Trace Context is used
- All services are required to forward trace headers

**Sampling strategy:**
- Development: 100% sampling
- Production: configurable sampling rate (default 10%)
- Critical endpoints may override sampling to ensure trace capture

#### 4.3.6.2 Logging Strategy
**Logging principles:**
- All services log to standard output (stdout)
- Logs are treated as event streams and collected externally
- No file-based logging inside containers

**Log format:**
- Structured JSON logging
- Each log entry must include:
	- Timestamp
	- Log level
	- Service name
	- Message
	- Trace ID
	- Span ID (if available)

**Log levels:**
- ERROR: system failures
- WARN: unexpected but non-fatal behavior
- INFO: business-relevant events
- DEBUG: development-only diagnostics

**Log correlation:**
- Logs must include trace identifiers to correlate with distributed traces

#### 4.3.6.3 Metrics Strategy
**Metrics collection:**
- All services expose Prometheus-compatible metrics endpoints

**Core metrics:**
- HTTP request count, latency, error rate
- Kafka producer/consumer throughput and lag
- Database query latency
- JVM metrics (memory, CPU, threads)

**Aggregation:**
- Metrics are scraped by Prometheus
- Long-term storage is handled by Mimir

#### 4.3.6.4 Observability Architecture
**Flow:**
- Applications → OpenTelemetry (traces + metrics) → collectors
- Logs → stdout → log collector → Loki
- Metrics → Prometheus → Mimir (long-term storage)
- Traces → Tempo

**Visualization:**
- Grafana provides unified dashboards for:
	- Metrics
	- Logs
	- Traces

#### 4.3.6.5 Design Constraints
- Observability must not introduce significant latency
- All instrumentation should favor auto-instrumentation where possible
- Observability components are isolated within the internal network layer

## 4.4 Shared Libraries
### 4.4.1 Contract Libraries
Each command service will share a library with the projection service to provide the same types for events.
### 4.4.2 Content Parsing Library
A common content parsing library is imported by user service to parse biographies and by post service to parse post content.

# 5. Data Stores

## 5.1 Users Database
- **Purpose:** 
	- Stores user account and profile information.
	- Stores email verification tokens.
- **Type:** MySQL
## 5.2 Posts Database
- **Purpose:** Stores posts and reply relationships.
- **Type:** MySQL
## 5.3 Interactions Database
- **Purpose:** Stores likes and follows.
- **Type:** MySQL
## 5.4 Projection Database
- **Purpose:** Stores DTOs.
- **Type:** MySQL

---
# 6. External Integrations
## 6.1 Image Storage
- **Name:** GC Storage
- **Purpose:** Image storage and hosting
- **Integration Method:** SDK
## 6.2 Mail Service
- **Name:** GMail
- **Purpose:** Email sending
- **Integration Method:** HTTP

---
# 7. Deployment & Infrastructure
- **Cloud Provider:** 
	- GC
- **Infrastructure:** 
	- Kafka
	- NGINX (Ingress controller)
	- Kubernetes
	- Docker
	- Databases as Kubernetes StatefulSets
	- Redis
- **Services Used:** 
	- GC Storage
	- Google Kubernetes Engine (GKE Autopilot).
- **CI/CD Pipeline:** 
	- Github Actions
- **Observability & Monitoring**: 
	- Prometheus
	- Loki
	- OpenTelemetry
	- Grafana
	- Mimir

# 8. Network Topology & Service Exposure
The system follows a layered internal network exposure model implemented through Kubernetes Services and NetworkPolicies.
## 8.1 Public Layer
Accessible from the internet via ingress controller:
- Frontend SSR service
- API Gateway

Responsibilities:
- User interaction
- Authentication entry point
- External API access

## 8.2 Application Layer
Services are accessible only inside the Kubernetes cluster.

Communication model:
- REST via API Gateway
- Event streaming via Kafka

## 8.3 Data Layer
Accessible only by owning services:
- Databases
- Kafka brokers
- Redis

## 8.4 Observability Layer
Accessible only internally.

---
# 9. Security
- **Authentication:** JWT
- **Protocol:** HTTPS
- **Data Encryption:**
	- **In Transit:** TLS
	- **At Rest:** 
		- **Passwords:** BCrypt hashing
		- **Database storage:** Encrypted
- **Rate Limiting**
	- **Global**: 120 requests per minute
	- **Authentication**: 5 requests per minute
	- **Email Verification**: 1 request per hour
	- **Post Creation/Update/Deletion**: 10 requests per minute
	- **Interactions (Like, Follow)**: 30 requests per minute
	- **Read Operations**: 100 requests per minute

# 10. Development & Testing
## 10.1 Development Strategy
Local development uses Docker Compose to provide a reproducible service environment consistent with production infrastructure topology.

Containers that allow it should reload automatically for faster development.

---
## 10.2 Testing Strategy
The system follows a layered automated testing strategy.

### 10.2.1 Unit Tests
Validate internal service logic and domain behavior.
Executed during CI integration stage.

**Technologies:**
- Spring Boot Test
- Vitest
- Storybook

### 10.2.2 Integration Tests
Validate service-to-service communication and infrastructure interaction.
Executed during CI pipeline validation.

**Scope:**
- REST communication via API Gateway
- Kafka event publication and subscription
- database persistence behavior
- projection update correctness

**Technologies:**
- Spring Boot Test
- Testcontainers
- Kafka Testcontainers
- MySQL Testcontainers
- Playwright

### 10.2.3 Contract Tests
Validate compatibility between services and shared API/event specifications.

**Technologies:**
- Spring Cloud Contract
- OpenAPI validation tooling

### 10.2.4 End-to-End Tests
Validate full user workflows across system boundaries.
Executed before production releases.

**Scope includes:**
- Authentication
- Post lifecycle
- Interaction workflows
- Timeline rendering

**Technologies:**
- Playwright

### 10.2.5 Performance Tests
Validate throughput and latency characteristics of critical system components.
Executed periodically and before production deployment.

**Scope:**
- API Gateway throughput
- Kafka event throughput
- Projection update latency

**Technology:**
- k6

---
# 11. API Specification
## 11.1 HTTP
The system exposes a REST api defined in [[/contracts/public/rest.yml]].
## 11.2 WebSocket
The system allows web socket communication as defined in [[/contracts/public/websocket.yml]].
## 11.3 Domain Entities
The system allows web socket communication as defined in [[/contracts/domain]].
## 11.4 Internal Contracts
The system defines internal contracts at [[/contracts/internal]].


