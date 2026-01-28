# Enterprise AI Agent Challenges: A Thematic Framework

## Document Purpose
Client-facing reference document for WAM (Wealth Asset Management) Line of Business, presenting organizational challenges that necessitate a centralized Agent Factory approach.

---

## Thematic Overview

| Theme | Bundled Challenges | Core Value Proposition |
|-------|-------------------|------------------------|
| **Governance & Auditability** | Agent Sprawl, Security & Compliance | Clear audit trails, policy enforcement, regulatory readiness |
| **Reusability & Standardization** | Inconsistent Agent Quality, Lifecycle Management | Plug-and-play workflows, blueprints, version control |
| **Interoperability & Orchestration** | Unified Orchestration | Federated system compatibility, seamless agent coordination |
| **Operational Excellence** | Uncontrolled Costs, Scaling & Reliability | Cost optimization, latency reduction, high availability |

---

# Theme 1: Governance & Auditability

> **Value Proposition**: Establish clear audit trails, enforce policies consistently, and maintain regulatory compliance across all AI agent operations.

---

## Challenge 1.1: Agent Sprawl & Shadow AI

### Challenge Definition
Uncontrolled proliferation of AI agents across the enterprise without centralized visibility, inventory management, or ownership accountability—creating a new form of "Shadow IT" that organizations cannot monitor, govern, or secure.

### Enterprise/Business Pain

| Pain Point | Business Impact | Supporting Data |
|------------|-----------------|-----------------|
| **Unknown Attack Surface** | Security teams cannot assess or protect what they cannot see | 40% of enterprises will experience shadow AI security incidents by 2030 ([Gartner](https://www.gartner.com/en/documents/6714034)) |
| **Compliance Exposure** | Inability to demonstrate AI governance to regulators | Only 12% of organizations have dedicated AI governance structures ([Gartner](https://www.isaca.org/resources/news-and-trends/industry-news/2025/the-rise-of-shadow-ai-auditing-unauthorized-ai-tools-in-the-enterprise)) |
| **Unattributable Spend** | Finance cannot allocate AI costs to business units | Shadow AI breaches cost $670,000 more than standard incidents ([IBM 2025](https://www.kiteworks.com/cybersecurity-risk-management/ibm-2025-data-breach-report-ai-risks/)) |
| **Duplicated Investment** | Multiple teams solving identical problems independently | 80%+ of companies report no material earnings from GenAI initiatives ([McKinsey](https://www.mckinsey.com/capabilities/quantumblack/our-insights/the-state-of-ai)) |

**Financial Services Context**: 22% of workers used unauthorized AI for risky finance-related tasks ([Microsoft Study](https://www.itpro.com/technology/artificial-intelligence/gartner-says-40-percent-of-enterprises-will-experience-shadow-ai-breaches-by-2030-educating-staff-is-the-key-to-avoiding-disaster))

### Engineering Challenge

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENGINEERING GAPS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ No centralized agent registry or catalog                    │
│  ❌ No automated discovery of deployed agents                   │
│  ❌ No standardized metadata schema (owner, purpose, status)    │
│  ❌ No dependency mapping between agents and downstream systems │
│  ❌ No lifecycle state tracking (dev → staging → prod → retired)│
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Technical Debt Drivers**:
- Teams deploy agents via ad-hoc scripts without registration
- No API gateway or service mesh capturing agent traffic
- Lack of tagging/labeling standards across cloud environments
- No integration with CMDB or asset management systems

**Required Engineering Capabilities**:
1. Agent Registry Service with mandatory registration APIs
2. Automated agent discovery via network/API traffic analysis
3. Metadata enforcement layer with ownership validation
4. Dependency graph visualization and impact analysis

---

## Challenge 1.2: Security & Compliance

### Challenge Definition
AI agents accessing sensitive data and executing business-critical actions without adequate access controls, audit logging, credential management, or policy enforcement—creating regulatory and operational risk.

### Enterprise/Business Pain

| Pain Point | Business Impact | Supporting Data |
|------------|-----------------|-----------------|
| **Regulatory Penalties** | Non-compliance with AI governance mandates | $4.6B in global AML fines in 2024; H1 2025 up 417% YoY ([Fenergo](https://resources.fenergo.com/newsroom/global-financial-institutions-struggle-with-rising-client-losses-and-compliance-costs-as-ai-adoption-increases-fenergo)) |
| **Data Leakage** | Sensitive information exposed via AI interactions | 46% of organizations reported internal data leaks through GenAI ([Cisco 2025](https://acuvity.ai/2025-state-of-ai-security/)) |
| **Audit Failures** | Cannot demonstrate agent decision provenance | 80% report risky AI agent behaviors (unauthorized access, data exposure) ([KPMG](https://kpmg.com/us/en/media/news/q4-ai-pulse.html)) |
| **Credential Sprawl** | API keys and secrets scattered across teams | Only 6% use advanced security frameworks for AI ([Security Study](https://kpmg.com/us/en/media/news/q4-ai-pulse.html)) |

**Regulatory Landscape**:
- U.S. Treasury AI Report (Dec 2024): [Uses, Opportunities, and Risks of AI in Financial Services](https://www.debevoise.com/insights/publications/2025/01/treasurys-post-2024-rfi-report-on-ai-in-financial)
- NY DFS Guidance (Oct 2024): [Cybersecurity Risks from AI](https://www.dfs.ny.gov/industry-guidance/industry-letters/il20241016-cyber-risks-ai-and-strategies-combat-related-risks)
- FSOC elevated AI as significant focus area in December 2024 Annual Report
- 59 U.S. AI regulations issued in 2024 (more than double previous year)

### Engineering Challenge

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENGINEERING GAPS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ No centralized credential vault for agent secrets           │
│  ❌ No RBAC/ABAC enforcement layer for agent permissions        │
│  ❌ No immutable audit log capturing all agent actions          │
│  ❌ No policy-as-code framework for compliance rules            │
│  ❌ No data classification integration (PII/PCI/PHI tagging)    │
│  ❌ No explainability layer for agent decision rationale        │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Technical Debt Drivers**:
- Agents use hardcoded credentials or environment variables
- No integration with enterprise IAM (Okta, Azure AD, etc.)
- Logging fragmented across agent implementations
- No standardized format for compliance reporting

**Required Engineering Capabilities**:
1. Secrets Management integration (HashiCorp Vault, AWS Secrets Manager)
2. Policy Engine with OPA/Rego for declarative compliance rules
3. Centralized audit log with tamper-proof storage
4. Data Loss Prevention (DLP) integration for sensitive data detection
5. Explainable AI (XAI) layer for decision traceability

---

# Theme 2: Reusability & Standardization

> **Value Proposition**: Enable plug-and-play workflows, standardized agent blueprints, and consistent lifecycle management to maximize reuse and reduce redundant development.

---

## Challenge 2.1: Inconsistent Agent Quality

### Challenge Definition
Absence of standardized patterns, guardrails, and quality gates resulting in agents with varying reliability, accuracy, and safety profiles—leading to unpredictable business outcomes and potential harm.

### Enterprise/Business Pain

| Pain Point | Business Impact | Supporting Data |
|------------|-----------------|-----------------|
| **Revenue Loss from Errors** | Agents making unauthorized commitments | Air Canada forced to honor AI-cited nonexistent policy ([Tribunal Ruling 2024](https://www.knostic.ai/blog/ai-hallucinations)) |
| **Decision Quality Risk** | Business decisions based on false AI outputs | 47% of enterprise AI users made major decisions based on hallucinated content ([Enterprise Survey](https://www.fullview.io/blog/ai-statistics)) |
| **Production Adoption Barrier** | Teams unwilling to trust inconsistent agents | Only 10% moved GenAI to production; hallucinations cited as major barrier ([Gartner](https://www.gartner.com/en/newsroom/press-releases/2023-10-11-gartner-says-more-than-80-percent-of-enterprises-will-have-used-generative-ai-apis-or-deployed-generative-ai-enabled-applications-by-2026)) |
| **Reputational Damage** | Customer-facing agents providing incorrect information | 77% of businesses concerned about AI hallucinations ([Deloitte](https://dextralabs.com/blog/llm-hallucinations-enterprise-ai-risks-control/)) |

**Hallucination Rates by Domain**:
| Domain | Rate | Source |
|--------|------|--------|
| General LLM (37 models benchmarked) | >15% | [AI Multiple](https://research.aimultiple.com/ai-hallucination/) |
| Legal (specialized tools) | 17-34% | [Knostic](https://www.knostic.ai/blog/ai-hallucinations) |
| Legal (state-of-the-art LLMs) | 69-88% | [Dextra Labs](https://dextralabs.com/blog/llm-hallucinations-enterprise-ai-risks-control/) |
| GPT-4 class (forced responses) | 20-30% | [OpenAI 2025](https://www.knostic.ai/blog/ai-hallucinations) |

### Engineering Challenge

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENGINEERING GAPS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ No standardized agent blueprint/template library            │
│  ❌ No guardrail framework (input validation, output filtering) │
│  ❌ No automated testing suite for agent behaviors              │
│  ❌ No human-in-the-loop approval workflows for critical actions│
│  ❌ No hallucination detection and mitigation layer             │
│  ❌ No grounding/RAG integration standards                      │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Technical Debt Drivers**:
- Each team implements guardrails (or not) independently
- No shared prompt engineering patterns or libraries
- Testing limited to functional checks, not behavioral validation
- No standardized evaluation metrics across agents

**Required Engineering Capabilities**:
1. Agent Blueprint Library with pre-built guardrails
2. Guardrail Framework (NeMo achieves 95% accuracy, [Research](https://www.auxis.com/ai-guardrails-stop-ai-hallucinations-and-inaccuracies/))
3. RAG + Guardrails integration (reduces hallucinations by 96%, [Stanford](https://www.morphik.ai/blog/eliminate-hallucinations-guide))
4. Behavioral Testing Framework with adversarial prompts
5. Human approval workflow engine for high-stakes decisions

---

## Challenge 2.2: Lifecycle Management Gaps

### Challenge Definition
Lack of standardized processes for versioning, deploying, monitoring, updating, and retiring agents—leading to production instability, broken dependencies, and accumulated technical debt.

### Enterprise/Business Pain

| Pain Point | Business Impact | Supporting Data |
|------------|-----------------|-----------------|
| **Slow Time-to-Value** | Lengthy development and deployment cycles | Average 8 months from prototype to production ([Gartner](https://www.nttdata.com/global/en/insights/focus/2024/between-70-85p-of-genai-deployment-efforts-are-failing)) |
| **Failed AI Investments** | Projects abandoned after significant spend | 85%+ of AI projects fail due to lack of operational infrastructure ([Industry Research](https://lakefs.io/mlops/)) |
| **Production Instability** | Updates break downstream dependencies | Only 48% of AI projects make it to production ([Gartner](https://www.nttdata.com/global/en/insights/focus/2024/between-70-85p-of-genai-deployment-efforts-are-failing)) |
| **Orphaned Agents** | Retired agents leave broken workflows | No systematic deprecation process in most organizations |

**MLOps Adoption**:
- Market: $1.7B (2024) → $129B (2034), 43% CAGR ([MLOps Research](https://arxiv.org/html/2503.15577v1))
- 64.3% of large enterprises have adopted MLOps platforms
- 70% of enterprises will operationalize AI using MLOps ([Gartner](https://www.veritis.com/blog/best-mlops-tools-for-enterprises/))

### Engineering Challenge

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENGINEERING GAPS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ No agent versioning system (model + prompt + config)        │
│  ❌ No CI/CD pipeline for agent deployment                      │
│  ❌ No blue-green/canary deployment capability                  │
│  ❌ No automated rollback mechanism                             │
│  ❌ No dependency tracking for downstream consumers             │
│  ❌ No deprecation workflow with consumer notification          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Technical Debt Drivers**:
- Agents deployed via manual scripts ("it works on my machine")
- No separation between model artifacts, prompts, and configurations
- Updates overwrite production without safety nets
- No integration with enterprise release management

**Required Engineering Capabilities**:
1. Agent Artifact Repository with semantic versioning
2. CI/CD Pipeline with automated testing gates
3. Deployment Orchestrator supporting progressive rollout
4. Rollback Engine with automatic trigger on quality degradation
5. Dependency Graph with impact analysis for changes

**Proven Impact**: MLOps reduces deployment time from 6-12 months → 2-4 weeks and infrastructure costs by up to 60% ([MLOps Research](https://www.veritis.com/blog/best-mlops-tools-for-enterprises/))

---

# Theme 3: Interoperability & Orchestration

> **Value Proposition**: Enable federated system compatibility, seamless agent coordination, and plug-in architecture for existing workflows.

---

## Challenge 3.1: Unified Orchestration

### Challenge Definition
Inability to coordinate multiple agents across teams, departments, and systems for complex workflows—resulting in manual handoffs, siloed capabilities, and unrealized automation potential.

### Enterprise/Business Pain

| Pain Point | Business Impact | Supporting Data |
|------------|-----------------|-----------------|
| **Manual Process Bottlenecks** | Human handoffs between agent outputs | Workflow completion time: days instead of hours |
| **Integration Paralysis** | Cannot connect agents to existing systems | 95% face challenges integrating AI into existing processes ([MuleSoft 2025](https://thenewstack.io/scaling-ai-agents-in-the-enterprise-the-hard-problems-and-how-to-solve-them/)) |
| **Stranded AI Investments** | Valuable agents isolated in silos | >40% of agentic AI projects will be canceled by 2027 ([Gartner](https://www.deloitte.com/us/en/insights/industry/technology/technology-media-and-telecom-predictions/2026/ai-agent-orchestration.html)) |
| **Coordination Complexity** | Leaders unable to manage multi-agent systems | 65% cite agentic system complexity as top barrier ([KPMG Q4 2025](https://kpmg.com/us/en/media/news/q4-ai-pulse.html)) |

**Market Signal**: 1,445% surge in multi-agent system inquiries (Q1 2024 → Q2 2025) ([Gartner](https://machinelearningmastery.com/7-agentic-ai-trends-to-watch-in-2026/))

**Orchestration Value**: Multi-agent systems achieve 45% faster problem resolution and 60% more accurate outcomes ([Industry Research](https://www.onabout.ai/p/mastering-multi-agent-orchestration-architectures-patterns-roi-benchmarks-for-2025-2026))

### Engineering Challenge

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENGINEERING GAPS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ No central planner for task decomposition and routing       │
│  ❌ No agent capability registry (skills, inputs, outputs)      │
│  ❌ No standardized agent communication protocol                │
│  ❌ No workflow definition language for multi-agent flows       │
│  ❌ No context/state management across agent handoffs           │
│  ❌ No conflict resolution for competing agent outputs          │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Technical Debt Drivers**:
- Agents built with incompatible interfaces
- No shared understanding of agent capabilities
- Point-to-point integrations instead of hub-and-spoke
- No standardized message formats or protocols

**Emerging Standards**:
- Model Context Protocol (MCP)
- Agent Communication Protocol (ACP)
- Agent-to-Agent Protocol (A2A)
- Agent Network Protocol (ANP)

**Required Engineering Capabilities**:
1. Central Planner with task decomposition and agent matching
2. Agent Capability Registry with skill ontology
3. Protocol Adapter Layer supporting multiple communication standards
4. Workflow Engine with visual designer and YAML/JSON definitions
5. State Management Service for context persistence across agents
6. Arbitration Layer for output conflict resolution

**Architecture Patterns**:
| Pattern | Use Case | Trade-off |
|---------|----------|-----------|
| Centralized | Strict governance | Single point of failure |
| Decentralized | Resilience | Harder to debug |
| Hierarchical | Complex workflows | Increased latency |
| Event-Driven | Real-time response | Eventual consistency |
| Hybrid Human-AI | Regulated industries | Higher operational cost |

---

# Theme 4: Operational Excellence

> **Value Proposition**: Optimize costs, reduce latency, and ensure high availability through intelligent resource management and production-grade reliability.

---

## Challenge 4.1: Uncontrolled Costs

### Challenge Definition
Lack of visibility into LLM API consumption, inefficient token usage, and inability to attribute costs to business units—resulting in budget overruns and inability to demonstrate ROI.

### Enterprise/Business Pain

| Pain Point | Business Impact | Supporting Data |
|------------|-----------------|-----------------|
| **Budget Overruns** | Surprise bills and unplanned spend | API spending: $0.5B (2023) → $8.4B (mid-2025) ([Menlo Ventures](https://menlovc.com/perspective/2025-mid-year-llm-market-update/)) |
| **No Cost Attribution** | Cannot charge back to business units | 72% expect higher LLM spending with limited visibility ([Kong Inc.](https://konghq.com/blog/enterprise-ai-spending-2025)) |
| **Inefficient Consumption** | Wasted tokens on redundant or verbose prompts | Chips and staff = 70-80% of total LLM costs ([2024 Analysis](https://www.ptolemay.com/post/llm-total-cost-of-ownership)) |
| **ROI Uncertainty** | Cannot justify AI investments | 95% of GenAI implementations fail to meet expectations ([MIT](https://fortune.com/2025/08/18/mit-report-95-percent-generative-ai-pilots-at-companies-failing-cfo/)) |

**Spending Reality**:
| Metric | Value | Source |
|--------|-------|--------|
| Average enterprise GenAI investment | $1.9M | [Kong Inc.](https://konghq.com/blog/enterprise-ai-spending-2025) |
| Organizations spending >$250K/year | 37% | [Kong Inc.](https://konghq.com/blog/enterprise-ai-spending-2025) |
| Expected spending increase | 72% expect higher | [Kong Inc.](https://konghq.com/blog/enterprise-ai-spending-2025) |

**ROI Potential**: Top performers achieve $10.30 return per dollar invested ([Wharton](https://knowledge.wharton.upenn.edu/special-report/2025-ai-adoption-report/))

### Engineering Challenge

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENGINEERING GAPS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ No token metering per agent/team/workflow                   │
│  ❌ No cost allocation tagging infrastructure                   │
│  ❌ No prompt optimization layer (caching, compression)         │
│  ❌ No model routing based on cost/quality trade-offs           │
│  ❌ No budget alerts and automatic throttling                   │
│  ❌ No chargeback integration with finance systems              │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Technical Debt Drivers**:
- Direct LLM API calls without metering proxy
- No standardized tagging for cost attribution
- Using expensive models for simple tasks
- No caching of repeated queries

**Required Engineering Capabilities**:
1. Token Metering Gateway with per-request attribution
2. Cost Allocation Engine with business unit tagging
3. Prompt Cache with semantic similarity matching
4. Model Router selecting optimal model per task complexity
5. Budget Management with alerts, quotas, and throttling
6. FinOps Dashboard with drill-down and forecasting

**Cost Optimization Opportunity**: Inference costs fell 280-fold for GPT-3.5-class models (2020-2024) ([Stanford AI Index](https://www.typedef.ai/resources/llm-adoption-statistics))

---

## Challenge 4.2: Scaling & Reliability

### Challenge Definition
Inability to handle variable workloads, lack of fault tolerance, and extended incident resolution times—resulting in service degradation, customer impact, and operational firefighting.

### Enterprise/Business Pain

| Pain Point | Business Impact | Supporting Data |
|------------|-----------------|-----------------|
| **Service Outages** | Customer-facing agents unavailable during peak demand | GenAI incidents take 1.72x longer to mitigate ([arXiv](https://arxiv.org/html/2504.08865v2)) |
| **Scaling Limitations** | Cannot handle traffic spikes | Only 2% have deployed agentic AI at scale ([Industry Research](https://www.webpronews.com/overcoming-challenges-in-scaling-ai-agents-for-enterprises/)) |
| **High Failure Rates** | Projects abandoned due to reliability issues | 42% abandoned most AI initiatives in 2025 (up from 17% in 2024) ([Enterprise Survey](https://www.fullview.io/blog/ai-statistics)) |
| **Detection Gaps** | Issues discovered by users, not monitoring | 38.3% of GenAI incidents detected by humans vs 13.7% for other services ([arXiv](https://arxiv.org/html/2504.08865v2)) |

**Production Incident Breakdown**:
| Incident Type | Percentage | Source |
|---------------|-----------|--------|
| Performance degradation | 49.8% | [arXiv](https://arxiv.org/html/2504.08865v2) |
| Deployment failure | 35.7% | [arXiv](https://arxiv.org/html/2504.08865v2) |
| Invalid inference | 14.5% | [arXiv](https://arxiv.org/html/2504.08865v2) |

**Top Scaling Barriers (2025)**:
| Barrier | % Citing | Source |
|---------|----------|--------|
| Data privacy risks | 67% | [Enterprise Survey](https://www.spaceo.ai/blog/agentic-ai-frameworks/) |
| Integration complexity | 64% | [Enterprise Survey](https://www.spaceo.ai/blog/agentic-ai-frameworks/) |
| Hallucination/reliability | 60% | [Enterprise Survey](https://www.spaceo.ai/blog/agentic-ai-frameworks/) |

### Engineering Challenge

```
┌─────────────────────────────────────────────────────────────────┐
│                    ENGINEERING GAPS                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ❌ No auto-scaling based on request volume/latency             │
│  ❌ No circuit breaker for cascading failure prevention         │
│  ❌ No load balancing across agent instances                    │
│  ❌ No health checks and self-healing capabilities              │
│  ❌ No observability stack (metrics, traces, logs)              │
│  ❌ No disaster recovery / multi-region deployment              │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

**Technical Debt Drivers**:
- Single-instance agent deployments
- No containerization or orchestration (K8s)
- Synchronous calls without timeout/retry logic
- Logging insufficient for root cause analysis

**Required Engineering Capabilities**:
1. Auto-Scaler with request-based and predictive scaling
2. Circuit Breaker with configurable thresholds and fallbacks
3. Load Balancer with health-aware routing
4. Observability Platform (Prometheus, Jaeger, ELK/Loki)
5. Chaos Engineering framework for resilience testing
6. Multi-Region Deployment with automated failover

---

# Summary: Theme-to-Capability Mapping

| Theme | Challenges | Key Engineering Capabilities |
|-------|------------|------------------------------|
| **Governance & Auditability** | Agent Sprawl, Security & Compliance | Agent Registry, Policy Engine, Audit Log, Secrets Vault, DLP Integration |
| **Reusability & Standardization** | Inconsistent Quality, Lifecycle Gaps | Blueprint Library, Guardrail Framework, CI/CD Pipeline, Version Control |
| **Interoperability & Orchestration** | Unified Orchestration | Central Planner, Capability Registry, Protocol Adapters, Workflow Engine |
| **Operational Excellence** | Uncontrolled Costs, Scaling & Reliability | Token Metering, Model Router, Auto-Scaler, Observability, Circuit Breakers |

---

# Key Sources Summary

## Analyst Firms
| Firm | Key Reports |
|------|-------------|
| Gartner | Shadow AI predictions, Agentic AI forecasts, MLOps adoption |
| McKinsey | State of AI, Agentic AI Mesh architecture |
| Deloitte | GenAI enterprise state, Orchestration insights |
| KPMG | AI Pulse quarterly surveys |

## Research & Standards
| Organization | Focus Area |
|--------------|------------|
| MIT | GenAI implementation failure rates |
| Stanford | RAG + Guardrails effectiveness |
| NIST | AI Risk Management Framework |
| ISO | 42001 AI Management System Standard |

## Regulatory (Financial Services)
| Body | Guidance |
|------|----------|
| U.S. Treasury | AI in Financial Services Report (Dec 2024) |
| NY DFS | AI Cybersecurity Guidance (Oct 2024) |
| FSOC | AI Risk Focus (Dec 2024 Annual Report) |
| Fenergo | AML Fines Analysis |

---

## Document Control

| Field | Value |
|-------|-------|
| Version | 2.0 |
| Created | January 2026 |
| Structure | Thematic with Challenge Layout |
| Target Audience | WAM Line of Business |

---

*All statistics sourced from cited research. Verify against original sources before client presentation.*
