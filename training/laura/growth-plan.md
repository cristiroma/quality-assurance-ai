# Plan de creștere Laura – 6 luni

Premisă: Laura are 16h/săptămână alocate proiectului UN Ocean Prediction. Din acestea:
- **70% (11h)** = activitate QA pe proiect (testare manuală + scriere de teste)
- **30% (5h)** = învățare structurată + pair sessions

Pe măsură ce skill-urile cresc, raportul se inversează (luna 4+: 90% execuție, 10% învățare continuă).

---

## Luna 1 (mai – iunie 2026): fundamente + manual structurat

### Obiective
- Cunoaște aplicația în profunzime.
- Documentează test cases în format Gherkin.
- Înțelege HTML / CSS selectors / DevTools la nivel de bază.
- Scrie primele 3–5 smoke tests cu **Playwright Codegen** (fără cod scris manual).

### Săptămâni
| Săpt | Focus | Deliverable |
|---|---|---|
| S1 | Onboarding tehnic + acces medii. Lectură `processes/` și `standards/`. Tour cu tech lead pe codebase. | Notițe + întrebări documentate |
| S2 | Mapare critical user journeys (împreună cu PM). Documentare în `projects/un-ocean-prediction/critical-user-journeys.md`. | Listă 10–15 CUJs |
| S3 | Scriere primelor 5 test cases în format Gherkin (template-ul `templates/test-case-template.md`). DevTools workshop (1h cu dev). | 5 TCs + checklist regression v1 |
| S4 | Instalare Playwright local. Tutorial codegen. Înregistrare 3 smoke tests pentru: home, login, listing modele. | 3 fișiere `*.spec.ts` în repo |

### Deliverables luna 1
- ✅ Document `critical-user-journeys.md` complet
- ✅ 10+ test cases în Gherkin
- ✅ 3+ smoke tests Playwright generate cu codegen
- ✅ Regression checklist v1

### Învățare (5h/săpt)
- **Curs gratuit**: [Playwright official tutorial](https://playwright.dev/docs/intro) – 4h
- **Web fundamentals**: [MDN HTML Basics](https://developer.mozilla.org/en-US/docs/Learn/HTML) – 6h
- **CSS selectors**: [CSS Diner](https://flukeout.github.io/) – 2h (fun, în loc de coffee break)

---

## Luna 2: primele teste scrise manual

### Obiective
- De la codegen la cod scris manual.
- Înțelegere fundamentală a JavaScript / TypeScript (variabile, funcții, async/await).
- Acoperire 5+ CUJs critice în Playwright.

### Activități
- **Pair coding** 2h/săpt cu un dev pentru a re-scrie testele din codegen în cod curat.
- Învață `expect`, locator best practices (`getByRole`, `getByLabel` vs CSS selectors).
- Introducere `beforeEach` / `afterEach`.
- Înțelegere `playwright.config.ts`.

### Deliverable
- 10–15 teste E2E pentru CUJs critice (login, profil, creare model, filtru hartă, navigare iframe Nuxt).
- Toate rulează stabile pe local + în GitHub Actions (manual trigger pentru moment).

### Învățare (5h/săpt)
- **JavaScript essentials**: [JavaScript.info – primele 4 capitole](https://javascript.info/) – 10h
- **Async/await pentru începători**: video curs scurt – 2h
- **Carte recomandată**: *"Agile Testing"* – Lisa Crispin & Janet Gregory (lectură 30 min/zi).

---

## Luna 3: Page Object Model & fixtures

### Obiective
- Refactor: muta logica de localizare a elementelor în Page Objects.
- Fixtures custom pentru: user logat, organizație creată, model creat (via API, nu prin UI – mai rapid).
- Coverage > 50% din CUJs.

### Activități
- Workshop intern: "Why Page Object Model?" (1h, prezentat de tech lead, ascultat de Laura).
- Refactor primele 5 teste în POM.
- Construiește un `apiClient` fixture pentru a crea date prin JSON:API Drupal (skip UI overhead).
- Scrie primul test care verifică un bug găsit anterior pe prod (regression test).

### Deliverable
- Folder `tests/e2e/pages/` cu 5+ page objects.
- Folder `tests/e2e/fixtures/` cu user, org, model fixtures.
- 20+ teste E2E stabile.

### Învățare
- TypeScript intermediar: type aliases, interfaces.
- **Carte**: *"xUnit Test Patterns"* – Gerard Meszaros (capitole despre Test Doubles, Test Setup).

---

## Luna 4: integrare CI + visual regression

### Obiective
- Testele rulează automat pe fiecare PR.
- Smoke suite < 5 min, full suite < 30 min.
- Primele 10 teste de visual regression.

### Activități
- Configurare GitHub Actions workflow pentru Playwright (cu tech lead).
- Self-hosted runner: instalare Playwright dependencies.
- Sharding pentru paralelizare (`--shard 1/4` etc.).
- Visual snapshots pe homepage, profil, hartă (master baseline).
- Process pentru aprobare / respingere snapshot diffs.

### Deliverable
- Pipeline-uri `.github/workflows/qa-*.yml` în repo.
- HTML report publicat pe GitHub Pages branch.
- 10 visual snapshots aprobate ca baseline.

---

## Luna 5: accessibility + performance

### Obiective
- WCAG 2.1 AA scan automat pe paginile critice.
- Lighthouse CI integrat în pipeline.
- Coverage > 80% CUJs.

### Activități
- Integrare `@axe-core/playwright`.
- Scan inițial → listă violări → triere cu PM (care se rezolvă, care se ignoră cu justificare).
- Configurare Lighthouse CI cu buget aprobat.
- Cross-browser job în CI (Chromium + Firefox + WebKit).

### Deliverable
- Raport accessibility per pagină.
- Lighthouse trend dashboard.
- Documentat: cum se rulează local, cum se interpretează rezultate.

---

## Luna 6: maturitate + mentorat

### Obiective
- Coverage ≥ 90% CUJs.
- Suite stabilă (< 2% flaky rate).
- Laura poate face onboarding pentru un junior QA.
- Începe să identifice singură zone slab acoperite.

### Activități
- Audit propriu al suite-ului: care teste sunt cele mai valoroase, care sunt redundante.
- Documentație "How to write a Playwright test" (intern, scrisă de Laura) → consolidează cunoașterea prin scriere.
- Participare la code review pe PR-uri de teste.
- Posibil: prezentare 30 min în company "Lessons learned from automating UN Ocean Prediction".

---

## Indicatori de succes

| KPI | Luna 1 | Luna 3 | Luna 6 |
|---|---|---|---|
| Teste E2E scrise | 3 | 20 | 50+ |
| CUJs acoperite | 20% | 60% | 90% |
| Flaky rate | n/a | < 5% | < 2% |
| Teste scrise complet manual (fără codegen) | 0% | 70% | 100% |
| Autonomie pe debugging | low | medium | high |

## Risk-uri în plan

| Risk | Mitigare |
|---|---|
| Lipsa timpului pentru learning din cauza release-urilor | Block calendar 5h/săpt, ne-negociabil |
| Frustrare cu programarea | Pair sessions săptămânale, început cu codegen, victorii mici |
| Teste devin flaky și abandonate | Code review obligatoriu pe PR de teste, "fix or delete" rule |
| Buget redus de la client | Prioritizare strictă pe CUJs cu impact business mare |
