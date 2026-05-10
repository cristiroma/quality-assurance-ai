# UN Ocean Prediction Atlas – QA project overview

## Overview

Portal de informații despre **modele oceanice de forecasting**, cu utilizatori autentificați care pot:
- Adăuga / edita organizația lor pe hartă
- Adăuga modele de forecasting (cu metadata: tip, regiune, accuracy etc.)
- Documenta "use cases" legate de modele oceanice
- Vizualiza informații pe o hartă interactivă

## URLs

| Environment | URL |
|---|---|
| Production (site) | https://www.unoceanprediction.org/ |
| Production (atlas page) | https://www.unoceanprediction.org/en/atlas |
| Cartography app (iframe) | https://cartography.unoceanprediction.org/ |
| Staging | TBD |
| Local dev | TBD |

## Tech stack

| Layer | Tech | Notes |
|---|---|---|
| CMS | **Drupal 10** | Site principal, autentificare, content management |
| Cartography app | **Nuxt** | Aplicație separată embedded ca iframe în pagina `/en/atlas` |
| Hosting | Self-hosted | Self-hosted GitHub Actions runner pentru CI/CD |
| CI/CD | **GitHub Actions** | Deploy pe staging + prod deja configurat |
| Issue tracker | **Redmine** (https://helpdesk.eaudeweb.ro/) | |

## Echipa

| Rol | Persoană | Alocare |
|---|---|---|
| Tech Lead | TBD | |
| Developer 1 | TBD | |
| Developer 2 | TBD | |
| QA | Laura | 16h/săptămână |
| PM | TBD | |

## Limba și audiența

- **Limba**: doar Engleză (nu este multilingv, deci scope-ul de testare i18n este limitat).
- **Audiența**: utilizatori autentificați (researchers, organizații marine, contributori de modele).

## Contract

- **Tip**: mentenanță, bugfixing, îmbunătățiri
- **Început**: 2026-05-11
- **Frecvență release**: bi-weekly (probabil miercuri)
- **SLA contractual**: nu există – aplicăm SLA intern (vezi `processes/bug-lifecycle.md`)

## Considerații speciale pentru testare

### 1. Iframe cross-origin
Pagina `/en/atlas` este de fapt Drupal, dar ce vede utilizatorul este aplicația Nuxt din iframe. Asta înseamnă că:
- Testele E2E trebuie să folosească `frameLocator()` în Playwright.
- Bug-urile de pe `/en/atlas` pot fi în Drupal (shell) **sau** în Nuxt (conținut iframe). Triere clară necesară.
- Sincronizarea release-urilor între Drupal și Nuxt este critică.
- **Cypress nu este o opțiune** din cauza limitărilor cross-origin → folosim Playwright.

### 2. Funcționalitate principală: hartă interactivă
- Testarea hărților e mai complexă (Canvas, WebGL, sau SVG?). Verificăm tipul de rendering și adaptăm strategia.
- Visual regression e foarte util aici, dar și foarte fragil – necesită praguri tolerante.

### 3. Date geografice și formulare complexe
- Forecast models au probabil multe câmpuri custom (Drupal entities + paragraphs?).
- Validările formularelor sunt o zonă cu risc de bugs → coverage prioritar.

### 4. Roluri și permisiuni
Probabil avem cel puțin: anonymous, authenticated, model contributor, organization admin, site admin. Fiecare CUJ trebuie testat din perspectiva rolului relevant.

## Documente asociate

- [30-day plan](30-day-plan.md) – plan concret pentru primele 4 săptămâni
- [Risk assessment](risk-assessment.md)
- [Critical user journeys](critical-user-journeys.md)
- [Smoke test plan](test-plans/smoke-test-plan.md)
- [Release regression checklist](checklists/release-regression-checklist.md)

## Întrebări deschise / TODO discovery

- [ ] URL exact al staging environment
- [ ] Lista exactă a rolurilor și permisiunilor
- [ ] Numele dezvoltatorilor și disponibilitatea pentru pair sessions
- [ ] Există deja teste manuale documentate undeva?
- [ ] Backlog de bugs cunoscute din contractul anterior?
- [ ] Tipul de rendering al hărții (MapLibre/Leaflet/Mapbox/OpenLayers?)
- [ ] Dacă Nuxt repo e separat sau în același repo cu Drupal
- [ ] Ce monitoring e activ în prod (Sentry, New Relic, Matomo, GA?)
