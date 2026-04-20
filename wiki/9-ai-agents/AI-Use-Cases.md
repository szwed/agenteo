# AI Use Cases

Platform engineering use cases and personas for [[AI-Agents-Overview]].

## Platform Engineer Persona

**Key responsibilities**:
- Infrastructure management (design, implement, manage cloud/on-prem infra)
- Automation (CI/CD pipelines, repetitive task automation)
- Monitoring and observability (system health and performance)
- Collaboration (align platform capabilities with business needs)

**Tools**: Docker, Kubernetes, AWS/Azure/GCP, Jenkins/GitHub Actions, Prometheus/Grafana

**Example**: design K8s-based infrastructure for microservices, automate deployments with Helm charts, integrate Prometheus and Grafana for observability.

## Available Persona Profiles

| Profile | Agents | Use Case |
|---------|--------|----------|
| **platform-engineer** | ArgoCD, AWS, Backstage, Confluence, GitHub, GitLab, Jira, Komodor, PagerDuty, Slack, Splunk, Weather, Webex, Petstore | Full platform operations |
| **devops-engineer** | ArgoCD, GitHub | DevOps-focused CI/CD |
| **incident-engineer** | PagerDuty, GitHub, Backstage, Jira, Confluence, Komodor | Incident response |
| **product-owner** | Jira, Confluence | Story creation, backlog management |
| **caipe-basic** | Weather, Petstore | Getting started / demo |

## Pre-Built Skills

Skills are pre-built prompt templates available in the [[AI-Agents-UI]] use cases gallery:

| Skill | Description |
|-------|-------------|
| **aws-cost-analysis** | AWS cost analysis and optimization |
| **check-deployment-status** | ArgoCD deployment status check |
| **cluster-resource-health** | AWS/Kubernetes cluster health |
| **documentation-search** | RAG knowledge base search |
| **incident-investigation** | PagerDuty + Jira + ArgoCD incident analysis |
| **oncall-handoff** | Multi-agent on-call handoff |
| **release-readiness-check** | Multi-agent release readiness |
| **review-open-pull-requests** | GitHub PR review |
| **review-specific-pr** | Detailed single PR review |
| **security-vulnerability-report** | GitHub security vulnerability report |
| **sprint-progress-report** | Jira sprint progress |

## See Also

- [[AI-Prompt-Library]] — prompt configurations that drive these use cases
- [[AI-Platform-Agents]] — agents referenced by each persona
