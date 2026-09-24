# BookNow App - Sprint Test Plan

**Sprint:** Sprint 1
**Sprint Duration:** 2 weeks
**Application:** BookNow (Single-page booking flow)
**Screens:** Login → Rooms → Booking → Confirmation
**Document Version:** 1.0
**Last Updated:** 2026-09-24

---

## Sprint Scope & Objectives

### User Stories Targeted for This Sprint

| Story ID | User Story | Acceptance Criteria |
|----------|-------------|---------------------|
| US-001 | As a user, I want to log in with email and password so that I can access the booking system | Valid credentials grant access; invalid credentials show error; session maintained; logout available |
| US-002 | As a user, I want to browse available rooms with pricing so that I can select a room to book | Rooms display with images, descriptions, prices, discounts, and availability; correct price calculations |
| US-003 | As a user, I want to book a room by providing guest and stay details so that I can complete a reservation | Form validates all inputs; price calculates correctly; booking creates confirmation |
| US-004 | As a user, I want to see a booking confirmation with reference number so that I have proof of reservation | Confirmation shows all booking details and unique reference; form resets for next booking |

### Defect Fixes Targeted for This Sprint

| Defect ID | Component | Description | Priority |
|-----------|-----------|-------------|----------|
| DEF-001 to DEF-007 | Login | Wrong credentials navigation, error display, password masking, session state, navbar visibility, credential exposure | High |
| DEF-008 to DEF-012 | Rooms | Discount calculation, badge styling, broken images, alt text, text overflow | High |
| DEF-013 to DEF-019 | Booking | Total calculation, nights calculation, form validation, input types, date constraints, guests validation, label attributes | High |
| DEF-020 to DEF-025 | Confirmation/General | Confirmation details, form reset, toast messages, nav links, page title, back button handling | High |

### Sprint Testing Objectives

1. **Primary Objective:** Verify all 25 identified defects are fixed and the core booking flow (Login → Rooms → Booking → Confirmation) works end-to-end
2. **Secondary Objective:** Validate form field validations per the requirements document
3. **Tertiary Objective:** Ensure basic accessibility and responsive design standards are met

---

## In-Scope vs. Out-of-Scope

### In-Scope (This Sprint)

**Functional Testing:**
- Core user flow: Login → Rooms → Booking → Confirmation
- All 25 defect fixes verification
- Form validation for all required fields
- Price calculation accuracy
- Session management (login/logout)
- Route protection

**Non-Functional Testing:**
- Basic accessibility (keyboard navigation, ARIA labels, alt text)
- Responsive layout on mobile devices
- Cross-browser compatibility (Chrome, Firefox, Safari, Edge)
- Basic security checks (input sanitization, credential exposure)

**Test Types:**
- Functional testing (manual)
- Defect verification (manual)
- UI/UX testing (manual)
- Cross-browser testing (manual)
- Basic accessibility testing (manual)

### Out-of-Scope (Deferred to Future Sprints)

**Features:**
- Password show/hide toggle
- Forgot password functionality
- Filter/sort rooms by price or type
- Enter key form submission
- Advanced accessibility audit (WCAG full compliance)
- Automated test suite development
- API testing (if backend is added)
- Performance testing
- Security penetration testing

**Test Types:**
- Automation scripting
- Load/performance testing
- Comprehensive security testing
- Exploratory testing beyond happy paths

---

## Test Approach & Types

### Test Types for This Sprint

| Test Type | Description | Coverage Target | Automation Strategy |
|-----------|-------------|-----------------|---------------------|
| Functional Testing | Verify core user stories and defect fixes | 100% of in-scope user stories | Manual |
| Defect Verification | Re-test all 25 identified defects | 100% of defects | Manual |
| Form Validation Testing | Validate all field validation rules | 100% of validation rules | Manual |
| UI/UX Testing | Visual consistency, responsive design | 100% of screens | Manual |
| Cross-Browser Testing | Chrome, Firefox, Safari, Edge | 4 browsers desktop + 2 mobile | Manual |
| Accessibility Testing | Basic keyboard nav, ARIA, alt text | Critical accessibility features | Manual |

### Test Approach

**Sequential Testing Phases:**
1. **Smoke Testing (Day 1):** Verify the application launches and core flow is accessible
2. **Defect Verification (Days 1-2):** Systematically verify each of the 25 defects
3. **Functional Testing (Days 2-3):** Execute end-to-end user story tests
4. **Form Validation Testing (Day 3):** Comprehensive validation rule testing
5. **Cross-Browser & UI Testing (Day 4):** Browser compatibility and responsive design
6. **Regression Testing (Day 5):** Re-test critical areas after bug fixes

**Test Execution Strategy:**
- **Manual Testing:** All testing in this sprint will be manual
- **Exploratory Testing:** Limited to happy paths and edge cases identified in test review
- **Defect Triage:** Daily triage meetings to prioritize fixes
- **Re-testing Cycle:** Each fix will be re-tested before marking defect as closed

---

## Environment & Data Requirements

### Test Environments

| Environment | Purpose | URL/Location | Availability |
|-------------|---------|--------------|--------------|
| Local Development | Initial testing and defect verification | `localhost` via local server | Available now |
| QA Environment | Staging-like testing (if available) | TBD | TBD |
| QA-Mobile | Mobile responsive testing | Physical devices or emulators | Available now |

### Test Data Requirements

**Valid Test Data:**
- **User Credentials:** `test@example.com` / `SecurePass123!` (or as configured in app)
- **Guest Names:** `John Doe`, `Jane Smith` (valid formats)
- **Email:** `test@example.com`, `user@test.org`
- **Phone:** `+1-555-123-4567`, `555-123-4567`
- **Dates:** Future dates with 1+ night difference (e.g., check-in: tomorrow, check-out: day after tomorrow)
- **Guests:** 1, 2, 3 (within room capacity)

**Invalid Test Data:**
- Empty fields: All form fields tested empty
- Whitespace-only: Fields with only spaces
- Invalid email: `test@`, `@example.com`, `test.example.com`
- Invalid phone: `abc`, `123`, `1234567890123456` (too long)
- Invalid dates: Past dates, same-day check-out
- Invalid guests: 0, -1, 1.5, text input

**Room Data (for price verification):**
- Deluxe Room: $129 original, 20% discount → $103.20/night
- Standard Room: $99 original, 15% discount → $84.15/night
- Suite: $199 original, 25% discount → $149.25/night

### Dependencies

- **Code Deployment:** Latest code with defect fixes must be deployed to test environment
- **Design Assets:** Room images must be available and accessible (fix DEF-010)
- **Browser/Device Access:** Chrome, Firefox, Safari, Edge desktop browsers; iOS and Android mobile devices or emulators
- **Test Account:** Valid test credentials for login testing

---

## Entry and Exit Criteria

### Entry Criteria (Must be met before testing begins)

| Criteria | Status | Notes |
|----------|--------|-------|
| Build deployed to test environment | ⬜ Pending | Local server or QA environment |
- Unit tests passed (if available) | ⬜ N/A | No unit tests currently |
- All 25 defects marked as "Fixed" in defect tracker | ⬜ Pending | Developer confirmation required |
- Test environment accessible | ⬜ Pending | Local environment available |
- Test data prepared | ✅ Complete | Data documented in this plan |
- Test cases reviewed and approved | ✅ Complete | Based on test review document |

### Exit Criteria (Must be met to pass sprint)

| Criteria | Target | Actual |
|----------|--------|--------|
- All High-priority test cases executed | 100% | TBD |
- All 25 defects verified as fixed | 100% | TBD |
- Zero Critical bugs open | 0 | TBD |
- Zero High-severity bugs open | 0 | TBD |
- Medium-severity bugs < 5 | <5 | TBD |
- Core user flow (Login→Rooms→Booking→Confirm) working | Pass | TBD |
- Cross-browser compatibility verified | 4 browsers | TBD |
- Basic accessibility standards met | Pass | TBD |
- Test execution report completed | Yes | TBD |

**Go/No-Go Decision:** Sprint cannot be marked complete until all exit criteria are met. Any blocking issues will require sprint extension or defect deferral.

---

## Risks & Dependencies

### Risks

| Risk | Impact | Likelihood | Mitigation Strategy | Owner |
|------|--------|------------|-------------------|-------|
| Critical login defects not fixed | High | Medium | Prioritize login defects first; create test account workaround | Dev Team |
| Room images still broken (DEF-010) | Medium | Low | Use placeholder images if original URLs cannot be fixed | Dev Team |
| Cross-browser compatibility issues | Medium | Medium | Early cross-browser testing; flag issues immediately | QA Team |
| Mobile responsive layout failures | Medium | Medium | Test on mobile early; prioritize responsive fixes | Dev Team |
| Price calculation defects persist | High | Low | Dedicated price verification test suite; manual calculation verification | QA Team |
| Test environment instability | High | Low | Use local development environment as backup | QA Team |
| Incomplete defect fixes | High | Medium | Daily defect triage; clear acceptance criteria for each fix | Dev Team |

### Dependencies

| Dependency | Type | Status | Contingency |
|------------|------|--------|-------------|
| Code deployment to test environment | Technical | Pending | Use local development environment |
- Developer availability for defect fixes | Resource | TBD | Prioritize critical defects only |
- Room image assets (fix DEF-010) | Technical | Pending | Use placeholder images if unavailable |
- Mobile devices/emulators for testing | Technical | Available | Use browser dev tools mobile emulation |
- Defect tracking system access | Tool | TBD | Use spreadsheet if Jira unavailable |

---

## Deliverables & Schedule

### Sprint Timeline (2 Weeks)

| Day | Activity | Deliverable | Owner |
|-----|----------|-------------|-------|
| Day 1 | Sprint planning, test environment setup, smoke testing | Environment ready, smoke test report | QA Team |
| Day 2 | Defect verification (Login & Rooms defects DEF-001 to DEF-012) | Defect verification report (Part 1) | QA Team |
| Day 3 | Defect verification (Booking & Confirmation defects DEF-013 to DEF-025) | Defect verification report (Part 2) | QA Team |
| Day 4 | Functional testing (end-to-end user stories) | Functional test report | QA Team |
| Day 5 | Form validation testing | Validation test report | QA Team |
| Day 6 | Cross-browser & mobile testing | Cross-browser test report | QA Team |
| Day 7 | Accessibility testing | Accessibility test report | QA Team |
| Day 8 | Regression testing (critical areas) | Regression test report | QA Team |
| Day 9 | Bug re-testing (if any found) | Bug re-test report | QA Team |
| Day 10 | Final sign-off, test execution summary | Sprint test execution report | QA Team |

### Deliverables

| Deliverable | Due Date | Format | Location |
|-------------|----------|--------|----------|
| Test Execution Summary | Day 10 | Document | Project repository |
- Defect Verification Report | Day 3 | Document | Project repository |
- Functional Test Report | Day 4 | Document | Project repository |
- Cross-Browser Test Report | Day 6 | Document | Project repository |
- Accessibility Test Report | Day 7 | Document | Project repository |
- Bug Reports (if any new defects found) | As found | Defect tracker | Jira/Spreadsheet |
- Test Metrics Dashboard | Day 10 | Document/Spreadsheet | Project repository |

### Test Metrics to Track

- **Test Execution Progress:** % of test cases executed
- **Defect Detection Rate:** Number of new defects found
- **Defect Fix Rate:** % of sprint defects verified as fixed
- **Test Case Pass Rate:** % of test cases passed
- **Coverage:** % of in-scope user stories tested
- **Blockers:** Number of blocking issues identified

---

## Appendix

### A. Referenced Documents

- `resources/bookNow_Test_Review.md` - Feature requirements, validation rules, and defect list
- `index.html` - Application markup
- `app.js` - Application logic

### B. Contact Information

| Role | Name | Contact |
|------|------|---------|
| QA Lead | TBD | TBD |
- Developer Lead | TBD | TBD |
- Product Owner | TBD | TBD |

### C. Definitions

- **Critical Bug:** Blocks core functionality or testing; requires immediate fix
- **High Bug:** Major functionality broken but workaround exists
- **Medium Bug:** Minor functionality issues or UI problems
- **Low Bug:** Cosmetic issues or nice-to-have improvements
- **Defect:** Known issue identified in test review (DEF-001 to DEF-025)
- **User Story:** Feature requirement (US-001 to US-004)

---

**Document Approval:**

| Role | Name | Signature | Date |
|------|------|-----------|------|
| QA Lead | | | |
| Developer Lead | | | |
| Product Owner | | | |
