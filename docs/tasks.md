# Task List: ESG Management System (ESG-AI Nexus)

This document outlines the actionable tasks required to build the ESG-AI Nexus platform, prioritizing the migration of existing assets from `bintulu-fe-filamentphp` and the development of the core Agentic AI features.

## Phase 1: MVP & Migration (Months 1-3)
**Goal:** Establish the multi-tenant foundation and migrate key Carbon Accounting features.

### 1.1. Infrastructure & Setup
- [ ] **Initialize Repository:** Set up a new Laravel 11 project with FilamentPHP 3.
- [ ] **Multi-tenancy Configuration:**
    - [ ] Install `spatie/laravel-permission` or Filament's native multi-tenancy.
    - [ ] Define Tenant model (Organization/Company).
    - [ ] Configure Tenant isolation (database-per-tenant or schema separation).
- [ ] **Environment Setup:** Dockerize the application (Nginx, PHP 8.2, PostgreSQL, Redis).

### 1.2. Auth & User Management
- [ ] **Authentication System:** Implement generic login with Multi-Factor Authentication (MFA).
- [ ] **Role-Based Access Control (RBAC):**
    - [ ] Define roles: Super Admin, Tenant Admin, ESG Officer, Auditor.
    - [ ] Migrate `RoleResource` and `UserResource` from `bintulu-fe-filamentphp`.
- [ ] **User Onboarding:** Create invitation flows for new tenant users.

### 1.3. Data Model Migration (The "Lift & Shift")
- [ ] **Emission Factors:**
    - [ ] Migrate `EmissionFactors` model and table structure.
    - [ ] Port `EmissionFactorTableResource`, `UnitResource`, `GasesResource`.
    - [ ] Seed initial emission factors (IPCC/local data).
- [ ] **Carbon Calculation Engine:**
    - [ ] Refactor `EmissionEntry` model logic (Scope 1 & 2 calculation) into a standalone Service Class (`CarbonCalculatorService`).
    - [ ] Ensure "CO2e" conversion logic is robust and unit-aware.
- [ ] **Data Entry Forms:**
    - [ ] Port `EmissionEntryResource` form schema to the new tenant context.
    - [ ] Port `WaterBillEntryResource` for Resource Efficiency module.

### 1.4. ESG Readiness Assessment (New Feature)
- [ ] **Schema Design:** Create models for `Assessment`, `Question`, `Answer`, and `Score`.
- [ ] **Assessment UI:** Build a Filament wizard for the "ESG Readiness Self-Assessment".
- [ ] **Scoring Logic:** Implement scoring algorithm based on MITI i-ESG framework.
- [ ] **Report Generation:** Generate a simple PDF summary of the readiness score.

### 1.5. Audit Trail
- [ ] **Integration:** Install `owen-it/laravel-auditing`.
- [ ] **Configuration:** Port `AuditResource` to view logs in the admin panel.
- [ ] **Coverage:** Apply `Auditable` trait to all critical models (`EmissionEntry`, `User`, `Organization`).

---

## Phase 2: The Agentic Layer (Months 4-6)
**Goal:** Introduce AI agents to automate data hunting and reporting.

### 2.1. AI Microservice Setup
- [ ] **Service Skeleton:** Create a Python (FastAPI) project.
- [ ] **API Security:** Secure communication between Laravel and Python service (API Keys/JWT).
- [ ] **Vector Database:** Set up Pinecone or Weaviate for RAG (Retrieval-Augmented Generation).

### 2.2. "Chat with Data" (F-04)
- [ ] **Indexing:** Build a pipeline to index ESG data (Emission entries, Policies) into the vector DB.
- [ ] **Chat Interface:** Build a chat UI in Filament (using Livewire).
- [ ] **Agent Logic:** Implement LangChain agent to query the vector DB and SQL database to answer natural language questions ("What was our total Scope 1 emission last month?").

### 2.3. "Data Hunter" Agent
- [ ] **Anomaly Detection:** Train/Configure a model to detect outliers in energy bills.
- [ ] **Missing Data Identification:** Create a scheduled job that asks the AI to check for gaps in monthly reporting.
- [ ] **Notification:** Agent sends emails/Slack alerts to facility managers for missing data.

### 2.4. Reporting Engine
- [ ] **Template Management:** Create templates for GRI, SASB, and TCFD reports.
- [ ] **Data Mapping:** Map internal data points to standard framework fields.
- [ ] **Report Generator Agent:** Implement AI logic to draft narrative sections (e.g., "Management Approach") based on collected data.

---

## Phase 3: Scale & Supply Chain (Months 7+)
**Goal:** Extend reach to the supply chain and automate regulatory compliance.

### 3.1. Supply Chain Portal
- [ ] **Supplier Onboarding:** Create a simplified "Lite" view for suppliers.
- [ ] **Scope 3 Data Collection:** Forms for suppliers to submit their carbon data.
- [ ] **MSME Readiness Mode:** specific simplified assessment for small suppliers.

### 3.2. Regulatory Scout
- [ ] **Scraper:** Build a scraper for regulatory news sources (or hook into an API).
- [ ] **Analysis Agent:** AI agent that compares new regulations against stored internal policies.
- [ ] **Gap Analysis:** Dashboard showing compliance gaps.

### 3.3. Marketplace
- [ ] **Auditor Directory:** Registry of certified ESG auditors.
- [ ] **Engagement:** Workflow for hiring and granting data access to 3rd party auditors.

