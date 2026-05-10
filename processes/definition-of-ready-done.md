# Definition of Ready (DoR) și Definition of Done (DoD)

Aceste criterii sunt **gating** – un task care nu le îndeplinește nu trece mai departe.

## Definition of Ready (înainte ca un task să intre în Sprint / In Progress)

Un task (feature, bugfix, improvement) este **Ready** dacă:

- [ ] Are descriere clară: context, ce trebuie făcut, de ce.
- [ ] Are **acceptance criteria** explicite (preferabil în format Given/When/Then).
- [ ] Are estimate (story points sau ore).
- [ ] Pentru bug-uri: are steps to reproduce și severitate.
- [ ] Dependențele sunt identificate (alte taskuri, acces la API-uri externe, decizii de design).
- [ ] Are owner clar (un singur developer assignee).
- [ ] Pentru feature-uri vizuale: există mockup / wireframe sau confirmation că nu e nevoie.
- [ ] Impactul asupra altor zone (ex. cache, hartă Nuxt, autentificare) este menționat.

## Definition of Done (criterii pentru a închide un task)

Un task este **Done** dacă:

### Cod
- [ ] Codul respectă Drupal coding standards (PHPCS clean) și ESLint pentru JS / Nuxt.
- [ ] PHPStan trece la nivelul configurat al proiectului fără regresii.
- [ ] Pull request creat, review-uit și aprobat de cel puțin 1 alt developer (tech lead pentru zone critice).
- [ ] Nu introduce warning-uri noi în Drupal log sau în consola browserului.
- [ ] Configurări exportate (`drush cex`) și commit-uite dacă au fost modificări de config.

### Testare
- [ ] Developer-ul a testat local happy path + cel puțin 1 edge case.
- [ ] Pentru bug-uri scăpate dintr-o zonă acoperită de teste E2E, există test de regresie.
- [ ] Pentru feature-uri noi de UI critice, Laura a adăugat un smoke test Playwright (sau a deschis ticket pentru asta).
- [ ] CI pipeline e verde (lint + teste existente).
- [ ] Testat de Laura pe staging și mutat în `Closed` în Redmine.

### Documentație
- [ ] README / docs actualizate dacă s-au schimbat pași de instalare, env vars, comenzi.
- [ ] Release notes / changelog actualizate (one-liner per task).
- [ ] Dacă schimbă comportament observabil de utilizator: notă pentru client.

### Deployment
- [ ] Merged pe branch-ul de release.
- [ ] Deployed pe staging via GitHub Actions.
- [ ] Update path verificat (drush updb, cache rebuild) fără erori.
