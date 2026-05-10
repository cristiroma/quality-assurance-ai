# Risk assessment – UN Ocean Prediction

> Document de tip "living". Se revizuiește lunar în QA sync și după fiecare incident pe prod.

## Matrice de risc

```
Impact ↑
  High  | Auth     | Map +    | Map      |
        | break    | filters  | rendering|
  ------+----------+----------+----------+
  Med   | I18n*    | Forms    | API      |
        |          | (model)  | (JSON:API)|
  ------+----------+----------+----------+
  Low   | Footer   | Static   | Search   |
        | links    | pages    |          |
        +----------+----------+----------+----→ Probability
          Low        Medium     High
```
*I18n e Low impact aici pentru că site-ul e doar EN.

## Zone de risc identificate (top → low)

### 🔴 1. Autentificare & sesiuni (HIGH impact / LOW prob)
- **Ce poate merge prost**: login spart, password reset broken, sesiunea pierde rolul.
- **Cum acoperim**: smoke test E2E pe login + logout + password reset link, rulat pe fiecare release.
- **Owner**: Laura.

### 🔴 2. Hartă (rendering + filtre) (HIGH impact / HIGH prob)
- **Ce poate merge prost**: harta nu se încarcă, filtrele nu se aplică, markeri lipsă, performance proastă.
- **Complexitate**: rendering Canvas/WebGL/SVG (de confirmat) într-un iframe Nuxt cross-origin.
- **Cum acoperim**:
  - Smoke E2E: încărcare hartă + 1 filtru aplicat + verificare cont rezultate
  - Visual regression pe stare default + 2 stări de filtru
  - Performance budget pe pagina `/en/atlas`
- **Owner**: Laura + tech lead pentru iframe sync.

### 🟠 3. Sincronizare versiuni Drupal ↔ Nuxt (MEDIUM impact / MEDIUM prob)
- **Ce poate merge prost**: deploy Drupal cu API contract changes fără deploy Nuxt corespunzător → atlas page broken.
- **Cum acoperim**:
  - Versiune iframe pinned în settings Drupal
  - Test cross-version pe staging înainte de release
  - Release notes obligatoriu indică dacă e nevoie de release Nuxt sincron
- **Owner**: Tech lead.

### 🟠 4. Formulare (creare/editare model & organization) (MEDIUM impact / MEDIUM prob)
- **Ce poate merge prost**: validare server-side broken, upload fișiere broken, draft autosave broken, permisiuni greșite.
- **Cum acoperim**:
  - E2E happy path pentru fiecare formular major
  - Test cu rol diferit (verifică că un user normal nu poate edita modelul altuia)
  - Test cu input invalid (assert: mesaj de eroare apare)
- **Owner**: Laura.

### 🟠 5. JSON:API endpoints (MEDIUM impact / HIGH prob în refactoring)
- **Ce poate merge prost**: schemă schimbată, autentificare token broken, CORS broken pentru Nuxt.
- **Cum acoperim**:
  - API tests în Playwright (`request` fixture)
  - Test smoke: endpoint listare modele + endpoint listare organizații
- **Owner**: Laura + dev.

### 🟡 6. Permissions & roluri (MEDIUM impact / LOW prob)
- **Ce poate merge prost**: escalare privilegii, user vede date altui user.
- **Cum acoperim**:
  - Test matrix rol × pagină pentru paginile sensibile
  - Anual: penetration test extern (recomandare, nu blocker)
- **Owner**: Laura + tech lead.

### 🟡 7. Performance (MEDIUM impact / MEDIUM prob)
- **Ce poate merge prost**: regresii de performance la încărcarea hărții cu multe modele.
- **Cum acoperim**: Lighthouse CI cu buget; investigare orice scădere > 5 puncte.

### 🟢 8. Conținut static (Low impact / Low prob)
- Pagini "About", "Contact", footer links – verificare prin smoke test linkuri broken.

## Matrice CUJ × strategie de testare

| Critical User Journey | Manual | E2E | Visual | A11y | Perf | Owner |
|---|---|---|---|---|---|---|
| Anonymous: home → atlas → filter map | ✓ release | ✓ | ✓ | ✓ | ✓ | Laura |
| Anonymous: signup new user | ✓ release | ✓ | – | ✓ | – | Laura |
| User: login | ✓ release | ✓ | – | ✓ | – | Laura |
| User: edit profile | ✓ release | ✓ | – | – | – | Laura |
| User: add organization | ✓ release | ✓ | – | – | – | Laura |
| User: add forecast model | ✓ release | ✓ | – | – | – | Laura |
| User: add use case | ✓ release | ✓ | – | – | – | Laura |
| Editor: moderate content | ✓ release | partial | – | – | – | Laura |
| Admin: user management | ✓ release | – | – | – | – | Laura |

## Issues istorice de monitorizat

> TODO discovery – completat după audit Redmine săpt 1.

| Bug recurent | Frecvență | Cauza root | Test acoperire? |
|---|---|---|---|
| | | | |
