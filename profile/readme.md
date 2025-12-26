<!--
IMBA Org Profile README
Pfad: .github/profile/README.md
Optional Assets: .github/profile/assets/
-->

<p align="center">
  <img src="assets/imba-banner.png" alt="IMBA Baseline Autopilot" width="900" />
</p>

<h1 align="center">IMBA Baseline Autopilot</h1>

<p align="center">
  GitHub App installieren • Baseline-PR erstellen • Status live verfolgen • Security/SEO Checks • Conversion Utilities
</p>

<p align="center">
  <a href="https://puzzlepos-cloud.de"><img alt="Website" src="https://img.shields.io/badge/Website-puzzlepos--cloud.de-0b7285"></a>
  <img alt="Status" src="https://img.shields.io/badge/Status-v1%20ready-2f9e44">
  <img alt="Stack" src="https://img.shields.io/badge/Stack-Node%20%7C%20GitHub%20Apps%20%7C%20SQLite-364fc7">
  <img alt="Focus" src="https://img.shields.io/badge/Focus-Secure%20CI%20Baselines%20%26%20Monitoring-5f3dc4">
</p>

---

## TL;DR
IMBA automatisiert das Einspielen einer **secure CI baseline** per Pull-Request und ergänzt den Workflow um **Live-Monitoring**, **Security- und SEO-Checks** sowie **Convert-Utilities**.  
Alles ist auf **Transparenz** (Evidence/Exports) und **Safety Rails** (Policies/Overwrite-Guards) ausgelegt.

---

## Produkt-Flows (High-Level)

```mermaid
flowchart LR
  GH[GitHub] -->|Webhooks| API[Autopilot API]
  UI[Web UI] -->|SSE subscribe| API
  API -->|SSE events| UI

  API --> RUNS[(runs.db)]
  API --> SEO[(seo.db)]

  API --> Q[Job Queue]
  Q --> SEC[Security Scan]
  Q --> SEOC[SEO Scan]
  Q --> CONV[Convert Jobs]

  SEC --> API
  SEOC --> API
  CONV --> API
```

---

## Features

<table>
  <tr>
    <td width="50%">
      <h3>Wizard</h3>
      <p><b>Repo wählen → Baseline auswählen → PR erstellen</b></p>
      <ul>
        <li>Baselines: <code>secure-ci</code>, <code>secure-ci+obs</code>, Recipes speichern/laden</li>
        <li>Org-Policies enforced (z. B. Trivy blocking Pflicht, Overwrite verboten)</li>
        <li>Diff-Preview: Required/Optional/Konflikt-Badges</li>
        <li>Overwrite-Safety-Rail: Modal + Type-to-confirm</li>
      </ul>
      <p><i>Screenshot:</i> <code>assets/screen-wizard.png</code></p>
    </td>
    <td width="50%">
      <h3>Monitor / Runs</h3>
      <p><b>Live-Status, Failure-Classifier, Artefakte</b></p>
      <ul>
        <li>SSE Live-Updates, Filter, Auto-Refresh</li>
        <li>Failure-Tags/Classifier (z. B. auth/repo/ci/security)</li>
        <li>Artefakt-Snippets + Download-Links (TTL)</li>
      </ul>
      <p><i>Screenshot:</i> <code>assets/screen-monitor.png</code></p>
    </td>
  </tr>

  <tr>
    <td width="50%">
      <h3>Security Check</h3>
      <p><b>Threat / Suspicious / Hardening</b> mit Evidence</p>
      <ul>
        <li>Threat-Intel optional (Safe Browsing, weitere Feeds)</li>
        <li>Headers/TLS/Redirect/Mixed Content/Cookies/Downloads/Runtime</li>
        <li>Evidence-Panel: Punkte + Confidence, Filter/Sort</li>
        <li>Export JSON/CSV, Share-Link (TTL), Allowlist (Hardening-mute)</li>
      </ul>
      <p><i>Screenshot:</i> <code>assets/screen-security.png</code></p>
    </td>
    <td width="50%">
      <h3>SEO Check & Monitoring</h3>
      <p>Technischer On-Page-Audit + Historie + Alerts</p>
      <ul>
        <li>Meta/Canonical/Robots/X-Robots, OG/Twitter, hreflang</li>
        <li>robots.txt + Sitemap Fetch/Parsing, deterministisches Sampling</li>
        <li>Broken Links/Images (Sample), JSON-LD sanity checks</li>
        <li>Monitoring: Schedules + History + Regression Alerts</li>
        <li>Performance: <b>Lab</b> (TTFB/FCP/LCP/CLS/INP) als Warnungen</li>
      </ul>
      <p><i>Screenshot:</i> <code>assets/screen-seo.png</code></p>
    </td>
  </tr>

  <tr>
    <td width="50%">
      <h3>Convert</h3>
      <p>Batch-Conversion (Markdown ↔ PDF/DOCX) mit Presets</p>
      <ul>
        <li>Presets: IMBA / Minimal / Dark</li>
        <li>OCR optional</li>
        <li>Limits: max 10 Dateien, 8 MB • Downloads via TTL</li>
        <li>Retry/Delete + History</li>
      </ul>
      <p><i>Screenshot:</i> <code>assets/screen-convert.png</code></p>
    </td>
    <td width="50%">
      <h3>Ops</h3>
      <p>Status & Logs für Webhook/App/Token</p>
      <ul>
        <li>Letzte Events, Test-Ping, Auto-Refresh</li>
        <li>Webhook-URL nur per Copy nach Installationswahl</li>
        <li>Status-Pills (API/Webhook/Queue)</li>
      </ul>
      <p><i>Screenshot:</i> <code>assets/screen-ops.png</code></p>
    </td>
  </tr>
</table>

---

## Architecture (kompakter Blick)
```mermaid
sequenceDiagram
  participant User
  participant UI as Web UI
  participant API as Autopilot API
  participant GH as GitHub
  participant Q as Queue

  User->>UI: Wizard: Repo + Baseline wählen
  UI->>API: Create PR request
  API->>GH: Create branch + PR
  GH-->>API: Webhook events (checks, status)
  API-->>UI: SSE events (live status)

  User->>UI: Trigger Security/SEO/Convert
  UI->>API: Start job
  API->>Q: Enqueue job
  Q-->>API: Job result
  API-->>UI: Result + evidence + exports
```

---

## Quickstart (für Nutzer)
1. GitHub App installieren (Org/Repo auswählen)
2. Wizard öffnen → Baseline auswählen → PR erstellen
3. Monitor öffnen → Live-Status, Artefakte, Findings

---

## Trust & Grenzen
- Security/SEO sind **Web-Scans** (HTTP/HTML/Heuristiken + optional Threat-Intel), **kein** Endpoint-/AV-Scan.
- Share-Links und Downloads sind **TTL-basiert** (laufen automatisch ab).
- Convert hat **harte Upload-Limits** und löscht Ergebnisse nach Ablauf.

---

## Repositories (empfohlen pinnen)
- `imba-starter-kit`
- `imba-baseline-autopilot` (oder Hauptrepo)
- `docs` / `runbooks` / `examples` (je nach Struktur)

---

## Assets (optional)
Lege Bilder hier ab:
- `.github/profile/assets/imba-banner.png`
- `.github/profile/assets/screen-wizard.png`
- `.github/profile/assets/screen-monitor.png`
- `.github/profile/assets/screen-security.png`
- `.github/profile/assets/screen-seo.png`
- `.github/profile/assets/screen-convert.png`
- `.github/profile/assets/screen-ops.png`

Wenn du (noch) keine Bilder hast: Entferne einfach den Banner-Block oben und die Screenshot-Zeilen.

---

## Kontakt / Contribution
- Issues: Bitte über GitHub Issues im passenden Repo
- Diskussionen/Feedback: GitHub Discussions (falls aktiviert)
