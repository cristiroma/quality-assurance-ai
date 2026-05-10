# QA Gates

Punctele în care QA poate să **blocheze** progresul – pentru a proteja calitatea.

## Gate 1 – Pull Request

**Cine blochează**: pipeline CI + reviewer.

Criterii:
- [ ] PHPCS / ESLint clean
- [ ] PHPStan fără erori noi
- [ ] Build trece (composer install, Drupal config import dry-run)
- [ ] Smoke E2E rulează pe ephemeral environment (când e configurat) – minim verde

## Gate 2 – Merge în develop

**Cine blochează**: tech lead.

Criterii:
- [ ] Cel puțin 1 review aprobat
- [ ] Toate comentariile rezolvate
- [ ] DoD code-section bifat

## Gate 3 – Promote la staging

**Cine blochează**: GitHub Action + tech lead.

Criterii:
- [ ] Toate taskurile din `release/*` au status `Resolved`
- [ ] Pipeline verde end-to-end
- [ ] Update path testat (drush updb pe DB clonată din prod)

## Gate 4 – Promote la production (cel mai strict)

**Cine blochează**: Laura (QA sign-off).

Criterii: vezi [release-process.md § QA Gates](release-process.md#qa-gates-criterii-pentru-sign-off).

## Escalare

Dacă un gate este "forțat" (deploy fără sign-off din motive business):
1. Tech lead documentează decizia în release notes (`⚠ Deployed without full QA sign-off because...`).
2. Se creează ticket de follow-up pentru testare retrospectivă pe prod.
3. Se discută în retro.
