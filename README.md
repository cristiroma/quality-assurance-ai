# Quality Assurance – Documentație departament

Acest repository conține procesele, standardele, template-urile și planurile de testare folosite de departamentul QA pentru toate proiectele active (Drupal, WordPress, Nuxt etc.).

## Structură

```
.
├── README.md                       # Acest fișier (index general)
├── CLAUDE.md                       # Context pentru asistentul AI
│
├── processes/                      # Procese transversale (valabile pe toate proiectele)
│   ├── bug-lifecycle.md            # Severitate, prioritate, stări, SLA intern
│   ├── definition-of-ready-done.md # DoR / DoD pentru taskuri
│   ├── release-process.md          # Flow dev → staging → prod, QA gates
│   └── qa-gates.md                 # Criteriile QA pentru a aproba un release
│
├── standards/                      # Standardele tehnice ale departamentului
│   ├── test-pyramid.md             # Strategia pe straturi de testare
│   ├── tooling.md                  # Tool-urile aprobate (Playwright, axe, BackstopJS...)
│   └── metrics.md                  # KPI-uri QA și cum se măsoară
│
├── templates/                      # Template-uri reutilizabile
│   ├── bug-report-template.md
│   ├── test-case-template.md
│   ├── test-plan-template.md
│   └── release-checklist-template.md
│
├── training/                       # Planuri de creștere pentru membrii echipei
│   └── laura/
│       ├── growth-plan.md          # Plan 3–6 luni
│       └── learning-resources.md   # Cursuri, cărți, exerciții
│
├── people/                         # Profilurile membrilor echipei QA
│   └── laura.md
│
└── projects/                       # Documentație specifică pe proiect
    └── un-ocean-prediction/
        ├── README.md               # Overview proiect, contacte, stack
        ├── risk-assessment.md      # Zone critice, business impact
        ├── critical-user-journeys.md
        ├── 30-day-plan.md          # Plan QA primele 30 de zile
        ├── test-plans/
        │   └── smoke-test-plan.md
        └── checklists/
            └── release-regression-checklist.md
```

## Proiecte active

| Proiect | Stack | Start contract | Frecvență release | QA owner |
|---|---|---|---|---|
| [UN Ocean Prediction Atlas](projects/un-ocean-prediction/README.md) | Drupal 10 + Nuxt (iframe) | 2026-05-11 | Bi-weekly | Laura |

## Cum citești această documentație

- **Manageri / clienți**: începe cu `projects/<proiect>/README.md` și `30-day-plan.md`.
- **Developeri**: `processes/definition-of-ready-done.md` + `processes/release-process.md` + `standards/test-pyramid.md`.
- **QA (Laura)**: `training/laura/growth-plan.md` + `templates/` + `projects/<proiect>/checklists/`.
