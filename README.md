# <img src="https://cdn.simpleicons.org/snyk/4C4A73" height="32" align="center" /> Snyk Dependency Security Scan — manuelaklenke.com

Automated dependency vulnerability scanning for all manuelaklenke.com repositories using Snyk. Runs after every deployment and publishes reports to GitHub Pages.

---

## 📊 Security Report

Latest report: **[https://georget88.github.io/manuelaklenke-snyk-security/](https://georget88.github.io/manuelaklenke-snyk-security/)**

---

## 🛠️ Tech Stack

- [Snyk](https://snyk.io/) — dependency vulnerability scanner
- [snyk-to-html](https://github.com/snyk/snyk-to-html) — HTML report generator
- GitHub Actions — CI/CD pipeline
- GitHub Pages — report hosting

---

## 🔍 What Gets Scanned

All four repositories with npm dependencies:

| Repository | Dependencies |
|---|---|
| manuelaklenke-web | React, MUI, Supabase, Vite, i18next, etc. |
| manuelaklenke-playwright-e2e | Playwright |
| manuelaklenke-selenium-e2e | Selenium, Mocha, Allure, Chai |
| manuelaklenke-cypress-e2e | Cypress, Mochawesome |

Snyk checks each `package.json` against its vulnerability database and reports:
- Known CVEs in direct and transitive dependencies
- Severity level (Critical, High, Medium, Low)
- Fix recommendations (upgrade paths)

---

## ⚙️ CI/CD Pipeline

The scan is triggered automatically by [GeorgeT88/manuelaklenke-web](https://github.com/GeorgeT88/manuelaklenke-web) after every push to `main`, once all E2E tests have completed. Snyk runs in parallel with Semgrep SAST:

```
📦 Push to manuelaklenke-web
        ↓
⏳ Vercel deployment confirmed live
        ↓
🎭 Playwright + 🔬 Selenium + 🌲 Cypress (parallel)
        ↓
🛡️ OWASP ZAP — skipped (manual/nightly only)
        ↓
⚡ repository_dispatch: vercel-deploy  ←─ Snyk + Semgrep triggered in parallel
        ↓
🔒 Snyk scans all 4 repos
        ↓
📊 HTML report published to GitHub Pages
```

The scan can also be triggered manually from **Actions → Snyk Dependency Security Scan → Run workflow**, and runs on a nightly schedule at **07:00 UTC**.

---

## 🏷️ Run Name Convention

| Trigger | Run name |
|---|---|
| Push via app repo | `Snyk Dependency Scan — triggered by Vercel deploy` |
| Manual | `Snyk Dependency Scan — manual run` |
| Nightly schedule (07:00 UTC) | `Snyk Dependency Scan — nightly run` |
