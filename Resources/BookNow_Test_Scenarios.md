# BookNow: Test Scenario Document

**Application:** BookNow (Login → Rooms → Booking → Confirmation)
**Sprint:** Sprint 1
**Basis:** `BookNow_Requirements.md`, `BookNow_TestPlan.md`, `index.html`, `app.js`
**Priority:** High / Medium / Low
**Testing Types:** Functional, UI, Security, Accessibility, Compatibility, Regression

These are kept at scenario level (what to verify). Exact inputs, steps and expected results belong in the test cases. Positive, negative, edge and boundary coverage is folded into the scenario wording.

---

## 1. Login (US-001, DEF-001 to DEF-007)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_LOGIN_01 | US-001 | Login | Verify a user can log in with valid credentials and land on the Rooms page with the navbar and user name shown | High | Functional |
| TS_LOGIN_02 | US-001, DEF-001, DEF-002 | Login | Verify wrong email, wrong password, or both are rejected with a generic error message and the user stays on the Login page | High | Functional |
| TS_LOGIN_03 | US-001, DEF-002 | Login | Verify empty, partially filled and whitespace-only credentials are rejected with required-field errors | High | Functional |
| TS_LOGIN_04 | US-001 | Login | Verify email format validation (missing `@`, missing domain, spaces) and that surrounding spaces in a valid email are trimmed | Medium | Functional |
| TS_LOGIN_05 | US-001 | Login | Verify the password is case-sensitive and that leading/trailing spaces are not silently ignored | Medium | Functional |
| TS_LOGIN_06 | US-001, DEF-003 | Login | Verify the password field is masked and never appears as plain text | High | Security |
| TS_LOGIN_07 | US-001 | Login | Verify very long inputs, special characters and injection strings (SQL/script) are handled safely without errors or code execution | Medium | Security |
| TS_LOGIN_08 | US-001, DEF-005 | Login | Verify the navbar is hidden on the Login page and appears only after successful login | Medium | UI |
| TS_LOGIN_09 | US-001, DEF-007 | Login | Verify credentials aren't exposed in the page or source beyond the agreed demo hint | Medium | Security |
| TS_LOGIN_10 | US-001 | Login | Verify repeated rapid clicks on Sign In and repeated failed attempts behave consistently, with no duplicate navigation or crash | Low | Functional |

---

## 2. Session, Navigation and Route Protection (US-001, DEF-004, DEF-006, DEF-024)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_NAV_01 | US-001, DEF-004 | Session | Verify the session is maintained across pages and the logged-in user's identity is displayed | High | Functional |
| TS_NAV_02 | US-001 | Session | Verify logout ends the session, returns to Login and hides the navbar | High | Functional |
| TS_NAV_03 | US-001 | Route Protection | Verify Rooms, Booking and Confirmation can't be accessed without logging in (direct access, Back button, DOM manipulation) | High | Security |
| TS_NAV_04 | US-003, US-004 | Route Protection | Verify Booking can't be opened without a selected room and Confirmation can't be reached without a completed booking | High | Functional |
| TS_NAV_05 | DEF-024 | Navigation | Verify browser Back/Forward and page refresh at each screen keep the flow and state consistent (no broken pages, no resubmission) | High | Functional |
| TS_NAV_06 | DEF-022 | Navigation | Verify the navbar brand and Rooms link navigate correctly and are keyboard-focusable | Medium | Functional |

---

## 3. Rooms Listing (US-002, DEF-008 to DEF-012)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_ROOM_01 | US-002 | Rooms | Verify all rooms display with image, name, description, original price, discounted price, discount badge and availability | High | Functional |
| TS_ROOM_02 | US-002, DEF-008 | Rooms | Verify the discounted price is calculated correctly for every room, is formatted to 2 decimals, and matches the discount badge | High | Functional |
| TS_ROOM_03 | US-002, DEF-009 | Rooms | Verify the availability badge text and colour agree, and a sold-out room shows "Sold out" with Select Room disabled | High | Functional |
| TS_ROOM_04 | US-002, DEF-010 | Rooms | Verify every room image loads and a broken image falls back to a placeholder | High | UI |
| TS_ROOM_05 | US-002, DEF-011 | Rooms | Verify every image has meaningful alt text | Medium | Accessibility |
| TS_ROOM_06 | US-002, DEF-012 | Rooms | Verify long descriptions wrap or truncate without overflowing the card and cards stay aligned | Medium | UI |
| TS_ROOM_07 | US-002, US-003 | Rooms | Verify Select Room carries the correct room into Booking, and choosing a different room later updates it | High | Functional |
| TS_ROOM_08 | US-002 | Rooms | Verify rapid double-clicks on Select Room and returning to Rooms don't select the wrong room or duplicate cards | Low | Functional |

---

## 4. Booking: Guest Details (US-003, DEF-014, DEF-015, DEF-019)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_BOOK_01 | US-003 | Booking | Verify a booking with all valid guest and stay details is submitted successfully | High | Functional |
| TS_BOOK_02 | US-003, DEF-014 | Booking | Verify submitting an empty form shows all required-field errors together, moves focus to the first error, and blocks submission | High | Functional |
| TS_BOOK_03 | US-003 | Booking | Verify first and last name rules: required, whitespace-only rejected, min 2 / max 50 characters, allowed characters only (letters, spaces, hyphens, apostrophes) | High | Functional |
| TS_BOOK_04 | US-003, DEF-015 | Booking | Verify email is required and validated for format, including invalid, valid and edge formats (subdomains, plus-tags) | High | Functional |
| TS_BOOK_05 | US-003, DEF-015 | Booking | Verify phone is required and validated for allowed characters and 7 to 15 digit length (both boundaries) | High | Functional |
| TS_BOOK_06 | US-003 | Booking | Verify error messages clear when the field is corrected and entered data is retained after a failed submit | Medium | Functional |
| TS_BOOK_07 | US-003 | Booking | Verify double-clicking Book Now doesn't create duplicate bookings | High | Functional |
| TS_BOOK_08 | US-003 | Booking | Verify script/HTML input and very long text in guest fields are sanitised and don't break the layout | Medium | Security |
| TS_BOOK_09 | DEF-019 | Booking | Verify form labels are associated with their inputs and clicking a label focuses the field | Medium | Accessibility |

---

## 5. Booking: Stay Dates (US-003, DEF-013 to DEF-016)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_DATE_01 | US-003 | Booking | Verify valid future check-in and check-out dates (minimum 1 night) are accepted | High | Functional |
| TS_DATE_02 | US-003 | Booking | Verify check-in and check-out are required | High | Functional |
| TS_DATE_03 | US-003, DEF-016 | Booking | Verify past check-in dates are rejected and today is accepted (boundary) | High | Functional |
| TS_DATE_04 | US-003, DEF-016 | Booking | Verify check-out must be after check-in: same day and earlier dates are rejected, next day is accepted | High | Functional |
| TS_DATE_05 | US-003 | Booking | Verify the maximum stay limit, and very long stays, are handled per the business rule | Medium | Functional |
| TS_DATE_06 | US-003 | Booking | Verify changing or clearing one date re-validates the other and doesn't leave stale values | Medium | Functional |
| TS_DATE_07 | US-003 | Booking | Verify date calculations across month-end, year-end and leap-day, plus invalid manually typed dates | Medium | Functional |

---

## 6. Booking: Number of Guests (US-003, DEF-017)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_GUEST_01 | US-003 | Booking | Verify valid guest counts (1 up to the room's capacity) are accepted | High | Functional |
| TS_GUEST_02 | US-003, DEF-017 | Booking | Verify boundary values: 0 and negatives are rejected, 1 is accepted, capacity is accepted, capacity + 1 is rejected | High | Functional |
| TS_GUEST_03 | US-003, DEF-017 | Booking | Verify decimals, text, symbols, empty and very large values are rejected with a clear message | Medium | Functional |
| TS_GUEST_04 | US-003 | Booking | Verify the capacity limit is applied per selected room | Medium | Functional |

---

## 7. Price Calculation and Booking Summary (US-003, DEF-013)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_PRICE_01 | US-003, DEF-013 | Price | Verify nights are calculated from the selected dates and the total is nights × discounted price for every room | High | Functional |
| TS_PRICE_02 | US-003, DEF-013 | Price | Verify the summary updates immediately when either date changes | High | Functional |
| TS_PRICE_03 | US-003 | Price | Verify totals are rounded to 2 decimals without floating-point errors at 1 night, multi-night and very long stays | High | Functional |
| TS_PRICE_04 | US-003 | Price | Verify the summary handles missing or invalid dates without showing negative or incorrect totals, and the helper text disappears once dates are valid | Medium | Functional |
| TS_PRICE_05 | US-002, US-003 | Price | Verify price consistency across Rooms, Booking summary and Confirmation | High | Regression |
| TS_PRICE_06 | US-003 | Price | Verify the summary reflects the selected room and resets for each new booking (no stale nights or total) | Medium | Functional |
| TS_PRICE_07 | US-003 | Price | Verify tampering with price or room data from the browser doesn't alter the confirmed total | Low | Security |

---

## 8. Confirmation (US-004, DEF-020, DEF-021)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_CONF_01 | US-004, DEF-020 | Confirmation | Verify a successful booking shows a unique booking reference number | High | Functional |
| TS_CONF_02 | US-004, DEF-020 | Confirmation | Verify the confirmation shows room, dates, nights, guests, guest name and total, all matching the entered data | High | Functional |
| TS_CONF_03 | US-004 | Confirmation | Verify confirmation is not shown when validation fails | High | Functional |
| TS_CONF_04 | US-004, DEF-021 | Confirmation | Verify the form, selected room and summary are reset after booking so the next booking starts clean | High | Functional |
| TS_CONF_05 | US-004 | Confirmation | Verify refresh or Back on the confirmation page doesn't duplicate the booking or show stale data | Medium | Functional |
| TS_CONF_06 | US-004 | Confirmation | Verify two consecutive bookings with different rooms each show their own correct details | Medium | Regression |
| TS_CONF_07 | US-004 | Confirmation | Verify special characters in guest details render as plain text | Medium | Security |
| TS_CONF_08 | US-004 | Confirmation | Verify Browse More Rooms returns to the Rooms page | Low | Functional |

---

## 9. General: Toasts, Title, Accessibility and Compatibility (DEF-022, DEF-023, DEF-025)

| Scenario ID | Requirement ID | Module | Test Scenario Description | Priority | Testing Type |
|---|---|---|---|---|---|
| TS_GEN_01 | DEF-022 | Toast Messages | Verify success and error toasts appear for login and booking outcomes, auto-dismiss, and don't overlap | Medium | Functional |
| TS_GEN_02 | DEF-023 | Page Title | Verify a meaningful page title is shown on every screen | Low | UI |
| TS_GEN_03 | Test Plan: Accessibility | Accessibility | Verify the whole flow is completable with keyboard only, with visible focus and logical tab order | Medium | Accessibility |
| TS_GEN_04 | Test Plan: Accessibility | Accessibility | Verify error messages are announced to screen readers and aren't communicated by colour alone, with adequate contrast | Medium | Accessibility |
| TS_GEN_05 | Test Plan: Responsive | Responsive UI | Verify layouts adapt on desktop, tablet and mobile (down to 320 px) with no horizontal scroll or broken cards | Medium | UI |
| TS_GEN_06 | Test Plan: Cross-Browser | Compatibility | Verify the full flow, including the date picker, on Chrome, Firefox, Safari, Edge, iOS Safari and Android Chrome | High | Compatibility |
| TS_GEN_07 | Test Plan: Regression | Regression | Verify the end-to-end flow (Login → Rooms → Booking → Confirmation) after all defect fixes | High | Regression |
| TS_GEN_08 | DEF-025 | Styling | Review `style.css` (not yet provided) for further visual defects, such as badge colours and overflow styling | Low | UI |

---

## Coverage Summary

| Module | Scenarios |
|---|---|
| Login | 10 |
| Session, Navigation and Route Protection | 6 |
| Rooms Listing | 8 |
| Booking: Guest Details | 9 |
| Booking: Stay Dates | 7 |
| Booking: Number of Guests | 4 |
| Price Calculation | 7 |
| Confirmation | 8 |
| General | 8 |
| **Total** | **67** |

---

## Notes

1. **Defect IDs:** The DEF ranges come from the test plan. Its numbering is slightly offset from the 25-item list in the earlier review, so confirm the exact IDs against your defect tracker.
2. **Requirement ID gaps:** Accessibility, responsive and cross-browser scenarios have no user story, so they reference the test plan's non-functional scope. Consider adding story IDs for them.
3. **Test data in the plan:** It lists "Standard Room", "Suite" and `test@example.com / SecurePass123!`, which don't match the app (Superior, Family Suite, Penthouse, `guest@booknow.com / stay2026`). Update the plan before writing test cases.
4. **Open business rules:** Room capacity, maximum stay length and login lockout aren't defined, so TS_GUEST_04, TS_DATE_05 and TS_LOGIN_10 need product input.
