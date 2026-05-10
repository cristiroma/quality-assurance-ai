# Release checklist – template

> Copiază acest checklist într-un ticket Redmine de tip "Release" la începutul fiecărui ciclu.

# Release [YYYY-MM-DD] – v[X.Y.Z]

## T-5: Code freeze

- [ ] Branch `release/YYYY-MM-DD` creat din `develop`
- [ ] Toate ticketele incluse listate în descrierea ticketului
- [ ] Ticketele care NU intră au fost mutate înapoi în backlog
- [ ] Deploy automat pe staging trecut
- [ ] DB staging refresh din prod (cu sanitization) făcut

## T-4..T-2: QA execution

- [ ] Smoke test Playwright – verde pe staging
- [ ] Regression checklist (`projects/<proiect>/checklists/release-regression-checklist.md`) executat
- [ ] Test cases pentru ticketele incluse executate
- [ ] Visual regression – diferențe revizuite și aprobate / respinse
- [ ] Accessibility scan – fără regresii critical/serious
- [ ] Lighthouse – în limitele bugetului
- [ ] Cross-browser: Chrome ✓ Firefox ✓ Safari ✓
- [ ] Responsive: mobile ✓ tablet ✓ desktop ✓

## T-2: Bug bash (1h)

- [ ] Sesiune programată în calendar
- [ ] Toți participanții au acces la staging
- [ ] Bugs găsite create în Redmine cu tag `release-YYYY-MM-DD`
- [ ] Triere imediată după sesiune

## T-1: Final fixes & re-test

- [ ] Bugs S1/S2 fixed și re-testate
- [ ] Bugs S3/S4 mutate la următorul release dacă nu sunt rezolvate
- [ ] Smoke test final pe staging – verde
- [ ] Release notes scrise

## T-1: QA sign-off

- [ ] Toate criteriile QA Gate 4 îndeplinite (vezi `processes/release-process.md`)
- [ ] Comment în ticket Redmine: `QA sign-off ✅` de Laura
- [ ] PM aprobă deployment

## T (deploy day)

- [ ] DB snapshot prod înainte de deploy
- [ ] Tag git: `prod-YYYY-MM-DD`
- [ ] Deploy via GitHub Actions
- [ ] `drush updb`, `drush cr`, `drush cim` rulate fără erori
- [ ] Smoke test automat pe prod – verde
- [ ] Smoke manual: 5 user journeys critice
- [ ] Sentry / logs monitorizate 2h post-deploy
- [ ] Release notes publicate (intern + către client)
- [ ] Anunț Slack / email către echipă

## T+1: Retro mini

- [ ] Ce a mers bine
- [ ] Ce nu a mers
- [ ] Action items asignate

---

## Rollback plan (dacă e nevoie)

1. `git revert` tag-ul `prod-YYYY-MM-DD` și redeploy
2. Restore DB snapshot dacă au fost migrations care au stricat date
3. Comunicare client în max 30 min
4. Postmortem în 48h
