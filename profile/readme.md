# IMBA Baseline Autopilot

IMBA automatisiert die Erstellung einer sicheren CI-Baseline per Pull Request und ergänzt den Workflow um Monitoring, Security- und SEO-Checks sowie Conversion-Utilities.

## Warum IMBA?
- **Schneller Start**: Baseline-PR in Minuten statt Stunden
- **Konsistenz**: Policies & Recipes sorgen für reproduzierbare Standards
- **Transparenz**: Runs + Evidence + Exporte statt „Blackbox“
- **Betrieb**: Monitoring + Schedules + Regression-Alerts

## Features
### Wizard (Baseline-Composer)
- GitHub-App-Installationen laden, Repo auswählen
- Baselines: `secure-ci` / `secure-ci+obs`
- Policies (Org): z. B. Trivy blocking Pflicht, Overwrite verboten
- Diff-Preview: Required/Optional/Konflikt-Badges
- Safety-Rail: Overwrite nur mit Modal + Type-to-confirm

### Runs / Monitor
- Live-Status via SSE, Filter & Auto-Refresh
- Failure-Classifier + Tags
- Artefakt-Snippets und Download-Links

### Security Check
- Verdicts: **Threat / Suspicious / Hardening**
- Evidence mit Confidence/Weights, Filter/Sort
- Export (JSON/CSV), Share-Link (TTL), Domain-Allowlist (Hardening-mute)

### SEO Check & Monitoring
- Meta/Canonical/Robots/X-Robots, OG/Twitter, hreflang
- Sitemap/robots Checks, Link/Image Sampling
- Structured Data Sanity Checks
- Lab-Performance (synthetic) + Warnungen
- Historie + Schedules + Regression-Alerts

### Convert
- Batch-Uploads (Markdown ↔ PDF/DOCX), Presets
- OCR optional, Limits & TTL, Retry/Delete

## Quickstart
1. Installiere die GitHub App in deiner Organisation.
2. Öffne den Wizard, wähle Repo & Baseline und erstelle die PR.
3. Verfolge den Run im Monitor und prüfe Artefakte/Findings.

## Docs
- Quickstart, FAQ, Troubleshooting: **/docs**
- Status & Changelog: **/docs/status**, **/docs/changelog**

## Repositories (empfohlen pinnen)
- `imba-starter-kit`
- `imba-baseline-autopilot` (oder Hauptrepo)
- `docs`
- `examples`

## Trust & Grenzen
- Security/SEO sind Web-Scans (HTTP/HTML/Heuristiken + optional Threat-Intel), kein Endpoint-/AV-Scan.
- Share-Links/Downloads sind TTL-basiert; Uploads werden nicht dauerhaft gespeichert.

## Contributing
PRs willkommen. Bitte zuerst Issue/Discussion eröffnen.
