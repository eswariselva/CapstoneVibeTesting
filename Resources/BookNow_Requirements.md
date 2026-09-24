# BookNow App: Feature, Validation and Defect Review

**Files reviewed:** `index.html`, `app.js`

The app is a 4-screen single-page flow: **Login → Rooms → Booking → Confirmation**.

---

## 1. Features Required

### Login
- Email and password sign-in, with a clear error message on failure
- Password field masked, with an optional show/hide toggle
- Session state (`isLoggedIn` exists but is never set)
- Logged-in user shown in the navbar (`nav-user` exists but is never populated)
- Logout, plus route protection so Rooms, Booking and Confirm can't be reached without login
- Forgot password and Enter-key submit (nice to have)

### Rooms Listing
- Cards showing image, name, description, original price, discounted price, discount badge and availability
- Correct discounted-price calculation
- "Select Room" carries the chosen room into booking
- Availability status that reflects real state (Available / Sold out), with the button disabled when sold out
- Filter/sort by price or type (nice to have)

### Booking
- Guest details: first name, last name, email, phone
- Stay details: check-in, check-out, number of guests
- Live summary: room name, price per night, number of nights (calculated from the dates) and total
- Book Now submits only when the form is valid
- Back/change room option

### Confirmation
- Booking reference number
- Summary of room, dates, guests, guest name and total
- Browse More Rooms, and a cleared form/state for the next booking

### General
- Toast messages for errors and success
- Meaningful page title, navbar visibility rules, responsive layout, accessibility

---

## 2. Validations Required

| Area | Field | Rules |
|---|---|---|
| Login | Email | Required; valid email format; trimmed |
| Login | Password | Required; masked; case-sensitive |
| Login | Submit | Wrong or empty credentials show an error and stay on the login page; no user enumeration ("invalid email or password") |
| Booking | First / Last name | Required; letters, spaces, hyphens and apostrophes only; min 2 and max ~50 chars; whitespace-only rejected |
| Booking | Email | Required; valid format |
| Booking | Phone | Required; digits, `+`, spaces and dashes only; length 7–15 digits |
| Booking | Check-in | Required; not in the past |
| Booking | Check-out | Required; must be after check-in; minimum 1 night; sensible maximum stay |
| Booking | Guests | Required; integer ≥ 1; must not exceed room capacity; reject decimals, negatives, 0 and typed text |
| Booking | Submit | All errors shown together next to each field; focus moves to the first error; double-click doesn't create two bookings |
| Flow | Room selected | Booking page can't be opened without a selected room |
| Price | Total | Nights × discounted price, rounded to 2 decimals; updates whenever either date changes |

---

## 3. Defects Visible in the Code

### Login
1. Wrong credentials still go to the Rooms page (`buggyLogin` calls `showPage('rooms')` in both branches).
2. The error message box (`login-error`) is never used.
3. The password input is `type="text"`, so the password is visible.
4. No empty-field check.
5. The navbar is visible on the login page, because it has no `hidden` class initially. Its Rooms link works without login.
6. `isLoggedIn` is never set, and there is no logout.
7. Credentials are hardcoded in client-side JS and shown on the page (fine for a demo, but a security finding in a real app).

### Rooms
8. The discount is calculated with `/1000` instead of `/100`, so 20% off shows as 2% off, while the badge still says "20% OFF".
9. Every card has the availability badge styled `badge-unavailable` but labelled "Available".
10. Room 1's image URL is broken (404) and the image has no `alt`.
11. Room 3 has an empty `alt`, and its long description overflows the card (`overflow-bug` class).

### Booking
12. `buggyUpdateTotal()` is empty, so the total never updates when dates change.
13. Nights are stuck at 1 (`_frozenNights`), so the total is always one night, and the summary says "Select dates above to calculate total".
14. `buggyPlaceBooking()` goes straight to Confirm with no validation. All the `err-*` spans are never shown, so blank forms are accepted.
15. Email and phone use `type="text"` rather than `email` / `tel`.
16. The date inputs have no `min`, and check-out isn't tied to check-in.
17. Guests can be set to 0 or negative by typing (`min` isn't enforced on typed input) and has no maximum.
18. Booking labels lack `for` attributes, so they aren't linked to their inputs.

### Confirmation and General
19. The confirmation page shows no booking details or reference number.
20. The form isn't reset after booking, and `selectedRoom` persists.
21. `showToast` is never called.
22. Nav links are `<a>` tags without `href`, so they're not keyboard-focusable. The brand is a clickable `div`.
23. The page title is "Untitled".
24. The browser Back button isn't handled (no routing or history), so it leaves the app or breaks the flow.
25. The class `btn-book-buggy` and the `buggy*` function names suggest intentionally seeded bugs, so check whether `style.css` (not provided) has more, such as badge colours and overflow styling.

---

## 4. Suggested Test Focus

- Positive and negative login tests (valid, invalid, empty, whitespace, SQL/script strings)
- Boundary tests on dates (same-day, past, one night, very long stay) and guests (0, 1, max, max+1, decimals)
- Price verification per room (e.g. Deluxe $129 at 20% should be $103.20, and 3 nights should be $309.60)
- UI checks for images, alt text, text overflow, badge text and colour
- Navigation tests: direct access, back button, refresh mid-flow
- Cross-browser and mobile responsive checks, plus keyboard and screen-reader accessibility
