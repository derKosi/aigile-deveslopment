---
layout: post
title: "Document Vault in 10 Days – MVP built by an all-AI crew"
date: 2025-07-15
author: derKosi
lang: en
translation_id: dokumentenablage-in-10-tagen
tags: [AI-Team, Aspire, Azure, Bicep, Angular, Git-Flow]
---

> **TL;DR**  
> In one week, we – completely without human commits – developed a multi-tenant document storage for the company Atlantis, **went live** in Azure, and even had Alice & Bob synchronize. The secret: a disciplined division of roles between Kimi K2, GitHub Copilot, and Gemini CLI plus clean Git-Flow + Bicep.

---

## 🤖 The Team at a Glance

| Role | AI Model | Main Responsibility |
|-------|-----------|---------------------|
| Consultant / Architect | **Kimi K2** | ADRs, Threat Model, Cost Review |
| Product Owner | **GitHub Copilot** | Backlog, Gherkin AC, Releases |
| Backend Dev | **Gemini CLI** | .NET 9 Aspire API, EF Core, MassTransit |
| Frontend Dev | **Gemini CLI** | Angular 18, PWA, Upload-UX |
| Legacy Dev | **Gemini CLI** | WinForms 4.8, WPF 4.8 Sync-Clients |
| Security | **Gemini CLI** | SonarQube, IaC-Scan, Tenant-Isolation |
| DevOps | **Gemini CLI / ChatGPT** | Bicep, GitHub Actions, Blue-Green |

---

## 🏗️ What we have *already* built (Sprint 0 & 1)

1. **Repository & Git-Flow**  
main ────────► prod (blue-green ACA)
│
develop ─────► dev (auto-deploy)
│
feature/xyz ─► PR → SonarQube → Merge

2. **Bicep-Basis**  
- 3 environments (`dev`, `stage`, `prod`) with their own RGs  
- KeyVault, Blob Storage, Service Bus, Log Analytics – all via `az deployment` in < 5 min.

3. **Aspire Orchestration**  
`dotnet run --project src/Aspire.AppHost` → API, Angular-SSR and Service Bus Emulator start locally – no more Docker-Compose files needed.

4. **Tenant Isolation POC**  
- Database per tenant (SQLite → Postgres)  
- MassTransit filters events by `TenantId` header – no cross-tenant leaks.

5. **End-to-End Flow**  
Alice uploads a file via WinForms client →  
Charles retrieves the metadata in the browser →  
David downloads it on the tablet – all in 3 seconds.

---

## 📊 Numbers after 10 days

| Metric | Status |
|--------|-------|
| Story Points | 37 / 37 |
| Build Time | 1 min 48 s |
| Test Coverage | 83 % |
| Critical Sonar Findings | 0 |
| Uptime Dev Environment | 99.9 % |
| Costs Dev (Azure) | €3.47 / day |

---

## 🚀 Planned Milestones

| Sprint | Goal | ETA |
|--------|------|-----|
| **Sprint 2** | External invitation + Time-Box-Shares | 29.07. |
| **Sprint 3** | Regional Blue-Green (WEU+EUS2) | 12.08. |
| **Sprint 4** | Offline mode tablet (Delta-Sync) | 26.08. |
| **Sprint 5** | First third-party tenants (Troy, Pompeii) | 09.09. |

---

## 🧩 Learnings (so far)

1. **Clear instruct-*.md are gold** – every AI knows exactly what it delivers.  
2. **Bicep + Aspire = ❤️** – Infrastructure drift is eliminated because every change is scanned in the PR.  
3. **Test tenant isolation early** – a single unit test per story saves days later.  
4. **Don't forget legacy clients** – ClickOnce channel in the GitHub workflow was 3 lines of YAML.

---

## 🌱 Wishes & Roadmap

- **Terraform import** from Bicep for multi-cloud sandbox (AWS, GCP).  
- **AI-generated Playwright tests** from user story Gherkin.  
- **Usage Analytics** via Aspire Telemetry + PowerBI.  
- **Delphi-Native-Bridge** for old ERP systems (coming in Sprint 3).

---

## 📸 Impressions

![Browser Upload](/assets/images/2025-07-15-document-vault-10-days/charles-upload.svg)  
*Charles uploads in the browser – 2 clicks.*

![WinForms Sync](/assets/images/2025-07-15-document-vault-10-days/alice-sync.svg)  
*Alice sees the file 5 seconds later in the explorer.*

---

If you want to dive deeper:  
- [Repo](https://github.com/atlantis-ds/dokumentenablage)  
- [ADR Collection](https://github.com/atlantis-ds/dokumentenablage/tree/main/docs/adr)  
- [Live Demo](https://dev.dokumentenablage.atlantis.io) *(approved for Atlantis employees)*

**Next blog post:** *“How we generate Terraform from Bicep – without writing Terraform”*