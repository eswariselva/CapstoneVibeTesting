# BookNow App - Comprehensive Test Cases

**Application:** BookNow (Login → Rooms → Booking → Confirmation)
**Document Version:** 1.0
**Total Test Cases:** 25
**Coverage:** Happy Path, Negative Testing, Edge Cases, Boundary Values, Security, Accessibility

---

## Feature 1: Login Functionality

### TC_LOGIN_01: Valid User Login (Happy Path)
- **TC ID:** TC_LOGIN_01
- **Title:** Verify successful login with valid credentials
- **Precondition:** Application is loaded on Login page
- **Steps to Reproduce:** 
  1. Enter valid email: guest@booknow.com
  2. Enter valid password: stay2026
  3. Click "Sign In" button
- **Expected Result:** User is redirected to Rooms page, navbar becomes visible, session state is set
- **Priority:** High
- **Severity:** Critical

### TC_LOGIN_02: Invalid Credentials (Negative Testing)
- **TC ID:** TC_LOGIN_02
- **Title:** Verify login fails with invalid credentials
- **Precondition:** Application is loaded on Login page
- **Steps to Reproduce:**
  1. Enter invalid email: wrong@email.com
  2. Enter invalid password: wrongpass
  3. Click "Sign In" button
- **Expected Result:** Error message displayed ("Invalid email or password"), user remains on Login page
- **Priority:** High
- **Severity:** Critical

### TC_LOGIN_03: Empty Fields (Edge Case)
- **TC ID:** TC_LOGIN_03
- **Title:** Verify login fails with empty email and password fields
- **Precondition:** Application is loaded on Login page
- **Steps to Reproduce:**
  1. Leave email field empty
  2. Leave password field empty
  3. Click "Sign In" button
- **Expected Result:** Required field errors shown, user remains on Login page
- **Priority:** High
- **Severity:** Critical

### TC_LOGIN_04: Whitespace-Only Input (Boundary Value)
- **TC ID:** TC_LOGIN_04
- **Title:** Verify login fails with whitespace-only credentials
- **Precondition:** Application is loaded on Login page
- **Steps to Reproduce:**
  1. Enter email with only spaces: "   "
  2. Enter password with only spaces: "   "
  3. Click "Sign In" button
- **Expected Result:** Required field errors shown, whitespace is trimmed/rejected
- **Priority:** Medium
- **Severity:** Major

### TC_LOGIN_05: Email Format Validation (Edge Case)
- **TC ID:** TC_LOGIN_05
- **Title:** Verify email format validation with various invalid formats
- **Precondition:** Application is loaded on Login page
- **Steps to Reproduce:**
  1. Test invalid email formats: "test@", "@example.com", "test.example.com", "test @example.com"
  2. Enter valid password: stay2026
  3. Click "Sign In" button
- **Expected Result:** Invalid email formats are rejected with appropriate error message
- **Priority:** Medium
- **Severity:** Major

---

## Feature 2: Rooms Listing

### TC_ROOMS_01: Room Display Completeness (Happy Path)
- **TC ID:** TC_ROOMS_01
- **Title:** Verify all room details are displayed correctly
- **Precondition:** User is logged in and on Rooms page
- **Steps to Reproduce:**
  1. Navigate to Rooms page
  2. Verify each room card displays: image, name, description, original price, discounted price, discount badge, availability status
- **Expected Result:** All 4 rooms show complete information with correct data
- **Priority:** High
- **Severity:** Critical

### TC_ROOMS_02: Price Calculation Accuracy (Boundary Value)
- **TC ID:** TC_ROOMS_02
- **Title:** Verify discounted price calculation is correct for all rooms
- **Precondition:** User is on Rooms page
- **Steps to Reproduce:**
  1. Check Deluxe Room: $129 with 20% discount should show $103.20
  2. Check Superior Room: $89 with 10% discount should show $80.10
  3. Check Family Suite: $199 with 15% discount should show $169.15
  4. Check Penthouse Suite: $299 with 5% discount should show $284.05
- **Expected Result:** All discounted prices are calculated correctly (price × (1 - discount/100))
- **Priority:** High
- **Severity:** Critical

### TC_ROOMS_03: Broken Image Handling (Negative Testing)
- **TC ID:** TC_ROOMS_03
- **Title:** Verify broken room images are handled gracefully
- **Precondition:** User is on Rooms page
- **Steps to Reproduce:**
  1. Check Room 1 (Deluxe Room) with broken image URL
  2. Verify fallback behavior
- **Expected Result:** Broken images show placeholder or alt text, no broken image icons
- **Priority:** Medium
- **Severity:** Major

### TC_ROOMS_04: Room Selection Flow (Happy Path)
- **TC ID:** TC_ROOMS_04
- **Title:** Verify room selection carries correct data to booking page
- **Precondition:** User is on Rooms page
- **Steps to Reproduce:**
  1. Click "Select Room" on Superior Room
  2. Verify navigation to Booking page
  3. Verify selected room data is preserved
- **Expected Result:** User is navigated to Booking page with correct room selected
- **Priority:** High
- **Severity:** Critical

### TC_ROOMS_05: Availability Badge Consistency (Edge Case)
- **TC ID:** TC_ROOMS_05
- **Title:** Verify availability badge text and styling are consistent
- **Precondition:** User is on Rooms page
- **Steps to Reproduce:**
  1. Check all room availability badges
  2. Verify badge text matches styling (Available vs Sold out)
  3. Verify button state matches availability
- **Expected Result:** Badge text and styling are consistent, sold-out rooms have disabled buttons
- **Priority:** Medium
- **Severity:** Major

---

## Feature 3: Booking Form

### TC_BOOK_01: Complete Valid Booking (Happy Path)
- **TC ID:** TC_BOOK_01
- **Title:** Verify successful booking with all valid fields
- **Precondition:** User has selected a room and is on Booking page
- **Steps to Reproduce:**
  1. Enter valid first name: John
  2. Enter valid last name: Smith
  3. Enter valid email: john@example.com
  4. Enter valid phone: +1-555-123-4567
  5. Select future check-in date
  6. Select future check-out date (1+ nights)
  7. Enter valid guest count: 2
  8. Click "Book Now"
- **Expected Result:** Form validation passes, user is navigated to Confirmation page
- **Priority:** High
- **Severity:** Critical

### TC_BOOK_02: Empty Form Validation (Negative Testing)
- **TC ID:** TC_BOOK_02
- **Title:** Verify all required fields show errors when form is empty
- **Precondition:** User is on Booking page
- **Steps to Reproduce:**
  1. Leave all form fields empty
  2. Click "Book Now"
- **Expected Result:** All required field errors are displayed simultaneously, focus moves to first error
- **Priority:** High
- **Severity:** Critical

### TC_BOOK_03: Name Validation (Boundary Value)
- **TC ID:** TC_BOOK_03
- **Title:** Verify name field validation with boundary values
- **Precondition:** User is on Booking page
- **Steps to Reproduce:**
  1. Test single character: "A" (should fail - min 2 chars)
  2. Test valid name: "John" (should pass)
  3. Test very long name: 50+ characters (should fail)
  4. Test special characters: "John@123" (should fail)
  5. Test valid special chars: "Mary-Jane O'Connor" (should pass)
- **Expected Result:** Names are validated for length, allowed characters, and format
- **Priority:** High
- **Severity:** Major

### TC_BOOK_04: Date Validation (Edge Case)
- **TC ID:** TC_BOOK_04
- **Title:** Verify date field validation with edge cases
- **Precondition:** User is on Booking page
- **Steps to Reproduce:**
  1. Test past check-in date (should fail)
  2. Test check-out same as check-in (should fail - min 1 night)
  3. Test check-out before check-in (should fail)
  4. Test valid dates with 1 night difference (should pass)
- **Expected Result:** Date validation prevents invalid date ranges and past dates
- **Priority:** High
- **Severity:** Critical

### TC_BOOK_05: Guest Count Validation (Boundary Value)
- **TC ID:** TC_BOOK_05
- **Title:** Verify guest count validation with boundary values
- **Precondition:** User is on Booking page
- **Steps to Reproduce:**
  1. Test 0 guests (should fail)
  2. Test negative value: -1 (should fail)
  3. Test decimal: 1.5 (should fail)
  4. Test valid: 1 (should pass)
  5. Test room capacity: if capacity is 4, test 5 (should fail)
- **Expected Result:** Guest count is validated for minimum, maximum, and integer values
- **Priority:** High
- **Severity:** Major

---

## Feature 4: Booking Confirmation

### TC_CONF_01: Successful Booking Confirmation (Happy Path)
- **TC ID:** TC_CONF_01
- **Title:** Verify confirmation page shows all booking details
- **Precondition:** User has completed a valid booking
- **Steps to Reproduce:**
  1. Complete booking with valid data
  2. Verify confirmation page displays:
     - Unique booking reference number
     - Room name and details
     - Check-in and check-out dates
     - Number of nights
     - Guest count and name
     - Total amount
- **Expected Result:** All booking details are displayed correctly and match the form data
- **Priority:** High
- **Severity:** Critical

### TC_CONF_02: Form Reset After Booking (Edge Case)
- **TC ID:** TC_CONF_02
- **Title:** Verify form and state are reset after successful booking
- **Precondition:** User has completed a booking
- **Steps to Reproduce:**
  1. Complete first booking
  2. Click "Browse More Rooms"
  3. Select a different room
  4. Verify booking form is empty
  5. Verify no stale data from previous booking
- **Expected Result:** Form fields are cleared, selected room is reset, no stale data persists
- **Priority:** High
- **Severity:** Major

### TC_CONF_03: Invalid Form No Confirmation (Negative Testing)
- **TC ID:** TC_CONF_03
- **Title:** Verify confirmation page is not accessible with invalid data
- **Precondition:** User is on Booking page
- **Steps to Reproduce:**
  1. Submit booking with invalid/incomplete data
  2. Attempt to access confirmation page
- **Expected Result:** Confirmation page is not shown, user remains on booking page with errors
- **Priority:** High
- **Severity:** Critical

### TC_CONF_04: Refresh/Back Button Handling (Edge Case)
- **TC ID:** TC_CONF_04
- **Title:** Verify page refresh and back button don't duplicate bookings
- **Precondition:** User is on Confirmation page
- **Steps to Reproduce:**
  1. Complete a booking
  2. Refresh the browser page
  3. Use browser Back button
- **Expected Result:** No duplicate booking is created, system handles navigation gracefully
- **Priority:** Medium
- **Severity:** Major

### TC_CONF_05: Special Character Handling (Security Testing)
- **TC ID:** TC_CONF_05
- **Title:** Verify special characters in guest details are sanitized
- **Precondition:** User is on Booking page
- **Steps to Reproduce:**
  1. Enter guest name with HTML/script tags: "<script>alert('test')</script>"
  2. Complete booking
  3. Check confirmation page
- **Expected Result:** Special characters are displayed as plain text, no script execution occurs
- **Priority:** Medium
- **Severity:** Major

---

## Feature 5: General & Navigation

### TC_GEN_01: Route Protection (Security Testing)
- **TC ID:** TC_GEN_01
- **Title:** Verify protected pages cannot be accessed without login
- **Precondition:** Application is loaded, user not logged in
- **Steps to Reproduce:**
  1. Try to directly access Rooms page via URL manipulation
  2. Try to directly access Booking page via URL manipulation
  3. Try to directly access Confirmation page via URL manipulation
  4. Click navbar "Rooms" link before login
- **Expected Result:** All protected pages redirect to Login page, navbar is hidden on login
- **Priority:** High
- **Severity:** Critical

### TC_GEN_02: Toast Messages (Happy Path)
- **TC ID:** TC_GEN_02
- **Title:** Verify toast messages appear for success and error states
- **Precondition:** User is using the application
- **Steps to Reproduce:**
  1. Test successful login - expect success toast
  2. Test failed login - expect error toast
  3. Test successful booking - expect success toast
  4. Test failed booking - expect error toast
- **Expected Result:** Appropriate toast messages appear and auto-dismiss after 3 seconds
- **Priority:** Medium
- **Severity:** Major

### TC_GEN_03: Keyboard Navigation (Accessibility Testing)
- **TC ID:** TC_GEN_03
- **Title:** Verify complete flow is accessible via keyboard only
- **Precondition:** Application is loaded
- **Steps to Reproduce:**
  1. Navigate through Login → Rooms → Booking → Confirmation using only Tab key
  2. Verify focus is visible on all interactive elements
  3. Verify all buttons can be activated with Enter/Space
  4. Verify logical tab order
- **Expected Result:** Complete booking flow can be accomplished without mouse, focus is clearly visible
- **Priority:** Medium
- **Severity:** Major

### TC_GEN_04: Responsive Design (Edge Case)
- **TC ID:** TC_GEN_04
- **Title:** Verify layout adapts to different screen sizes
- **Precondition:** Application is loaded
- **Steps to Reproduce:**
  1. Test on desktop viewport (1920x1080)
  2. Test on tablet viewport (768x1024)
  3. Test on mobile viewport (320x568)
  4. Check for horizontal scroll on all viewports
  5. Verify cards and elements don't break
- **Expected Result:** Layout adapts smoothly, no horizontal scroll, all elements remain functional
- **Priority:** Medium
- **Severity:** Major

### TC_GEN_05: Price Calculation Live Update (Happy Path)
- **TC ID:** TC_GEN_05
- **Title:** Verify booking summary updates when dates change
- **Precondition:** User has selected a room and is on Booking page
- **Steps to Reproduce:**
  1. Select check-in date
  2. Select check-out date (3 nights later)
  3. Verify summary shows correct nights calculation
  4. Verify total is calculated correctly
  5. Change dates to different values
  6. Verify summary updates immediately
- **Expected Result:** Summary updates in real-time, nights and total are calculated correctly
- **Priority:** High
- **Severity:** Critical

---

## Test Coverage Summary

| Feature | Test Cases | Coverage Types |
|---------|------------|----------------|
| Login Functionality | 5 | Happy Path, Negative, Edge Cases, Boundary Values |
| Rooms Listing | 5 | Happy Path, Negative, Edge Cases, Boundary Values |
| Booking Form | 5 | Happy Path, Negative, Edge Cases, Boundary Values |
| Booking Confirmation | 5 | Happy Path, Negative, Edge Cases, Security |
| General & Navigation | 5 | Security, Accessibility, UI/UX, Happy Path |
| **Total** | **25** | **Comprehensive Coverage** |

---

## Test Case Distribution by Priority

| Priority | Count | Percentage |
|----------|-------|------------|
| High | 14 | 56% |
| Medium | 11 | 44% |
| Low | 0 | 0% |

---

## Test Case Distribution by Severity

| Severity | Count | Percentage |
|----------|-------|------------|
| Critical | 10 | 40% |
| Major | 15 | 60% |
| Minor | 0 | 0% |

---

## Test Execution Notes

1. **Environment Setup:** Ensure application is running on localhost or test environment
2. **Test Data:** Use the provided test credentials and sample data
3. **Browser Compatibility:** Execute tests on Chrome, Firefox, Safari, and Edge
4. **Mobile Testing:** Execute responsive design tests on actual mobile devices or emulators
5. **Defect Reporting:** Log any deviations from expected results in the defect tracking system
6. **Regression Testing:** Re-executed critical test cases after any bug fixes

---

## Document References

- `BookNow_Requirements.md` - Feature requirements and validation rules
- `BookNow_TestPlan.md` - Sprint testing approach and schedule
- `BookNow_Test_Scenarios.md` - Detailed test scenarios
- `index.html` - Application markup structure
- `app.js` - Application logic and known defects

---

**Document Status:** Ready for Test Execution
**Last Updated:** 2026-09-24
**Prepared By:** QA Team
**Approved By:** Pending