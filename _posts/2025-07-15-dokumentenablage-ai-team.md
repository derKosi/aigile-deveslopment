---
layout: post
title: "Dokumentenablage in 10 Tagen – wie wir mit einer reinen KI-Crew MVP-Software bauen"
date: 2025-07-15
author: derKosi
lang: de
translation_id: dokumentenablage-in-10-tagen
tags: [AI-Team, Aspire, Azure, Git-Flow, Bicep, Blazor, Angular]
---

> **TL;DR**  
> In einer Woche haben wir – komplett ohne menschliche Commits – eine mandantenfähige Dokumenten-Ablage für die Firma Atlantis entwickelt, in Azure **live geschaltet** und sogar schon Alice & Bob synchronisieren lassen. Das Geheimnis: eine disziplinierte Rollen-aufteilung zwischen Kimi K2, GitHub Copilot und Gemini CLI plus sauberes Git-Flow + Bicep.

---

## 🤖 Das Team auf einen Blick

| Rolle | KI-Modell | Haupt-Verantwortung |
|-------|-----------|---------------------|
| Consultant / Architekt | **Kimi K2** | ADRs, Threat-Model, Cost-Review |
| Product Owner | **GitHub Copilot** | Backlog, Gherkin-AC, Releases |
| Backend Dev | **Gemini CLI** | .NET 9 Aspire API, EF Core, MassTransit |
| Frontend Dev | **Gemini CLI** | Angular 18, PWA, Upload-UX |
| Legacy Dev | **Gemini CLI** | WinForms 4.8, WPF 4.8 Sync-Clients |
| Security | **Gemini CLI** | SonarQube, IaC-Scan, Tenant-Isolation |
| DevOps | **Gemini CLI / ChatGPT** | Bicep, GitHub Actions, Blue-Green |

---

## 🏗️ Was wir *schon* gebaut haben (Sprint 0 & 1)

1. **Repository & Git-Flow**  
main ────────► prod (blue-green ACA)
│
develop ─────► dev (auto-deploy)
│
feature/xyz ─► PR → SonarQube → Merge

2. **Bicep-Basis**  
- 3 Umgebungen (`dev`, `stage`, `prod`) mit eigenen RGs  
- KeyVault, Blob Storage, Service Bus, Log Analytics – alles per `az deployment` in < 5 min.

3. **Aspire-Orchestrierung**  
`dotnet run --project src/Aspire.AppHost` → API, Angular-SSR und Service Bus Emulator starten lokal – keine Docker-Compose-Files mehr nötig.

4. **Tenant-Isolation POC**  
- Datenbank pro Mandant (SQLite → Postgres)  
- MassTransit filtert Events nach `TenantId` Header – keine Cross-Tenant-Leaks.

5. **End-to-End Flow**  
Alice lädt über WinForms-Client eine Datei hoch →  
Charles ruft im Browser die Metadaten ab →  
David lädt sie im Tablet herunter – alles in 3 Sekunden.

---

## 📊 Zahlen nach 10 Tagen

| Metrik | Stand |
|--------|-------|
| Story-Punkte | 37 / 37 |
| Build-Zeit | 1 min 48 s |
| Test-Coverage | 83 % |
| Kritische Sonar-Findings | 0 |
| Uptime Dev-Umgebung | 99.9 % |
| Kosten Dev (Azure) | 3,47 € / Tag |

---

## 🚀 Geplante Meilensteine

| Sprint | Ziel | ETA |
|--------|------|-----|
| **Sprint 2** | Externe-Einladung + Time-Box-Shares | 29.07. |
| **Sprint 3** | Regionales Blue-Green (WEU+EUS2) | 12.08. |
| **Sprint 4** | Offline-Modus Tablet (Delta-Sync) | 26.08. |
| **Sprint 5** | Erste Fremdmandanten (Troja, Pompeji) | 09.09. |

---

## 🧩 Learnings (bisher)

1. **Klare instruct-*.md sind Gold** – jede KI weiß genau, was sie liefert.  
2. **Bicep + Aspire = ❤️** – Infrastructure drift fällt weg, weil jede Änderung im PR mitscant.  
3. **Tenant-Isolation früh testen** – ein einzelner Unit-Test pro Story rettet Tage später.  
4. **Legacy-Clients nicht vergessen** – ClickOnce-Kanal im GitHub Workflow war 3 Zeilen YAML.

---

## 🌱 Wünsche & Roadmap

- **Terraform-Import** aus Bicep für Multi-Cloud-Sandbox (AWS, GCP).  
- **AI-generierte Playwright-Tests** aus User-Story-Gherkin.  
- **Usage Analytics** via Aspire Telemetry + PowerBI.  
- **Delphi-Native-Bridge** für alte ERP-Systeme (kommt Sprint 3).

---

## 📸 Impressionen

![Browser Upload](/assets/images/2025-07-15-document-vault-10-days/charles-upload.svg)  
*Charles lädt im Browser hoch – 2 Klicks.*

![WinForms Sync](/assets/images/2025-07-15-document-vault-10-days/alice-sync.svg)  
*Alice sieht Datei 5 Sekunden später im Explorer.*

---

Wenn du tiefer einsteigen willst:  
- [Repo](https://github.com/atlantis-ds/dokumentenablage)  
- [ADR-Sammlung](https://github.com/atlantis-ds/dokumentenablage/tree/main/docs/adr)  
- [Live-Demo](https://dev.dokumentenablage.atlantis.io) *(freigegeben für Atlantis-Mitarbeiter)*

**Nächster Blog-Post:** *„Wie wir Terraform aus Bicep erzeugen – ohne Terraform zu schreiben“*