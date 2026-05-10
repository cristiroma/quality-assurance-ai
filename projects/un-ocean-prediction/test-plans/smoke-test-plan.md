# Smoke test plan – UN Ocean Prediction

Smoke = "does the application turn on?". Suite **scurtă (< 5 min)** rulată la fiecare deploy pe staging și prod.

## Scope

10 verificări critice. Dacă oricare pică → release este BLOCAT.

## Test cases

### ST-001: Homepage loads
- **URL**: `/`
- **Steps**: GET `/` → status 200, conținut homepage vizibil (titlu, meniu)
- **Assertion**: `expect(page.locator('header')).toBeVisible()`

### ST-002: Atlas page loads with iframe
- **URL**: `/en/atlas`
- **Assertion**: iframe-ul `cartography.unoceanprediction.org` se încarcă; status 200

### ST-003: Map renders inside iframe
- **Page**: `/en/atlas`
- **Assertion**: în `frameLocator()` → element canvas/svg al hărții vizibil în < 10s

### ST-004: Login flow works
- **Page**: `/user/login`
- **Steps**: completează test user → submit
- **Assertion**: redirect la pagina logged-in; cookie de sesiune setat

### ST-005: Logged-in user can access profile
- **After login**
- **Assertion**: `/user` page returnează 200, afișează username

### ST-006: Logout works
- **Assertion**: după logout, accesul la `/user/edit` returnează redirect către login

### ST-007: User can see list of forecast models
- **URL**: pagina listare modele (TBD)
- **Assertion**: cel puțin 1 model afișat

### ST-008: Search works (if exists)
- **Assertion**: search box returnează rezultate pentru query cunoscut

### ST-009: JSON:API endpoint răspunde
- **URL**: `/jsonapi/node/forecast_model` (TBD)
- **Assertion**: status 200, Content-Type `application/vnd.api+json`

### ST-010: No critical Drupal errors în log
- **Assertion**: după rularea pașilor 1–9, `drush watchdog:show --severity=Error` returnează 0 entries noi

## Configurare execuție

### Local
```bash
npx playwright test --grep @smoke
```

### CI (staging)
- Trigger: după deploy pe staging (workflow `qa-staging.yml`)
- Așteptare: max 5 min
- Notificare: Slack channel `#qa-alerts` la failure

### CI (production)
- Trigger: după deploy pe prod
- Subset: doar ST-001, ST-002, ST-003, ST-007, ST-009 (read-only, no login pe prod)
- Notificare: PagerDuty / SMS la failure (TBD)

## Test data

| Test user | Email | Role | Password |
|---|---|---|---|
| qa-smoke-user-1 | qa.smoke@test.local | authenticated | (vault) |

> Prod: NU folosim test users pe prod. Doar smoke read-only public.

## Owner & maintenance

- **Owner**: Laura
- **Review**: lunar, sau după orice incident
- **Update trigger**: orice CUJ nou sau breaking change în UI
