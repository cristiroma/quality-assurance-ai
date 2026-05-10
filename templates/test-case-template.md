# Test case – template

Folosim formatul **Gherkin (Given/When/Then)** pentru toate test cases manuale și automate. Acesta este și formatul în care Laura va scrie cazurile înainte să le automatizeze în Playwright.

---

## TC-XXX: [Titlu scurt și descriptiv]

**ID**: TC-001  
**Feature / Module**: (ex. User profile, Map filters, Forecast model creation)  
**Priority**: High / Medium / Low  
**Type**: Smoke / Regression / Functional / E2E / Visual / Accessibility  
**Automated**: ☐ No  ☐ Yes (link la fișierul de test: `tests/e2e/...spec.ts`)  
**Last updated**: YYYY-MM-DD by [Name]  

### Preconditions
> Ce trebuie să fie adevărat înainte de start.
- 
- 

### Test data
> Date specifice (utilizator, organizație, model). Folosește fixtures, nu date reale.
| Field | Value |
|---|---|
| Username | qa.user@test.local |
| Password | (din vault) |

### Scenario
```gherkin
Given I am logged in as an authenticated user with role "Model contributor"
  And I am on the page "/en/atlas"
When I click on the filter "Forecast type"
  And I select "Wave height"
  And I click "Apply"
Then the map should display only models matching "Wave height"
  And the URL should contain "?forecast_type=wave_height"
  And the result count should be greater than 0
```

### Expected results
- 
- 

### Postconditions / cleanup
> Ce trebuie făcut după test (ex. ștergere model creat, logout).

### Notes
> Linkuri Redmine, dependențe, edge cases cunoscute.
