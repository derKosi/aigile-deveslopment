---
layout: post
title: "Sejf dokumentów w 10 dni – MVP zbudowany przez ekipę all-AI"
date: 2025-07-15
author: derKosi
lang: pl
translation_id: dokumentenablage-in-10-tagen
tags: [AI-Team, Aspire, Azure, Bicep, Angular, Git-Flow]
---

> **TL;DR**  
> W ciągu tygodnia – całkowicie bez ludzkich commitów – stworzyliśmy wielodostępny magazyn dokumentów dla firmy Atlantis, **uruchomiliśmy go na żywo** w Azure, a nawet zsynchronizowaliśmy Alicję i Boba. Sekret: zdyscyplinowany podział ról między Kimi K2, GitHub Copilot i Gemini CLI oraz czysty Git-Flow + Bicep.

---

## 🤖 Zespół w skrócie

| Rola | Model AI | Główna odpowiedzialność |
|-------|-----------|---------------------|
| Konsultant / Architekt | **Kimi K2** | ADRy, model zagrożeń, przegląd kosztów |
| Product Owner | **GitHub Copilot** | Backlog, Gherkin AC, wydania |
| Backend Dev | **Gemini CLI** | .NET 9 Aspire API, EF Core, MassTransit |
| Frontend Dev | **Gemini CLI** | Angular 18, PWA, UX przesyłania |
| Legacy Dev | **Gemini CLI** | Klienci synchronizacji WinForms 4.8, WPF 4.8 |
| Bezpieczeństwo | **Gemini CLI** | SonarQube, skanowanie IaC, izolacja najemców |
| DevOps | **Gemini CLI / ChatGPT** | Bicep, GitHub Actions, Blue-Green |

---

## 🏗️ Co *już* zbudowaliśmy (Sprint 0 i 1)

1. **Repozytorium i Git-Flow**  
main ────────► prod (blue-green ACA)
│
develop ─────► dev (auto-deploy)
│
feature/xyz ─► PR → SonarQube → Merge

2. **Podstawa Bicep**  
- 3 środowiska (`dev`, `stage`, `prod`) z własnymi grupami zasobów  
- KeyVault, Blob Storage, Service Bus, Log Analytics – wszystko za pomocą `az deployment` w < 5 min.

3. **Orkiestracja Aspire**  
`dotnet run --project src/Aspire.AppHost` → API, Angular-SSR i emulator Service Bus uruchamiają się lokalnie – nie potrzeba już plików Docker-Compose.

4. **POC izolacji najemców**  
- Baza danych na najemcę (SQLite → Postgres)  
- MassTransit filtruje zdarzenia według nagłówka `TenantId` – brak wycieków między najemcami.

5. **Przepływ End-to-End**  
Alicja przesyła plik za pomocą klienta WinForms →  
Charles pobiera metadane w przeglądarce →  
David pobiera go na tablecie – wszystko w 3 sekundy.

---

## 📊 Liczby po 10 dniach

| Metryka | Stan |
|--------|-------|
| Punkty fabuły | 37 / 37 |
| Czas budowy | 1 min 48 s |
| Pokrycie testami | 83 % |
| Krytyczne znaleziska Sonar | 0 |
| Czas pracy środowiska deweloperskiego | 99.9 % |
| Koszty deweloperskie (Azure) | 3,47 € / dzień |

---

## 🚀 Planowane kamienie milowe

| Sprint | Cel | ETA |
|--------|------|-----|
| **Sprint 2** | Zewnętrzne zaproszenia + udziały czasowe | 29.07. |
| **Sprint 3** | Regionalne Blue-Green (WEU+EUS2) | 12.08. |
| **Sprint 4** | Tryb offline na tablecie (synchronizacja Delta) | 26.08. |
| **Sprint 5** | Pierwsi najemcy zewnętrzni (Troja, Pompeje) | 09.09. |

---

## 🧩 Wnioski (do tej pory)

1. **Jasne instrukcje-*.md są na wagę złota** – każda sztuczna inteligencja wie dokładnie, co ma dostarczyć.  
2. **Bicep + Aspire = ❤️** – dryf infrastruktury jest wyeliminowany, ponieważ każda zmiana jest skanowana w PR.  
3. **Wczesne testowanie izolacji najemców** – jeden test jednostkowy na historię oszczędza dni później.  
4. **Nie zapominaj o starszych klientach** – kanał ClickOnce w przepływie pracy GitHub to 3 linijki YAML.

---

## 🌱 Życzenia i mapa drogowa

- **Import Terraform** z Bicep dla piaskownicy wielochmurowej (AWS, GCP).  
- **Testy Playwright generowane przez AI** z Gherkin historii użytkownika.  
- **Analityka użytkowania** za pomocą Aspire Telemetry + PowerBI.  
- **Most natywny Delphi** для starych systemów ERP (w Sprincie 3).

---

## 📸 Wrażenia

![Przesyłanie w przeglądarce](/assets/images/2025-07-15-document-vault-10-days/charles-upload.svg)  
*Charles przesyła w przeglądarce – 2 kliknięcia.*

![Synchronizacja WinForms](/assets/images/2025-07-15-document-vault-10-days/alice-sync.svg)  
*Alicja widzi plik 5 sekund później w eksploratorze.*

---

Jeśli chcesz dowiedzieć się więcej:  
- [Repozytorium](https://github.com/atlantis-ds/dokumentenablage)  
- [Zbiór ADR](https://github.com/atlantis-ds/dokumentenablage/tree/main/docs/adr)  
- [Demo na żywo](https://dev.dokumentenablage.atlantis.io) *(zatwierdzone dla pracowników Atlantis)*

**Następny wpis na blogu:** *„Jak generujemy Terraform z Bicep – bez pisania Terraform”*