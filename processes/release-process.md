# Release process

## Cadență

- **Bi-weekly releases** pe miercuri (zi propusă – ajustabil).
- **Hotfix on-demand** pentru S1/S2 critice.

## Branching model

```
main          ──●─────────────●─────────────●──   (production, tag-uit la fiecare release)
                ↑             ↑             ↑
release/*    ──●──●──●──●──●──●──●──●──●──●──●──   (branch de release, deploy pe staging)
                ↑  ↑  ↑     ↑  ↑     ↑  ↑
develop      ──●──●──●─────●──●─────●──●─────────  (integrare zilnică)
                ↑  ↑        ↑        ↑
feature/*    ──●  ●        ●        ●
bugfix/*
hotfix/*     ────────────●─────────────────●────  (din main, merged înapoi în main + develop)
```

- `feature/REDMINE-1234-short-description`
- `bugfix/REDMINE-1234-short-description`
- `hotfix/REDMINE-1234-short-description`

## Timeline release bi-weekly (T = ziua release-ului)

| Ziua | Activitate | Owner |
|---|---|---|
| T-5 (vineri) | Code freeze pe `develop`. Se creează `release/YYYY-MM-DD`. Deploy pe staging. | Tech lead |
| T-4..T-2 | QA pe staging: regression checklist + test cases pentru taskurile incluse. | Laura |
| T-2 | Bug bash 1h (toată echipa explorează aplicația). | Toți |
| T-1 | Fixed only critical/major bugs. Re-test pe staging. | Devs + Laura |
| T-1 | QA sign-off: Laura aprobă în Redmine release ticket. | Laura |
| T (miercuri 10:00) | Deploy în producție. Smoke tests automate rulează în CI. | Tech lead |
| T (10:30) | Smoke manual + monitorizare logs 2h. | Laura |
| T+1 | Retro mini (15 min): ce a mers, ce nu. | Toți |

## QA Gates (criterii pentru sign-off)

Un release este aprobat de QA dacă:

1. ✅ Toate taskurile incluse au status `Closed` (verificate pe staging).
2. ✅ Smoke test suite automat (Playwright) trece 100% pe staging.
3. ✅ Regression checklist manual completat.
4. ✅ Niciun bug S1/S2 deschis în taskurile incluse.
5. ✅ Lighthouse score nu a scăzut cu mai mult de 5 puncte față de baseline.
6. ✅ Accessibility scan (axe) – fără regresii noi de tip `critical` sau `serious`.
7. ✅ Release notes scrise și aprobate de PM.

Dacă un criteriu nu e îndeplinit: decizie comună PM + tech lead + QA dacă se scoate task-ul din release sau se amână release-ul.

## Rollback

Pentru fiecare release:
- Tag git pe commit-ul de release: `prod-YYYY-MM-DD`.
- DB snapshot înainte de deploy (în GitHub Action).
- Procedură rollback documentată: revert tag + restore DB snapshot.
- Decizie de rollback: tech lead, în max 1h de la deploy dacă apare un S1.

## Componente speciale – Nuxt cartography app

Aplicația Nuxt de pe `cartography.unoceanprediction.org` are propriul ciclu, dar este sincronizată cu Drupal:

- Release Nuxt în aceeași fereastră cu Drupal când există schimbări de contract API.
- Versiune a iframe-ului hardcodată în Drupal printr-un setting → ușor de pinned/rollback independent.
