# Tooling QA – stack aprobat

## Reguli generale

- Folosim **un singur tool per categorie** ca să nu fragmentăm cunoașterea.
- Toate tool-urile sunt **open source** sau cu free tier suficient.
- Toate rezultatele se publică în **GitHub Actions artifacts** + Redmine.

## Stack pe categorii

### 1. End-to-End / UI testing
- **Playwright** (TypeScript) – tool principal.
  - Motiv: codegen pentru cei fără background de programare (Laura), debugging vizual (`--ui` mode), trace viewer, suport multi-browser nativ (Chromium, Firefox, WebKit).
  - Repo: `tests/e2e/` în repo-ul proiectului.
  - Config: `playwright.config.ts` cu projects pentru desktop + mobile.

### 2. Visual regression
- **Playwright snapshots** (`expect(page).toHaveScreenshot()`).
  - Motiv: integrat în același tool, fără infra suplimentară.
  - Alternativ: BackstopJS doar dacă apare nevoia de scenarii foarte complexe.

### 3. Accessibility
- **@axe-core/playwright** – integrat în testele E2E.
  - Rulează pe paginile critice; raportează violări `critical` și `serious`.
  - Standard țintă: **WCAG 2.1 AA**.

### 4. Performance
- **Lighthouse CI** (`@lhci/cli`) în GitHub Actions.
  - Buget: Performance ≥ 80, Accessibility ≥ 95, Best Practices ≥ 90, SEO ≥ 90.
  - Rulează pe top 5 pagini la fiecare PR pe `release/*`.

### 5. API testing
- **Playwright `request` fixture** pentru REST/JSON:API endpoints Drupal și API-ul Nuxt.

### 6. Static analysis (devs)
- **PHPStan** la nivel `level: 5` (creștem treptat la 6, 7).
- **PHPCS** cu `Drupal` și `DrupalPractice` standards.
- **ESLint** + Prettier pentru Nuxt.
- **drupal-rector** pentru deprecation fixes.

### 7. CI / orchestrare
- **GitHub Actions** cu self-hosted runner (deja configurat la voi).
- Workflow-uri sugerate:
  - `ci-pr.yml` – lint + unit + smoke (rulează pe fiecare PR)
  - `ci-staging.yml` – full regression după deploy pe staging
  - `ci-nightly.yml` – full suite + visual + a11y + performance, ora 03:00
  - `ci-prod-smoke.yml` – smoke după deploy în prod

### 8. Reporting
- **Playwright HTML reporter** publicat ca GitHub Pages branch.
- **Allure** – opțional, dacă apare nevoia de istoric și trend-uri.

### 9. Test data management
- **Drush** cu profile de testare + fixtures JSON pentru user creation.
- **Database sanitization** la sync prod → staging (anonymize emails, remove PII).

## Tool-uri **respinse** (și de ce)

| Tool | Motiv |
|---|---|
| Selenium | API verbose, mai puțin stabil decât Playwright; codegen mai slab |
| Cypress | Limitări pe multi-tab, multi-origin, iframe (avem iframe Nuxt!), no WebKit |
| TestCafe | Comunitate mai mică, ecosistem mai sărac |
| Behat | Ciclu de scriere lent pentru E2E vizuale; păstrăm pentru cazuri Drupal-specific dacă apar |

## Iframe Nuxt – considerație specială

Pagina `/en/atlas` conține iframe către `cartography.unoceanprediction.org`.
Playwright suportă cross-origin iframes nativ (`page.frameLocator()`), spre deosebire de Cypress care are limitări serioase. Acesta este un **motiv suplimentar tare** pentru Playwright.
