# SupportPilot Core

**SupportPilot** is the core customer support platform developed and maintained by Acme Horizon GmbH (EU Entity: Acme Horizon GmbH, acmemock02.de). SupportPilot provides enterprise-grade ticket management, escalation workflows, SLA management, and reporting capabilities for B2B customer support operations across Europe.

---

## Product Overview

SupportPilot is the backbone of Acme Horizon Group customer support operations. The platform handles the full lifecycle of support tickets from creation through resolution, with configurable escalation workflows, SLA enforcement, and reporting dashboards tailored to customer tier and industry requirements.

**Current Release:** Version 4.2 (June 2026)
**Platform:** Acme Horizon GmbH | acmemock02.de
**Support Region:** European Union

---

## Core Features

### Ticket Routing and Queue Management
- Multi-queue routing based on customer tier, issue category, and agent availability
- Rule-based assignment with support for AND/OR logic groups
- Priority-based queue management with real-time rebalancing
- Overflow routing for high-volume periods

### Escalation Workflows
- Configurable escalation timeout settings per customer tier
  - Standard Tier: 2-hour default escalation timeout
  - Professional Tier: 1-hour default escalation timeout
  - Enterprise Tier: 30-minute default escalation timeout
- Customer-level overrides for escalation thresholds
- Multi-stage escalation chains with automated notifications
- Escalation history tracking and audit logging

### SLA Management
- Tier-based SLA policy definitions
- Real-time SLA breach detection and alerts
- SLA pause and resume for waiting-on-customer states
- SLA compliance reporting with breach root cause tracking

### Reporting and Analytics
- SLA compliance dashboard (compliance %, average response time, average resolution time)
- Ticket volume trends by customer, category, and time period
- Agent performance metrics
- Customer satisfaction score (CSAT) correlation with ticket metrics
- Export to CSV and PDF for compliance reporting

### Knowledge Base Integration
- Embedded knowledge base search within ticket creation and update UI
- Automatic article suggestions based on ticket subject and category
- Agent-facing article recommendations during active ticket handling
- Reduction of escalation rates through self-service article surfacing (Beta in Release 4.2)

---

## Customer Context

SupportPilot serves the following EU customers in the current deployment wave:

| Customer | Tier | Industry | Key Focus |
|---|---|---|---|
| BluePeak Logistics | Enterprise | Logistics and Supply Chain | Multi-queue routing, priority SLA |
| Helio Retail Group | Professional | Retail | Escalation workflow customization |
| NordForge Manufacturing | Professional | Manufacturing | SLA compliance visibility and reporting |
| Meridian Health Supplies | Enterprise | Healthcare and Medical Distribution | High-volume query performance |
| UrbanNest Facilities | Standard | Facilities Management | CSAT tracking and satisfaction monitoring |
| ClearWave Utilities | Standard | Utilities and Energy | Knowledge base integration, self-service |

---

## Release 4.2 Highlights

Release 4.2.0 is scheduled for July 14, 2026, and represents the EU onboarding wave release for Acme Horizon GmbH customers.

### Tier-Based Escalation Timeout Configuration
Configurable timeout settings per customer tier replace the prior single-timeout model. Enterprise customers can now configure 30-minute escalation triggers, Professional customers use 1-hour defaults, and Standard customers use 2-hour defaults. All tiers support customer-level override configuration.

### SLA Compliance Reporting Dashboard
A new reporting dashboard provides real-time SLA compliance metrics including compliance percentage, average response time, and average resolution time. Filtering is available by customer, date range, and customer tier.

### Query Performance Optimization
Database indexes have been added on ticket status, created_at, and customer_id columns. Performance testing on the Meridian Health Supplies dataset (87,000 tickets) demonstrates an 85% improvement in query execution time for standard reporting and list queries.

### Custom Routing Rules Enhancement
The routing engine now supports AND/OR logic groups for complex routing rule definitions. Enterprise tier customers can define multi-condition rules that combine customer attributes, issue categories, and SLA tier conditions.

### Knowledge Base Integration (Beta)
Release 4.2 includes a beta integration of knowledge base article search within the ticket UI. Full release is planned for version 4.3. ClearWave Utilities is participating in the beta program.

### Customer Satisfaction Tracking Foundation
Infrastructure for post-resolution CSAT surveys has been deployed. Survey delivery and score correlation with ticket metrics will be activated for UrbanNest Facilities in the initial rollout.

---

## Setup and Installation

### Prerequisites
- Node.js 18.x or later
- PostgreSQL 14 or later
- Redis 7.x (for queue and session management)
- Docker and Docker Compose (for local development)

### Installation

```bash
# Clone the repository
git clone https://github.com/ACME-Mock-EU/supportpilot-core.git
cd supportpilot-core

# Install dependencies
npm install

# Copy environment configuration
cp .env.example .env

# Run database migrations
npm run db:migrate

# Start the development server
npm run dev
```

### Environment Configuration

```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/supportpilot

# Redis
REDIS_URL=redis://localhost:6379

# Application
APP_PORT=3000
APP_ENV=development
JWT_SECRET=your-jwt-secret

# Integrations
FLOWSPHERE_API_URL=https://api.flowsphere.internal
FLOWSPHERE_API_KEY=your-flowsphere-key
INSIGHTGRID_API_URL=https://api.insightgrid.internal
INSIGHTGRID_API_KEY=your-insightgrid-key

# Knowledge Base (Beta)
KB_API_URL=https://kb.supportpilot.internal
KB_INTEGRATION_ENABLED=false
```

### Database Migration (Release 4.2)

Release 4.2 includes a database migration for query performance indexes. The migration is zero-downtime compatible.

```bash
# Run migrations (zero-downtime compatible)
npm run db:migrate

# Verify index creation
npm run db:verify-indexes
```

---

## API Documentation

The SupportPilot REST API provides programmatic access to all platform features.

**Base URL:** `https://api.supportpilot.acmemock02.de/v4/`

**Authentication:** Bearer token (JWT), scoped per customer and agent role.

### Core Endpoints

| Endpoint | Method | Description |
|---|---|---|
| `/tickets` | GET | List tickets with filtering and pagination |
| `/tickets` | POST | Create a new support ticket |
| `/tickets/{id}` | GET | Retrieve a specific ticket |
| `/tickets/{id}/escalate` | POST | Trigger manual escalation |
| `/tickets/{id}/resolve` | POST | Mark ticket as resolved |
| `/escalation-rules` | GET | List escalation rule configurations |
| `/escalation-rules` | POST | Create or update escalation rule |
| `/sla-policies` | GET | List SLA policies by customer tier |
| `/reports/sla-compliance` | GET | SLA compliance metrics report |
| `/reports/ticket-volume` | GET | Ticket volume trends report |
| `/routing-rules` | GET | List ticket routing rules |
| `/routing-rules` | POST | Create routing rule with logic groups |
| `/kb/search` | GET | Knowledge base article search (Beta) |

Full API documentation is available at: `https://docs.supportpilot.acmemock02.de/api/v4`

---

## Integrations

### FlowSphere
SupportPilot integrates with FlowSphere for workflow automation and conditional branching. Release 4.2 custom routing rules align with FlowSphere Release 4.2 conditional branching capabilities.

- Bi-directional ticket status synchronization
- Automated workflow triggers on ticket state transitions
- FlowSphere notification delivery for escalation events
- Shared customer tier and SLA configuration

### InsightGrid
SupportPilot exports ticket and SLA metrics to InsightGrid for cross-platform business intelligence reporting.

- Scheduled data exports (hourly, daily, weekly)
- Custom metric definitions for InsightGrid dashboards
- SLA compliance data feed for executive reporting
- CSAT score integration into InsightGrid customer health scores

---

## Support and Contact

For internal support and escalation on the SupportPilot platform:

- **Internal Slack:** #supportpilot-platform
- **Engineering Escalation:** supportpilot-eng@acmemock02.de
- **EU Customer Success:** eu-success@acmemock02.de
- **Documentation Portal:** https://docs.supportpilot.acmemock02.de

For customer-facing support issues, contact the Acme Horizon GmbH support team at support@acmemock02.de.

---

## Contribution Guidelines

### Branching Strategy
- `main` - production-ready code, protected branch
- `release/x.x` - release preparation branches
- `feature/description` - feature development branches
- `fix/description` - bug fix branches

### Pull Request Requirements
- All pull requests require a minimum of two reviewer approvals
- Unit test coverage must not decrease below current baseline
- Integration tests required for changes to escalation or SLA services
- Performance tests required for database query changes
- PR description must reference the related issue number

### Commit Message Convention

Types: feat, fix, perf, refactor, docs, test, chore

### Code Review Standards
- Reviewer approval is required from at least one senior engineer for changes to escalation, SLA, or routing services
- All comments must be resolved before merge
- Merge is performed by the PR author after approval

---

## License

Copyright 2026 Acme Horizon GmbH. All rights reserved. This repository contains proprietary software and is intended for internal use and authorized customer integrations only.

