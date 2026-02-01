#Requirements 
## Smart Resource Allocation & Load Prediction System (Fluxerratic)

**Problem Statement ID:** 01  
**Theme:** Smart Automation / AI  
**Team Name:** SASSY CODERS  
**Version:** 1.0  
**Date:** 25 JAN 2026  

---

## 1. Project Overview
Many government and public-service digital platforms face heavy server load during peak hours due to high user traffic. This often causes slow response times, downtime, and poor user experience. Most systems react only after failure occurs instead of predicting load in advance.

This project proposes a smart system that monitors traffic patterns, predicts upcoming load, and dynamically allocates resources to ensure smooth, uninterrupted service.

---

## 2. Objectives
- Monitor real-time traffic and system usage.
- Reduce downtime and improve response time.
- Allocate resources automatically based on predicted load.
- Provide an admin dashboard for monitoring and control.
- Improve scalability to handle peak user loads.
- Ensure data security and confidentiality of sensitive information.
- Generate predictive analytics for proactive system management.
- Maintain high availability and reliability.

---

## 3. Stakeholders
- **End Users:** Citizens using the platform/services.
- **System Administrator:** Monitors performance and controls configurations.
- **Government Authority:** Uses reports and performance insights.
- **Cloud/Infrastructure Team:** Maintains deployment and scaling.
- **AI Prediction Module:** Predicts load and triggers scaling decisions.

---

## 4. Scope
### 4.1 In Scope
- Real-time monitoring of traffic and server performance.
- AI-based load prediction using historical + live data.
- Auto-scaling / resource allocation logic.
- Admin dashboard with graphs, alerts, and analytics.
- Logging and reporting for performance evaluation.

### 4.2 Out of Scope
- Full cloud provider billing/management (AWS/Azure/GCP account-level operations).
- Hardware procurement and physical server setup.
- Advanced cybersecurity auditing and penetration testing.
- Multi-language UI (future enhancement).

---

## 5. Functional Requirements (FR)
- **FR-01:** Collect real-time traffic and server performance data (RPS, CPU, RAM, response time).
- **FR-02:** Store and preprocess historical data for AI model training.
- **FR-03:** Predict upcoming load for the next interval (e.g., next 10–30 minutes).
- **FR-04:** Generate scaling recommendations based on predicted load.
- **FR-05:** Automatically allocate resources if load exceeds a defined threshold.
- **FR-06:** Provide a dashboard and alerts for real-time monitoring of system health.

---

## 6. Non-Functional Requirements (NFR)
- **NFR-01 (Performance):** System responds within 2 seconds under normal traffic.
- **NFR-02 (Scalability):** Supports scaling up to 200% of anticipated concurrent users.
- **NFR-03 (Availability):** Maintains 99% uptime during peak periods.
- **NFR-04 (Security):** Encrypts sensitive data during transmission.
- **NFR-05 (Reliability):** Monitoring and logging continue even if the prediction module fails.
- **NFR-06 (Usability):** Admin dashboard is intuitive and accessible with minimal training.

---

## 7. Assumptions & Constraints
- Stable internet connectivity is available for monitoring and dashboard access.
- The solution will be built within hackathon time constraints.
- Prediction accuracy depends on availability of historical traffic data.
- Deployment will be on limited resources (demo environment).
- Data collection depends on access to server logs and monitoring APIs.

---

## 8. Data Requirements
- **Traffic Data:** requests/sec, active users, session counts.
- **Server Data:** CPU %, RAM %, disk usage, network usage, latency.
- **Historical Data:** past peak-hour logs for model training.
- **Storage Format:** CSV/JSON/Database records.
- **Privacy:** No personal user data will be stored; only aggregated usage metrics will be used.

---

## 9. AI / Automation Requirements
- **Model Type:** Time-series prediction model (LSTM / ARIMA / Regression).
- **Inputs:** traffic metrics + server health metrics.
- **Output:** predicted load level (Low/Medium/High) or numeric load value.
- **Decision Logic:** scaling triggers when prediction exceeds a threshold.
- **Model Update:** system supports periodic retraining using new data.

---

## 10. Success Metrics
- Prediction accuracy ≥ 85% on test dataset.
- Response time improves by at least 30% during peak traffic.
- Reduction in downtime events compared to baseline.
- Auto-scaling triggers correctly for high-load scenarios.
- Dashboard updates with < 5 seconds delay.

---

## 11. Compliance & Standards
- Follow government IT security guidelines (basic best practices).
- Ensure no personal data is collected without consent.
- Maintain audit logs for monitoring and transparency.

---

## 12. Future Enhancements
- Multi-cloud support for scaling decisions.
- Advanced anomaly detection for sudden spikes/attacks.
- Multi-language dashboard support.
- Integration with SMS/WhatsApp alerts for administrators.
- Automated cost optimization for resource allocation.


# Design Document

**Project Name:** AI System Design Simulator  
**Theme:** AI / Cloud / Education / Smart Learning  
**Team Name:** SASSY CODERS *(edit if needed)*  
**Version:** 1.0  
**Date:** 25-01-2026  

---

## 1. System Overview
AI System Design Simulator is an interactive learning platform where users enter a system requirement such as:
> “Design a chat application for 1 million users.”

The platform uses AI to generate an initial scalable architecture, runs traffic simulations, identifies bottlenecks, explains failures, and recommends improvements (caching, sharding, message queues, autoscaling, CDN).  
This helps learners understand scaling behavior by experimentation rather than memorization.

---

## 2. High-Level Architecture (AWS)
**Frontend:** React / Next.js hosted on **Amazon S3 + CloudFront**  
**API Layer:** **Amazon API Gateway**  
**Compute / Backend:** **AWS Lambda** *(or ECS Fargate)*  
**AI Engine:** **Amazon Bedrock** *(LLM for architecture + explanations)*  
**Simulation Engine:** **AWS Lambda (async)** + **Step Functions** *(optional orchestration)*  
**Data Store:** **Amazon DynamoDB** *(configs, versions, results)*  
**Observability:** **Amazon CloudWatch** *(logs, metrics, alarms)*  
**Auth (optional):** **Amazon Cognito**

---

## 3. Architecture Diagram (Text)
```
User
 │
 ▼
Frontend (React / Next.js)  ── hosted on S3 + CloudFront
 │
 ▼
Amazon API Gateway
 │
 ▼
Backend Service (Lambda / ECS)
 │
 ├── DynamoDB (architecture versions, simulation results)
 │
 ├── Traffic Simulation Engine (Lambda async / Step Functions)
 │        │
 │        ▼
 │    Metrics + Logs → CloudWatch
 │
 └── AI Architecture Generator → Amazon Bedrock
           │
           ▼
   Recommendations + Explanation → Frontend
```

---

## 4. Component Design

### 4.1 Frontend (UI Layer)
**Purpose:** Collect user requirements, show generated architecture, run simulation, visualize bottlenecks and improvements.

**Main Screens**
- Requirement Input (system type, users, RPS, read/write ratio, latency target)
- Generated Architecture View (diagram + components list)
- Simulation Dashboard (traffic slider, metrics charts)
- Bottleneck & Explanation Panel
- Optimization Suggestions (with trade-offs)
- Export Report (PDF/JSON)

---

### 4.2 Backend Service (API + Orchestration)
**Purpose:** Validate input, call AI, trigger simulation, store results, return outputs.

**Core APIs**
| Endpoint | Method | Description |
|---------|--------|-------------|
| `/generate-architecture` | POST | Generate initial architecture via AI |
| `/run-simulation` | POST | Run traffic simulation for current architecture |
| `/get-results` | GET | Fetch simulation metrics and bottlenecks |
| `/apply-optimization` | POST | Apply AI suggestions and re-run simulation |
| `/export-report` | GET | Export final report |

---

### 4.3 AI Architecture Generator (Bedrock)
**Purpose:** Convert user requirements into architecture + improvement steps.

**Inputs**
- System requirement prompt
- Expected user load
- RPS + read/write ratio
- Latency target and cost preference

**Outputs**
- Components list (LB, services, cache, DB, queue, CDN)
- Suggested improvements with trade-offs
- Human-readable explanation of bottlenecks

---

### 4.4 Traffic Simulation Engine
**Purpose:** Simulate request flow and estimate component load.

**Simulation Capabilities**
- Gradual scaling (10K → 1M users)
- Burst traffic spikes
- Read-heavy / write-heavy scenarios
- Latency & throughput estimation
- Component saturation detection

**Metrics Produced**
- p50 / p95 latency
- Throughput (req/sec)
- Error rate
- CPU/memory utilization estimate
- Queue backlog and processing delay
- DB connection / write capacity saturation

---

### 4.5 Bottleneck Detection Module
**Purpose:** Detect failures and root causes during simulation.

**Example Bottlenecks**
- Database write throughput exceeded
- Cache hit rate below threshold (cache miss storm)
- App servers CPU > 85%
- Queue backlog delay increasing
- Network bandwidth saturation

**Output Format**
- Bottleneck component name
- Failure reason
- Impact on latency/error rate
- Recommended fixes

---

## 5. System Flow (Hackathon Orientation)

### 5.1 Main Flow
1. User enters requirement  
2. Frontend sends input to backend  
3. AI generates initial architecture  
4. Simulation engine runs traffic  
5. System checks for bottlenecks  
6. If stable → show metrics & report  
7. If bottleneck → explain + suggest improvements  
8. Apply improvements → re-run simulation  
9. Repeat until stable

### 5.2 Decision Loop (Text)
- **Bottleneck?**
  - **No:** System stable → update dashboard → end  
  - **Yes:** Explain cause → suggest fix → update architecture → simulate again  

---

## 6. Data Design

### 6.1 Stored Entities (DynamoDB)
- `UserSession`
- `ArchitectureVersion`
- `SimulationRun`
- `BottleneckReport`
- `RecommendationSet`

### 6.2 Example Simulation Result
```json
{
  "architectureId": "arch-101",
  "users": 1000000,
  "rps": 50000,
  "latencyP95": "420ms",
  "errorRate": "2.3%",
  "bottleneck": "Database",
  "reason": "Write throughput exceeded",
  "suggestions": ["Add sharding", "Introduce queue for writes", "Use cache for reads"]
}
```

---

## 7. Security Design
- IAM roles with least privilege
- API Gateway throttling + request validation
- Sanitized inputs to prevent prompt injection and abuse
- Optional authentication using Cognito
- CloudWatch logs for audit and debugging

---

## 8. Scalability & Reliability
- Stateless compute (Lambda/ECS) with auto-scaling
- Async simulation execution to avoid blocking UI
- DynamoDB for high-throughput storage
- CloudWatch alarms for failures
- Retry + timeout handling for simulation jobs

---

## 9. Trade-offs & Limitations (MVP)
- Simulation uses estimated models, not real infra load testing
- AI suggestions may vary by prompt constraints
- Limited number of templates in MVP (chat, e-commerce, streaming)
- Diagram rendering may be simplified for hackathon speed

---

## 10. Future Enhancements
- Real AWS cost estimation and budget-aware suggestions
- More templates (UPI, Netflix, Instagram, Uber)
- Multi-cloud comparison mode
- Interactive drag-drop architecture builder
- Team mode for collaborative design learning

---

## 11. Conclusion
AI System Design Simulator makes system design learning practical by combining AI-driven architecture generation, traffic simulation, bottleneck detection, and iterative optimization recommendations. It enables users to understand scaling behavior through experimentation and measurable feedback.
