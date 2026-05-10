# Bug lifecycle

Tracker oficial: **Redmine** – https://helpdesk.eaudeweb.ro/

## Stări (Redmine workflow)

```
New → Confirmed → In Progress → Resolved → Ready for QA → Closed
                                              ↓
                                          Reopened
```

- **New**: bug raportat, nu a fost încă triat.
- **Confirmed**: triat de tech lead / QA, reproductibil, are severitate/prioritate setate.
- **In Progress**: developer lucrează la el.
- **Resolved**: fix făcut, deployed pe staging.
- **Ready for QA**: Laura testează pe staging.
- **Closed**: verificat OK pe staging și inclus în release notes.
- **Reopened**: dacă Laura găsește că fix-ul nu este complet sau a introdus regresie.

## Severitate (impact tehnic)

| Severitate | Definiție | Exemple |
|---|---|---|
| **S1 – Critical** | Site down, data loss, security breach | 500 pe homepage, login spart, leak de date |
| **S2 – Major** | Funcționalitate principală blocată, fără workaround | Nu se pot adăuga modele oceanice, harta nu încarcă |
| **S3 – Minor** | Funcționalitate afectată parțial sau cu workaround | Filtru hartă nu salvează state, validare formular eronată |
| **S4 – Trivial** | Cosmetic, typo, UI minor | Aliniere greșită, traducere lipsă |

## Prioritate (urgență business)

`Immediate` / `Urgent` / `High` / `Normal` / `Low` – setată de PM împreună cu clientul.

> Severitatea ≠ prioritatea. Un typo pe homepage poate fi S4 dar prioritate Urgent.

## SLA intern (recomandat – nu există SLA contractual)

| Severitate | Triere | Fix target |
|---|---|---|
| S1 | < 2 ore | < 24h (hotfix branch) |
| S2 | < 1 zi lucrătoare | În următorul release bi-weekly |
| S3 | < 2 zile | În următoarele 1–2 release-uri |
| S4 | Best effort | Backlog |

## Câmpuri obligatorii la raportare

Vezi [bug report template](../templates/bug-report-template.md). Fără aceste câmpuri, bug-ul rămâne în `New` și nu este preluat în sprint:

1. Steps to reproduce (numerotate)
2. Expected result
3. Actual result
4. Environment (URL, browser, user role, dată/oră)
5. Screenshot / video / HAR file dacă e cazul
6. Severitate propusă

## Cine ce face

- **Reporter** (oricine, inclusiv client): completează template-ul.
- **Laura (QA)**: triază, încearcă reproducerea, setează severitatea, atașează informații suplimentare.
- **Tech lead**: confirmă, atribuie developer, validează fix-ul în code review.
- **Developer**: rezolvă, scrie test de regresie dacă bug-ul a scăpat dintr-o zonă acoperită, mută în `Resolved`.
- **Laura**: validează pe staging, închide sau reopen.
