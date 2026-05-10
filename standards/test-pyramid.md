# Test pyramid – strategia pe straturi

```
              ╱╲
             ╱E2╲              ← puține, lente, scumpe, dar realistice
            ╱ E  ╲                Playwright (Laura)
           ╱──────╲
          ╱ Visual ╲           ← snapshots pe pagini-cheie
         ╱  Regr.   ╲             BackstopJS / Playwright snapshots
        ╱────────────╲
       ╱  Functional   ╲       ← flow-uri în Drupal cu DB reală
      ╱  / Kernel       ╲         PHPUnit Drupal (devs, asistat AI)
     ╱────────────────────╲
    ╱     Unit tests        ╲  ← multe, rapide, izolate
   ╱   PHPUnit (PHP), Vitest ╲    Devs (asistat AI)
  ╱   (Nuxt)                  ╲
 ╱──────────────────────────────╲
╱   Static analysis & linters    ╲ ← gratis, ruleaza in fiecare commit
────────────────────────────────────  PHPStan, PHPCS, ESLint
```

## Principiu

> **Cu cât testul e mai sus, cu atât e mai scump și mai fragil. Investește mult în baza piramidei și păstrează vârful focusat doar pe user journeys critice.**

## Pe proiectul UN Ocean Prediction (focus pe testare web)

Conform deciziei de a ne concentra pe testare web, nu pe unit/functional, distribuția-țintă este:

| Strat | Cine | % din efortul total QA |
|---|---|---|
| Static analysis (linters, PHPStan) | Devs (în CI, automat) | 5% |
| Unit / Functional PHPUnit | Devs **asistați de AI** (Copilot, Claude) | 15% |
| **E2E Playwright** | **Laura** | **50%** |
| Visual regression | Laura | 15% |
| Accessibility (axe în Playwright) | Laura | 10% |
| Performance (Lighthouse CI) | Automat în CI | 5% |

## Reguli de aur

1. **Fiecare bug găsit pe prod → cel puțin 1 test automat care îl prinde** înainte să fie închis.
2. **Smoke suite (Playwright) trebuie să ruleze < 5 min** – altfel nimeni nu o așteaptă.
3. **Full regression suite < 30 min** – pentru a putea rula la fiecare PR pe release branch.
4. **Testele E2E sunt independente** – fiecare își face setup-ul propriu (user creation via API, fixtures), nu se bazează pe ordine de execuție.
5. **Niciodată nu hardcoda așteptări de timp** (`waitForTimeout(5000)`); folosește auto-waiting Playwright (`waitFor`, `expect.toBeVisible`).
6. **Page Object Model** pentru orice test ne-trivial – mentenanța e mai ieftină.

## Asistență AI pentru teste unitare/funcționale

Pentru a salva timp și buget pe straturile de jos:
- Developerul cere AI să genereze schelet de PHPUnit pe baza codului scris.
- Developer-ul **revizuiește și ajustează** – AI generează câteodată teste tautologice sau cu mock-uri excesive.
- Acceptăm doar teste care: (a) ar pica dacă logica se rupe, (b) sunt deterministe, (c) rulează < 1s.
