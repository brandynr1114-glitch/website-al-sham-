---
name: testing-al-sham-landing-page
description: Test the AL-SHAM restaurant landing page end-to-end. Use when verifying UI features, delivery links, contact form, gallery, certificate modal, or responsive layout.
---

# Testing AL-SHAM Landing Page

## Overview
Single-file HTML/CSS/JS landing page deployed as a static site. No build step, no framework — just `index.html` with inline styles and scripts.

## Live Preview
Deploy via `deploy frontend` tool pointing at the repo root directory. The site is static HTML so any static hosting works.

## Key Test Areas

### 1. Navigation Links
- Verify nav contains: Home, About, Locations, Menu, Contact, Order Online
- "About" should scroll to `#about` section
- "Contact" should scroll to `#contact` section  
- "Menu" link should open `https://ordersetups.com` in a new tab (`target="_blank"`)

### 2. Delivery Links (DoorDash & Uber Eats)
- Links appear in **3 locations**: hero section, CTA banner, and footer
- Verify all 6 links contain the correct store IDs
- Use browser console to query all `a[href*="doordash"]` and `a[href*="ubereats"]` selectors to batch-verify

### 3. Gallery Images
- 6 images in a grid, each wrapped in an `<a>` tag
- Odd images (1,3,5) → `instagram.com` with `fa-instagram` icon overlay
- Even images (2,4,6) → `facebook.com` with `fa-facebook-f` icon overlay
- Hover to see the social icon overlay appear

### 4. Customer Reviews
- 3 review cards with specific quotes and reviewer names
- Each card has 5 gold star icons (`fa-star`)
- Cards have hover scale/lift micro-interaction

### 5. Contact Form
- HTML5 validation: `required` on Name, Email, Message fields
- Submit with valid data triggers `alert()` with thank-you message
- Form resets after submission (`this.reset()` in onsubmit handler)
- The form uses `event.preventDefault()` — no actual backend submission

### 6. Halal Certificate Modal
- 3 thumbnails in footer under "Halal Certified"
- Clicking a thumbnail opens a full-screen modal with the certificate image
- **3 close methods to test:** X button, Escape key, backdrop (overlay) click
- Modal sets `body.style.overflow = 'hidden'` when open
- Certificate images are local files in `images/` directory — must be deployed alongside `index.html`

### 7. Footer Links
- Careers link: `mailto:careers@alshamfood.com` with `fa-briefcase` icon
- Contact email: `mailto:info@alshamfood.com`
- Phone: `tel:+12155551234`

### 8. Mobile Responsiveness
- CSS breakpoint at `max-width: 768px`
- `.menu-toggle` button (hamburger) is `display: none` at desktop, `display: block` at mobile
- Nav links reposition to fixed overlay with slide-in animation
- If you cannot physically resize the browser viewport in the test environment, verify CSS media query rules programmatically via `document.styleSheets` inspection

## Testing Tips

- **Use browser console for batch verification:** Query multiple elements at once (e.g., `document.querySelectorAll('a[href*="doordash"]')`) rather than clicking each link individually. This is faster and more reliable for verifying hrefs.
- **Modal close via Escape key:** Use `{"action": "key", "key": "Escape", "text": "Escape"}` format in the computer tool — the `text` parameter is required.
- **Certificate images:** These are local PNG files in `images/` directory. They must be present in the deployed directory or they'll show as broken images. If deploying, ensure the `images/` folder is included.
- **Contact form alert:** The browser may auto-dismiss the `alert()` dialog in some environments. Verify form reset (fields cleared back to placeholder text) as secondary confirmation that the alert fired and `this.reset()` executed.
- **Unsplash images:** If any food images break (404), replace with a different Unsplash photo ID. Test with `curl -sI <url> | head -1` to verify HTTP 200 before committing.

## No Secrets Needed
This is a fully static site with no backend, no API keys, and no authentication required for testing.
