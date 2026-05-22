# Saucedemo Web App — Manual QA Test Suite

**Type:** Manual Testing — UX/UI, Functional & Compatibility | Test Case Design, Execution & Bug Reporting  
**Environment:** Chrome 148.0.7778.98 / Windows 10 / 1920×1080  
**Tester:** Alejandro Gutiérrez  
**Test Period:** May 14–21, 2026

---

## What is this?

Saucedemo (https://www.saucedemo.com/) is a mock e-commerce web application built by Sauce Labs as a testing sandbox. It simulates a complete online shopping flow — from login, through product browsing and cart management, all the way to checkout and order completion — with a fixed set of products and a fixed set of user accounts, each designed to exhibit different behaviors.

This entry documents the full design and execution of a manual QA test suite covering the UX/UI and functional aspects of the application across all available user types and multiple platforms.

![UI Testing](https://img.shields.io/badge/UI_Testing-Manual-4CAF50?style=flat-square)
![UX Testing](https://img.shields.io/badge/UX_Testing-Validated-2196F3?style=flat-square)
![Functional Testing](https://img.shields.io/badge/Functional_Testing-Test_Suite-FF9800?style=flat-square)
![Compatibility Testing](https://img.shields.io/badge/Compatibility_Testing-Cross--Platform-9C27B0?style=flat-square)

---


## Objective

The goal of this test suite was to evaluate the robustness of the Saucedemo web application by designing and executing a comprehensive test suite covering both UX/UI and functional aspects of the app.

UX/UI testing was included deliberately — while it carries lower priority than functional testing, a well-designed and visually consistent interface is key for building user trust. A glitchy or broken page can deter customers from completing a purchase or from ever returning to the service.

Functional testing went beyond the happy path. Negative and edge case scenarios were included to push the app toward unexpected behaviors, since real users don't always follow the expected flow — they can be unpredictable, and the app needs to handle that gracefully.

---


## Product / Functionality — What Did I Test?

The test suite covered the complete end-to-end flow of the application:

- **Login page** — valid/invalid credentials, empty fields, locked out behavior
- **Products page** — layout, sorting, product cards, cart interaction
- **Product Info page** — navigation, content accuracy, add to cart
- **Cart page** — product display, quantities, remove functionality, navigation
- **Checkout — Your Information** — form validation, field behavior
- **Checkout — Overview** — order summary, pricing logic, totals
- **Order Complete page** — confirmation display, navigation back to products
- **Cross-cutting concerns** — hamburger menu, footer links, scroll behavior, session persistence

Tests were executed across **6 user types** provided by the application:

| User | Purpose |
|---|---|
| `standard_user` | Baseline happy path user |
| `locked_out_user` | Validates lockout behavior |
| `problem_user` | Exposes functional and data integrity bugs |
| `performance_glitch_user` | Exposes performance issues |
| `error_user` | Exposes backend/API error handling |
| `visual_user` | Exposes UI/visual rendering bugs |

Compatibility testing was also performed for `standard_user` across three platform/browser combinations:

| Platform | Browser | Resolution |
|---|---|---|
| Desktop — Windows 10 | Chrome (covered in standard_user) | 1920×1080 |
| Desktop — Windows 10 | Edge | 1920×1080 |
| Mobile — iOS (DevTools emulation) | Safari | 414×896 |
| Mobile — Android | Chrome | 934×1373 |

> **Note on the compatibility matrix:** The ideal matrix would include native iOS Safari and Android Chrome testing. Since I don't own an Apple device, iOS Safari was emulated via Chrome DevTools device simulation. This is a known limitation of this test cycle.

---

## Tools Used
![Chrome](https://img.shields.io/badge/Chrome-Testing-4285F4?style=flat-square)
![Edge](https://img.shields.io/badge/Edge-Testing-0078D7?style=flat-square)
![Chrome DevTools](https://img.shields.io/badge/Chrome_DevTools-Debugging-FBBC05?style=flat-square)
![Android Chrome](https://img.shields.io/badge/Android_Chrome-Mobile_Testing-34A853?style=flat-square)

---

## Testing Methodologies
![Manual Testing](https://img.shields.io/badge/Manual_Testing-2C3E50?style=flat-square)
![Equivalence Partitioning](https://img.shields.io/badge/Equivalence_Partitioning-8E44AD?style=flat-square)
![Negative Testing](https://img.shields.io/badge/Negative_Testing-D35400?style=flat-square)
![Edge Testing](https://img.shields.io/badge/Edge_Testing-16A085?style=flat-square)
![Compatibility Matrix](https://img.shields.io/badge/Compatibility_Matrix-0E7490?style=flat-square)
![Exploratory Testing](https://img.shields.io/badge/Exploratory_Testing-7C3AED?style=flat-square)

---

## Scope

**In scope:**
- Full UX/UI validation of all pages in the purchase flow
- Functional testing of the complete checkout flow (happy path, negative, edge, and logic cases)
- All 6 user types provided by the application
- Compatibility testing across Desktop (Chrome/Edge), Mobile Android (Chrome), and Mobile iOS (Safari via DevTools emulation) for `standard_user`

**Out of scope:**
- Edge was excluded from per-user execution since it was already covered during `standard_user` compatibility testing — running it again across all users would have been redundant without adding meaningful coverage
- Compatibility testing was limited to the UX/UI suite, since functional behavior had already been validated across users in Chrome
- Performance benchmarking beyond subjective observation (no automated tooling was used)
- API/backend testing beyond what was observable through Chrome DevTools (Network tab, DOM inspection)
- Equivalence partitioning for authentication scenarios was limited due to the application's predefined test accounts and lack of field-level validation constraints. As a result, test classes were primarily divided into:
  - Registered users
  - Non-registered/invalid users

- Shipping form equivalence classes were also limited by the absence of input restrictions or validation rules. Testing therefore focused on:
  - Empty field scenarios
  - Fields containing generic character input

---

## Test Suite Reusability

![Smoke_Testing](https://img.shields.io/badge/Smoke_Testing-22C55E?style=flat-square)
![Sanity_Testing](https://img.shields.io/badge/Sanity_Testing-3B82F6?style=flat-square)
![Regression_Testing](https://img.shields.io/badge/Regression_Testing-8B5CF6?style=flat-square)

The priority system applied across this test suite (High / Medium / Low) was designed with reusability in mind. Depending on the testing scenario, the same suite can be used in different ways:

- **Smoke Testing** — Execute High-priority cases only. Covers the core purchase flow (login → products → cart → checkout → order completion) and validates that the app is functional after a deployment.

- **Sanity Testing** — Execute High and Medium-priority cases within the affected area. If only the checkout flow changed, run the checkout-related cases without executing the full suite.

- **Regression Testing** — Execute the full suite across all users. Validates that no previously working functionality was broken by recent changes.

No redesign is needed — the priority assignments already in place make this suite ready for any of these scenarios.
<p align="center">
  <img width="800" alt="Compatibility Matrix" src="https://github.com/user-attachments/assets/5c219305-a3a1-4f39-abee-24703e1966c6" />
  <br/>
  <em>UX/UI Tests</em>
</p>

<p align="center">
  <img width="800" alt="Bug Report" src="https://github.com/user-attachments/assets/588f68d5-719e-4dc8-9514-ef53523116c5" />
  <br/>
  <em>Functional Tests</em>
</p>

---

## Artifacts in This Folder

```text
SauceDemo_manual_testing_suite/
├── Test Suite SauceDemo.com (Manual).xlsx
└── README.md
```
```text
Workbook Structure
├── UX Tests
├── Functional Tests
├── Compatibility Matrix
├── Results - standard_user
├── Results - locked_out_user
├── Results - problem_user
├── Results - performance_glitch_user
├── Results - error_user
├── Results - visual_user
├── Compatibility Results
└── Bug Report
```

- `Test Suite SauceDemo.com (Manual).xlsx` — Complete manual QA test suite including UI, UX, functional, compatibility, user-based testing, compatibility matrix, and bug reports organized by document sheet.
- `UX Tests` — Complete UX/UI test case suite (SL-001 to SL-060, SL-116)
- `Functional Tests` — Complete functional test case suite (SL-061 to SL-115)
- `Compatibility Matrix` — Ideal vs. actual test environments based on statistics
- `Results - standard_user` — Test results for `standard_user`
- `Results - locked_out_user` — Test results for `locked_out_user`
- `Results - problem_user` — Test results for `problem_user`
- `Results - performance_glitch_user` — Test results for `performance_glitch_user`
- `Results - error_user` — Test results for `error_user`
- `Results - visual_user` — Test results for `visual_user`
- `Compatibility Results` — Cross-platform execution results for `standard_user`
- `bug-report` — Complete bug report (BUGSL-001 to BUGSL-032)
- All execution evidence, screenshots, recordings, and supporting material are referenced directly within the workbook through Google Drive and Loom links.

---

## Key Decisions — What Did I Prioritize and Why?

**Priority assignment** followed a simple principle: the closer a test case is to the core purchase flow, the higher its impact on the user and the business, and therefore the higher its priority. A broken checkout is far more damaging than a misaligned footer icon. This logic applied to both UX/UI and functional cases.

**Test execution order** followed priority — High cases first, then Medium, then Low. In this test cycle there was enough time to execute everything, but under time constraints, the High-priority functional cases covering the core flow (login → cart → checkout → order completion) would have been executed first.

**Scope decisions** were made to avoid redundant coverage. Running all 6 users across all 3 platforms would have produced diminishing returns — the functional differences between users were already captured in the per-user Chrome execution, and the visual differences between platforms were already captured by the `standard_user` compatibility run.

**Omitted cases** in `problem_user` were a deliberate call. When product entries were confirmed to be mismatched (BUGSL-009), attempting to follow test cases that depended on specific product-to-entry accuracy would have produced misleading results. Omitting them and documenting the reason was more honest and useful than forcing an execution with broken preconditions.

---
## Results

### Test Execution Overview

![Users_Tested](https://img.shields.io/badge/Users_Tested-6-2563EB?style=flat-square)
![Test_Cases](https://img.shields.io/badge/Test_Cases-116-059669?style=flat-square)

### Summary by User

| User | Total | Pass | Partial Pass | Fail | Blocked | Omitted |
|---|---|---|---|---|---|---|
| `standard_user` | 116 | 110 | ~6 | 6 | 0 | 0 |
| `locked_out_user` | 106 | 1 | 0 | 0 | 105 | 0 |
| `problem_user` | 106 | 63 | Variable | 10 | 31 | 2 |
| `performance_glitch_user` | 106 | 100 | Variable | 6 | 0 | 0 |
| `error_user` | 106 | 67 | Variable | 10 | 29 | 0 |
| `visual_user` | 106 | 82 | Variable | 24 | 0 | 0 |

> Partial passes were documented contextually within execution notes when behavior deviated from expected results without fully blocking task completion.

---

### Environment Compatibility Matrix

| Environment | Status | Notes |
|---|---|---|
| Chrome (Windows) | Pass | Primary execution environment |
| Edge (Windows) | Pass | Compatibility validation completed |
| Chrome (Android) | Pass | Mobile UI/UX compatibility validated |
| Safari(iOS with DevTools) | Pass | Mobile UI/UX compatibility validated |
<p align="center">
  <img width="800" alt="Compatibility Matrix" src="https://github.com/user-attachments/assets/19a03a80-52e7-4197-abbd-2ceeb1b19cfb" />
  <br/>
  <em>Compatibility Matrix — Ideal vs. actual test environment</em>
</p>


---

### Bugs Found: 32 (BUGSL-001 to BUGSL-032)

![Bugs_Found](https://img.shields.io/badge/Bugs_Found-32-DC2626?style=flat-square)
![Critical](https://img.shields.io/badge/Critical-2-991B1B?style=flat-square)
![High](https://img.shields.io/badge/High-13-EA580C?style=flat-square)
![Medium](https://img.shields.io/badge/Medium-8-D97706?style=flat-square)
![Low](https://img.shields.io/badge/Low-9-65A30D?style=flat-square)

| Severity | Count |
|---|---|
| Critical | 2 |
| High | 13 |
| Medium | 8 |
| Low | 9 |

<p align="center">
  <img width="800" alt="Bug Report" src="https://github.com/user-attachments/assets/ba0d299b-2480-4e79-9f4b-16beeededeaa" />
  <br/>
  <em>Bug Report sample</em>
</p>

---

### Key Findings

**`standard_user`** — The app is in solid baseline shape for a standard user. Most of the flow works correctly. The main issues found were minor navigation inconsistencies (BUGSL-004: "Back to products" from the Cart returning to the Products page instead), a business logic failure allowing empty orders to be placed (BUGSL-007), a cross-user cart privacy violation (BUGSL-005), and minor content issues with code-language text in two product entries (BUGSL-002).

**`locked_out_user`** — Behaves exactly as expected. Login is correctly blocked with the appropriate error message. All downstream tests are blocked as a direct consequence, which is the correct outcome.

**`problem_user`** — The most broken user profile. A critical bug (BUGSL-011/012) makes the "Last Name" field in the checkout form completely non-functional — input is redirected to the "First Name" field and only the last character is retained — which blocks the entire checkout flow. Additionally, all product images are replaced with a dog photo (BUGSL-008), product info pages display mismatched entries (BUGSL-009), one product leads to a completely glitched entry that crashes the cart when added (BUGSL-017), the "Remove" button is non-functional (BUGSL-015), and several products cannot be added to the cart at all (BUGSL-016).
<p align="center">
  <img width="800" alt="BUGSL-008 — Dog image replacing all product images" src="https://github.com/user-attachments/assets/b582fb3b-7cc2-4819-a8a0-0763afc26eb2" />
  <br/>
  <em>BUGSL-008 — Every product image is replaced with a dog photo (problem_user)</em>
</p>

**`performance_glitch_user`** — Functionally similar to `standard_user` with one major exception: the Products page and all actions that reference it suffer from a severe performance degradation (5+ seconds load time, BUGSL-018). Investigation via DevTools pointed to an active service worker introducing an artificial delay. An additional navigation bug was found where the "Cancel" button on the checkout form redirects to the Products page instead of the Cart (BUGSL-019).

**`error_user`** — The sort-by dropdown triggers a 503 backend error on every interaction (BUGSL-020), making sorting completely unavailable. The "Last Name" field is also broken (BUGSL-021), though the root cause here is a three-layer failure: a UI input freeze, a backend 503 error, and a frontend TypeError in the console. Several "Add to Cart" and "Remove" buttons are also unresponsive due to backend errors (BUGSL-022).

**`visual_user`** — Functionally the app works, but it is riddled with visual inconsistencies. The hamburger menu and cart icon are rotated and misplaced across all pages (BUGSL-023/024). The most impactful issue is on the Products page, where prices cycle through incorrect values depending on the active sorting option (BUGSL-026/027), and the first product entry always displays a dog image regardless of sorting (BUGSL-025). Buttons on the Cart page are also misplaced (BUGSL-029/030).
<p align="center">
  <img width="800" alt="BUGSL-026 — Incorrect prices displayed in visual_user" src="https://github.com/user-attachments/assets/15471cb6-db9c-45c6-83f2-d22cade697c6" />
  <br/>
  <em>BUGSL-026 — Prices cycle through incorrect values depending on the active sorting option (visual_user)</em>
</p>

**Compatibility** — The app is generally consistent across Desktop Chrome, Android Chrome, and iOS Safari (emulated). One issue was found: product images appear slightly stretched and a large white gap appears between description and price on mobile (BUGSL-032).

---

## What Would I Improve Next Time?

**Documentation consistency** — Variable naming and bug ID conventions were not always consistent throughout the test cycle. Standardizing naming from the start (field names, page names, user references) would make the documentation cleaner and easier to cross-reference.

**Deeper DevTools usage** — I used the Network tab and DOM inspector throughout this cycle and learned a lot from them. Going forward I'd like to deepen my understanding of the DOM tree and how to better read and interpret console errors, particularly for distinguishing frontend from backend root causes more confidently.

**Coverage vs. prioritization balance** — There are always more niche edge cases that could be added, but adding them indefinitely defeats the purpose of prioritization. Next time I would be even more deliberate about defining scope boundaries before writing test cases, rather than adjusting mid-cycle.
