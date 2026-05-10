# QA Metrics – KPI și cum se măsoară

Metricile sunt instrumente de îmbunătățire, **nu de pedeapsă**. Toate sunt review-uite lunar în QA sync.

## Metrici principale (raportate lunar)

### 1. Escape rate
**Definiție**: bugs găsite în prod / (bugs găsite în prod + bugs găsite pe staging) × 100

**Țintă**: < 15% (industry good); < 10% (excellent)

**Sursă date**: Redmine – câmp custom `Found on environment` (Production / Staging / Dev).

### 2. Mean Time To Detect (MTTD) – pentru bugs din prod
**Definiție**: timpul mediu de la deploy la raportarea bug-ului.

**Țintă**: < 48h (sugerează că monitoring + smoke prod funcționează).

### 3. Mean Time To Resolve (MTTR)
**Definiție**: timpul mediu de la `Confirmed` la `Closed`, pe severitate.

**Țintă**: 
- S1: < 24h
- S2: < 1 release cycle (2 săpt)
- S3: < 2 release cycles

### 4. Regression rate
**Definiție**: bugs care reactivează funcționalitate care anterior funcționa / total bugs.

**Țintă**: < 10%. Peste 10% = avem nevoie de mai mult coverage automat.

### 5. Test automation coverage (E2E)
**Definiție**: număr de critical user journeys acoperite de teste Playwright / total CUJs identificate.

**Țintă pentru UN Ocean Prediction**:
- Luna 1: ≥ 30%
- Luna 3: ≥ 70%
- Luna 6: ≥ 90%

### 6. Build / pipeline health
- **CI green rate**: % de pipeline-uri care trec din prima.
- **Flaky test rate**: % de teste care eșuează random pe re-run. **Țintă < 2%**. Test flaky = test broken.

### 7. Release sănătate
- **Hotfix rate**: % din release-uri care necesită hotfix în 48h.
- **Țintă**: < 15%.

## Metrici secundare (nice to have)

- Lighthouse scores trend (Performance, A11y, Best Practices, SEO).
- Numărul de violări `axe` per pagină critică (trend descrescător).
- Acoperire cod PHPUnit (informativ; nu setăm țintă strictă).

## Anti-metrici (NU le folosim)

- ❌ Numărul de bugs raportat de Laura (incentiv pentru raportare excesivă/falsă).
- ❌ Numărul de teste scrise (incentiv pentru teste tautologice).
- ❌ Coverage % ca țintă strictă (incentiv pentru teste fără valoare).

## Dashboard

Pas următor (luna 2): un dashboard simplu (Redmine custom queries + Google Sheet sau Grafana) cu cele 7 metrici principale, refresh săptămânal.
