# Plan QA – primele 30 de zile (11 mai – 9 iunie 2026)

Obiectiv: până la sfârșitul lunii avem un cadru QA funcțional, primul release bi-weekly livrat cu sign-off formal, și Laura cu primele 3 teste Playwright scrise.

## Săptămâna 1: 11–15 mai – Discovery & setup

### Goals
- Cunoaștere completă a aplicației și echipei.
- Acces la toate mediile.
- Procese de bază comunicate echipei.

### Activități
| Zi | Activitate | Owner | Output |
|---|---|---|---|
| Lun | Kickoff meeting (toată echipa, 1h). Prezentare contract, roluri, procese. | QA Manager | Notes + slack channel |
| Lun | Setup acces: Redmine, GitHub, staging, prod (read-only), VPN. | Tech Lead | Acces verificat |
| Mar | Tour aplicației cu PM (1h). Identificare CUJs preliminare. | Laura + PM | Listă brută CUJs |
| Mar | Code walkthrough (1h cu tech lead): structura repo Drupal + Nuxt, branching, deploy. | Laura + Tech Lead | Notes |
| Mie | Audit issue tracker: bugs deschise, istoric ultimele 3 luni, zone cu cele mai multe regresii. | Laura | Listă top 10 zone problematice |
| Mie | Setup local environment Drupal (lando/ddev). | Laura + Dev | Local working |
| Joi | Documentare CUJs în `critical-user-journeys.md`. Review cu PM. | Laura | Doc finalizat |
| Joi | Setup Playwright local: `npm init playwright@latest` în repo. | Laura + Tech Lead | playwright.config.ts |
| Vin | Risk assessment workshop (1h). Output: `risk-assessment.md`. | Toată echipa | Risk matrix |
| Vin | Comunicare procese (DoR, DoD, bug template) către dezvoltatori. | QA Manager | Email + doc shared |

### Deliverables săpt 1
- ✅ `critical-user-journeys.md` complet
- ✅ `risk-assessment.md` complet
- ✅ Playwright setup în repo (gol, dar funcțional)
- ✅ Procese comunicate

---

## Săptămâna 2: 18–22 mai – Smoke suite + primul release pregătit

### Goals
- 3 smoke tests Playwright scrise (cu codegen).
- Regression checklist v1.
- Branch `release/2026-05-27` creat și testat.

### Activități
| Zi | Activitate | Owner | Output |
|---|---|---|---|
| Lun | Pair session 2h: înregistrare codegen pentru flow login. | Laura + Dev | `tests/e2e/auth/login.spec.ts` |
| Mar | Codegen: navigare home → atlas page → filtru hartă. | Laura | `tests/e2e/atlas/basic-navigation.spec.ts` |
| Mar | CI workflow draft: `.github/workflows/qa-smoke.yml` (doar manual trigger). | Tech Lead | Workflow file |
| Mie | Codegen: profil utilizator (view + edit name). | Laura | `tests/e2e/profile/edit-profile.spec.ts` |
| Mie | Test data: creare 2 utilizatori de test în staging cu drush. Documentare credentials în vault. | Tech Lead + Laura | Users created |
| Joi | Regression checklist v1 (40–60 itemi manuali). | Laura | `checklists/release-regression-checklist.md` |
| Joi | Test smoke pe staging: rulare manuală + raport bugs găsite. | Laura | Bugs raportate în Redmine |
| Vin | Bug triage cu tech lead. | Laura + Tech Lead | Bugs prioritizate |
| Vin | Release planning meeting pentru `release/2026-05-27`. | Toată echipa | Lista taskuri incluse |

### Deliverables săpt 2
- ✅ 3 teste Playwright (smoke) verzi pe local
- ✅ CI workflow QA smoke (manual trigger)
- ✅ Regression checklist v1
- ✅ Release scope definit

---

## Săptămâna 3: 25–29 mai – Primul release sub procesul nou

### Goals
- Release `2026-05-27` livrat cu sign-off formal.
- Toate gates trecute (chiar dacă imperfect).
- Lessons learned documentate.

### Activități
| Zi | Activitate | Owner |
|---|---|---|
| Lun (T-2) | Code freeze. `release/*` branch creat. Deploy staging. | Tech Lead |
| Lun | Bug bash 1h, toată echipa pe staging. | Toți |
| Mar (T-1) | QA execution: smoke automat + regression checklist + test cases pe taskuri. | Laura |
| Mar | Bug fixing critical only. | Devs |
| Mar evening | Re-test. QA sign-off în Redmine. | Laura |
| Mie (T) 10:00 | Deploy producție. Smoke automat pe prod. | Tech Lead |
| Mie 10:30–12:30 | Smoke manual + monitoring. | Laura |
| Joi (T+1) | Retro 30 min. Action items. | Toți |
| Vin | Update procese pe baza retro-ului. Începe pregătirea release-ului următor. | QA Manager |

### Deliverables săpt 3
- ✅ Release deployed
- ✅ Sign-off formal documentat
- ✅ Retro notes + action items
- ✅ Process v1.1 (ajustat după realitate)

---

## Săptămâna 4: 1–5 iunie – Consolidare + învățare

### Goals
- Refactor primele teste Playwright (de la codegen la cod curat).
- Începere POM (Page Object Model) pe 1 zonă.
- Metrici inițiale măsurate.

### Activități
| Zi | Activitate | Owner |
|---|---|---|
| Lun | Pair session: refactor `login.spec.ts` cu locatori `getByRole`/`getByLabel`. | Laura + Dev |
| Lun | Citire `processes/release-process.md`, întrebări, propuneri îmbunătățire de la Laura. | Laura |
| Mar | Începere `pages/LoginPage.ts` (primul Page Object). | Laura |
| Mie | Adăugare 2 teste noi pentru CUJs neacoperite. | Laura |
| Joi | Calcul metrici prim luna: escape rate, MTTR, regression rate, coverage. | Laura + QA Manager |
| Joi | Document `metrics-2026-05.md` în `projects/un-ocean-prediction/`. | QA Manager |
| Vin | 1:1 Laura: review luna 1, ajustare plan luna 2. | QA Manager + Laura |
| Vin | Planning luna 2 + scope release `2026-06-10`. | Toată echipa |

### Deliverables săpt 4
- ✅ 1 Page Object scris
- ✅ 5+ teste Playwright total
- ✅ Raport metrici luna 1
- ✅ Plan luna 2 ajustat

---

## Risc-uri pentru primele 30 zile

| Risc | Probabilitate | Impact | Mitigare |
|---|---|---|---|
| Acces întârziat la medii | Medie | Mare | Cere acces în prima zi, nu prima săpt |
| Staging instabil sau cu date stricate | Medie | Mare | Refresh DB din prod cu sanitization, scriptat |
| Laura overwhelmed cu volumul de info | Mare | Mediu | Block 1h/zi pentru learning, fără task-uri urgente |
| Devs nu adoptă DoR/DoD | Mare | Mare | Tech lead aliniat înainte; review în retro săpt 3 |
| Bugs urgente de la client în prima săpt distrag de la setup | Mare | Mediu | Tech lead absoarbe primul, Laura urmărește dar nu blochează |
| Iframe Nuxt complex de testat | Medie | Mediu | Pair session dedicat în săpt 2 |

## Indicatori de succes la 30 zile

- [ ] 5+ teste Playwright scrise și verzi
- [ ] 1+ release livrat cu sign-off formal
- [ ] 0 bugs S1 în prod scăpate prin smoke suite
- [ ] Toți devs au folosit DoR/DoD pe cel puțin 1 task
- [ ] Laura: confort cu Playwright codegen + început de cod manual
- [ ] Metrici inițiale măsurate și raportate
