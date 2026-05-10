# Release regression checklist – UN Ocean Prediction

Folosit la fiecare release bi-weekly **până când** funcționalitatea respectivă e acoperită de teste automate stabile.

> Marchează cu ✅ pe staging înainte de sign-off. Atașează acest fișier completat ca comentariu în ticketul de release Redmine.

## Release: ____________ Date: ____________ QA: ____________

## A. Public pages (anonymous)

- [ ] Homepage `/` se încarcă fără erori în consolă
- [ ] Meniul principal este vizibil și toate linkurile funcționează (click + verificare URL destinație)
- [ ] Footer-ul este vizibil și toate linkurile funcționează
- [ ] Logo-ul UN Ocean Prediction este corect afișat
- [ ] Pagina `/en/atlas` se încarcă
- [ ] Iframe-ul `cartography.unoceanprediction.org` se încarcă în < 5s
- [ ] Harta afișează markeri (cel puțin un model)
- [ ] Click pe un marker deschide popup/detail
- [ ] Filtrul "Forecast type" funcționează
- [ ] Filtrul "Region" / area funcționează (dacă există)
- [ ] Reset filtre funcționează
- [ ] Pagina "About" se încarcă
- [ ] Pagina "Contact" se încarcă; formularul (dacă există) trimite mesaje
- [ ] Pagina "Use cases" listează use cases
- [ ] Click pe un use case afișează detaliile

## B. Authentication

- [ ] Pagina `/user/login` se încarcă
- [ ] Login cu credentiale corecte → redirect la pagina autentificată
- [ ] Login cu credentiale greșite afișează mesaj de eroare clar
- [ ] "Forgot password" link → pagina de reset
- [ ] Reset password trimite email
- [ ] Linkul din email setează parolă nouă cu success
- [ ] Login cu parola nouă funcționează
- [ ] Register: formular vizibil, validări funcționează
- [ ] Register: email de confirmare primit
- [ ] Activare cont via link → user activ
- [ ] Logout → utilizatorul nu mai poate accesa zone autentificate

## C. User profile

- [ ] `/user` afișează profilul propriu
- [ ] Edit profile: schimbarea numelui se salvează
- [ ] Edit profile: upload avatar funcționează
- [ ] Edit profile: schimbarea parolei funcționează
- [ ] Setări notificări (dacă există) se salvează

## D. Organizations

- [ ] Listă organizații se încarcă
- [ ] Click pe o organizație → detail page
- [ ] Add organization (logged in): formular se trimite cu success
- [ ] Organizația apare pe hartă după aprobare/imediat (de confirmat flow)
- [ ] Edit organizația proprie funcționează
- [ ] User normal NU poate edita organizația altui user (verificare URL direct)

## E. Forecast models

- [ ] Listă modele se încarcă (dacă există pagină dedicată)
- [ ] Detail model: toate câmpurile afișate (nume, tip, regiune, descriere, owner)
- [ ] Add forecast model: formular se trimite cu success
- [ ] Câmpuri obligatorii: validare funcționează (testează cu câmpuri goale)
- [ ] Upload fișiere (dacă există) funcționează
- [ ] Edit propriul model funcționează
- [ ] Delete propriul model funcționează (sau marchează ca inactiv)
- [ ] User normal NU poate edita modelul altui user

## F. Use cases

- [ ] Listă use cases se încarcă
- [ ] Add use case (logged in) funcționează
- [ ] Asociere use case ↔ model funcționează
- [ ] Edit propriul use case funcționează

## G. Admin (cu cont admin)

- [ ] `/admin` accesibil
- [ ] User management: listă utilizatori
- [ ] Block / unblock user funcționează
- [ ] Content moderation: listă pending items (dacă aplicabil)
- [ ] Aprobare conținut → conținutul devine public
- [ ] Drupal cron rulează fără erori (`/admin/reports/status` – Last run = recent)
- [ ] Status report `/admin/reports/status` – fără erori roșii noi
- [ ] Recent log `/admin/reports/dblog` – fără spike de erori după release

## H. Tehnic / non-funcțional

- [ ] Fără erori 500 în logs în orele de la deploy
- [ ] Fără erori în consolă browser pe paginile critice
- [ ] Performance: Lighthouse score Performance ≥ 80 pe `/` și `/en/atlas`
- [ ] Accessibility: niciun warning critical/serious nou în axe pe paginile critice
- [ ] Cross-browser: pagina atlas funcționează pe Chrome, Firefox, Safari
- [ ] Responsive: site utilizabil pe mobile (375px), tablet (768px), desktop (1440px)
- [ ] Imagini: nu sunt imagini lipsă (404)
- [ ] HTTPS: certificat valid, fără mixed content warnings
- [ ] Robots.txt + sitemap.xml accesibile

## I. Smoke automat

- [ ] Playwright smoke suite trecută 100% pe staging
- [ ] Playwright smoke suite trecută 100% pe prod (după deploy)

## J. Sign-off

- [ ] Toate bug-urile S1/S2 din scope rezolvate și verificate
- [ ] Bug-urile S3/S4 nerezolvate sunt mutate la următorul release cu acordul PM
- [ ] Release notes scrise și aprobate
- [ ] Comment final în Redmine: **"QA sign-off ✅ – Laura, YYYY-MM-DD HH:MM"**

---

## Bug-uri găsite în această sesiune

| ID Redmine | Severity | Status | Note |
|---|---|---|---|
| | | | |

## Timp total checklist
**Start**: __________ **End**: __________ **Total**: __________
