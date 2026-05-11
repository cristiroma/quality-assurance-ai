# Critical User Journeys (CUJs) – UN Ocean Prediction

> **TODO**: Document de validat cu PM și utilizatori reali în săptămâna 1.
> 
> CUJ = un flow care, dacă nu funcționează, **utilizatorul nu poate atinge un obiectiv business** important.
> Nu confunda cu "feature" – un CUJ traversează multiple feature-uri.

## Anonymous (vizitator)

### CUJ-A1: Descoperă aplicația Atlas
1. Aterizează pe homepage `https://www.unoceanprediction.org/`
2. Navighează către "Atlas" (meniu principal)
3. Așteaptă încărcarea hărții (iframe Nuxt)
4. Vede markeri pe hartă cu persoane, organizații, modele și use-case oceanice
5. Click pe un marker → vede detaliile unei persoane, organizație, model sau use-case
6. **Goal**: Înțelege ce conține portalul.

**Priority**: 🔴 Critical. Aceasta este probabil cea mai vizitată pagină.

### CUJ-A2: Filtrează modele după criterii
1. Pe pagina Atlas
2. Deschide panoul de filtre
3. Selectează un tip de forecast (ex. "Wave height")
4. Apply
5. Vede markeri actualizați + count
6. **Goal**: Găsește modele relevante pentru research-ul lui.

**Priority**: 🔴 Critical.

### CUJ-A3: Citește un use case
1. Navighează la "Use cases"
2. Click pe un use case
3. Citește conținut + vede modele asociate
4. **Goal**: Învață cum sunt aplicate modelele.

**Priority**: 🔴 Critical.

### CUJ-A4: Înregistrare cont nou
1. Click "Register"
2. Completează formular (email, password, optional fields)
3. Confirmă email
4. Login
5. **Goal**: Devine contributor.

**Priority**: 🔴 Critical (fără asta nu există contributori noi).

## Authenticated user (contributor)

### CUJ-U1: Login
1. Click "Login"
2. Email + password → submit
3. Redirected pe profil sau homepage logged-in
4. **Goal**: Acces la funcționalități pentru autentificați.

**Priority**: 🔴 Critical.

### CUJ-U2: Adaugă organizația proprie pe hartă
1. Login
2. Profil → "My organization" (sau echivalent)
3. Add organization → completează nume, descriere, locație geografică (lat/lng), website
4. Submit
5. Verificare: organizația apare pe hartă.
6. **Goal**: Vizibilitate organizațională.

**Priority**: 🔴 Critical.

### CUJ-U3: Adaugă un forecast model
1. Login
2. Navighează la "Add forecast model"
3. Completează: nume, tip, regiune, descriere, organization owner, parameters, accuracy
4. Atașează poate fișiere/linkuri (de confirmat)
5. Submit / save draft
6. Verificare: modelul apare în lista proprie + pe hartă (după moderare?)
7. **Goal**: Contribuie cu date.

**Priority**: 🔴 Critical.

### CUJ-U4: Editează un model existent
1. Login
2. Lista propriilor modele
3. Edit
4. Modifică câmpuri
5. Save
6. Verificare: schimbările apar atât pe hartă, cât și în detail page.
7. **Goal**: Mentenanță a contribuției proprii.

**Priority**: 🟠 High.

### CUJ-U5: Adaugă un use case
1. Login
2. "Add use case"
3. Asociază 1+ modele
4. Save
5. **Goal**: Documentează aplicarea modelelor.

**Priority**: 🟠 High.

### CUJ-U6: Editează profilul propriu
1. Login → My profile → Edit
2. Schimbă nume, avatar, bio
3. Save
4. **Goal**: Branding personal.

**Priority**: 🟡 Medium.

### CUJ-U7: Logout
1. Click logout din meniu
2. Verificare: nu mai are acces la zone autentificate.
3. **Goal**: Securitate.

**Priority**: 🟠 High.

### CUJ-U8: Password reset
1. Pagina login → "Forgot password"
2. Introduce email
3. Primește email
4. Click link
5. Setează parolă nouă
6. Login cu noua parolă
7. **Goal**: Recuperare cont.

**Priority**: 🟠 High.

## Editor / Moderator (dacă există acest rol)

### CUJ-E1: Moderează contribuții noi
1. Login as editor
2. Vede listă modele/use cases în "pending"
3. Aprobă / respinge cu motiv
4. **Goal**: Calitate conținut.

**Priority**: 🟠 High (dacă rolul există).

> **TBD**: Confirmare rol și permisiuni cu PM.

## Admin

### CUJ-AD1: Gestionează utilizatori
1. Login as admin
2. Lista utilizatori → block / unblock / delete
3. **Goal**: Mentenanță platformă.

**Priority**: 🟡 Medium (rar folosit, dar critic când e necesar).

### CUJ-AD2: Configurări site (taxonomii, tipuri de modele)
1. Login as admin
2. Modifică o taxonomy term
3. Verificare: schimbarea se reflectă în formular
4. **Goal**: Evolution platformă.

**Priority**: 🟡 Medium.

---

## Prioritizare pentru automatizare (luna 1–3)

| Order | CUJ | Tipo | Săptămână țintă |
|---|---|---|---|
| 1 | CUJ-U1 (login) | Smoke E2E | Săpt 2 |
| 2 | CUJ-A1 (atlas + map load) | Smoke E2E | Săpt 2 |
| 3 | CUJ-U6 (edit profile) | Smoke E2E | Săpt 2 |
| 4 | CUJ-A2 (map filter) | E2E | Săpt 4 |
| 5 | CUJ-U3 (add forecast model) | E2E | Săpt 5 |
| 6 | CUJ-U2 (add organization) | E2E | Săpt 6 |
| 7 | CUJ-A4 (register) | E2E | Săpt 7 |
| 8 | CUJ-U8 (password reset) | E2E | Săpt 8 |
| 9 | CUJ-U4 (edit model) | E2E | Săpt 9 |
| 10 | CUJ-U5 (add use case) | E2E | Săpt 10 |
| 11+ | CUJ-E1, CUJ-AD1, CUJ-AD2 | E2E | Luna 3+ |
