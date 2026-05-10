# Test plan – template

Inspirat din IEEE 829, simplificat pentru proiecte web agile.

---

# Test plan: [Nume release / feature / proiect]

| | |
|---|---|
| **Document version** | 1.0 |
| **Author** | |
| **Date** | YYYY-MM-DD |
| **Status** | Draft / Approved |
| **Approvers** | PM, Tech Lead, QA Lead |

## 1. Introduction & scope

### 1.1 Ce se testează
> Lista clară de feature-uri / module / pagini.

### 1.2 Ce NU se testează (out of scope)
> La fel de important. Ex. "Nu testăm performanța sub load > 100 utilizatori concurenți".

### 1.3 Referințe
- Redmine epic / version: 
- Specificații funcționale: 
- Mockups: 

## 2. Test strategy

### 2.1 Tipuri de testare aplicate
- [ ] Smoke
- [ ] Functional / E2E
- [ ] Regression
- [ ] Visual regression
- [ ] Accessibility (WCAG 2.1 AA)
- [ ] Performance (Lighthouse)
- [ ] Cross-browser (Chrome, Firefox, Safari)
- [ ] Responsive (mobile, tablet, desktop)
- [ ] Security (basic – OWASP top 10 awareness)

### 2.2 Distribuție manual vs. automat
| Categorie | Manual | Automat |
|---|---|---|
| Happy paths | 0% | 100% |
| Edge cases | 30% | 70% |
| Exploratory | 100% | 0% |

## 3. Test environment

| Environment | URL | Purpose | Refresh |
|---|---|---|---|
| Local | http://atlas.lndo.site | Dev | n/a |
| Staging | https://staging.unoceanprediction.org | QA pre-release | weekly from prod |
| Production | https://unoceanprediction.org | Live | n/a |

- Test users: vezi vault.
- Browsers: Chrome (latest, latest-1), Firefox (latest), Safari (latest).
- Devices: Desktop 1920×1080, Laptop 1366×768, iPad, iPhone 14.

## 4. Entry / exit criteria

### Entry criteria
- [ ] Build deployat pe staging
- [ ] Smoke test automat verde
- [ ] Toate ticketele incluse au status `Resolved`
- [ ] Test data pregătită

### Exit criteria
- [ ] 100% test cases planificate executate
- [ ] 0 bugs S1, S2 deschise
- [ ] < 5 bugs S3 deschise (cu acordul PM)
- [ ] Sign-off QA în Redmine

## 5. Test deliverables

- Test cases (link la doc / wiki)
- Test execution report (Playwright HTML report)
- Bug list (Redmine query)
- Sign-off email

## 6. Schedule

| Activity | Start | End | Owner |
|---|---|---|---|
| Test design | | | |
| Test execution round 1 | | | |
| Bug fixing | | | |
| Re-test | | | |
| Sign-off | | | |

## 7. Risks & mitigation

| Risk | Probability | Impact | Mitigation |
|---|---|---|---|
| Iframe Nuxt nu sincronizat cu Drupal release | Med | High | Test cross-version pe staging |
| Test data anonimizat insuficient | Low | High | Review script anonimizare |
| | | | |

## 8. Roles & responsibilities

| Role | Person | Responsibility |
|---|---|---|
| QA Lead / Tester | Laura | Test design, execution, sign-off |
| Tech Lead | | Code review, test infrastructure |
| Devs | | Unit tests, bug fixing |
| PM | | Priorities, sign-off business |
