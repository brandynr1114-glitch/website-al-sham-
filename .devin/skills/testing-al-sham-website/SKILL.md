---
name: testing-al-sham-website
description: Test the AL-SHAM restaurant landing page end-to-end. Use when verifying UI changes, modal interactions, embed integrations, or link updates.
---

# Testing AL-SHAM Restaurant Website

## Overview
Single-file HTML/CSS/JS landing page deployed to devinapps.com. All code lives in `index.html`.

## Test Environment
- Deploy with `deploy frontend` tool pointing to the repo root directory
- Live preview URL pattern: `https://website-al-sham-{hash}.devinapps.com`
- No build step required — it's a static HTML file

## Key Interactive Features to Test

### 1. Certificate Lightbox Modal
- Certificates are in the footer under "Halal Certified" heading
- Text links (not thumbnails) open a fullscreen modal overlay
- Modal has 3 close methods: X button, Escape key, clicking backdrop
- Certificate images are in `images/` directory (halal-cert-1.png, halal-cert-2.png, halal-cert-3.png)
- Verify each link opens the correct corresponding image by checking `#certModalImg` src

### 2. Instagram Embed
- Located in the Contact section (#contact) under "Follow Us"
- Uses `blockquote.instagram-media` with async `embed.js` script
- The embed may take a few seconds to fully render — wait for the iframe to load
- When rendered, shows profile photo, follower count, and recent posts grid

### 3. Social Media Links
- Links appear in 4 locations: floating sidebar, gallery images, contact section, footer
- Gallery images alternate between Instagram and Facebook links
- Use DOM inspection to verify all href attributes match expected URLs
- Check that no generic placeholder URLs (e.g., `https://instagram.com` without a profile path) remain

### 4. Contact Form
- Has client-side validation (required fields: name, email, message)
- Shows `alert()` on successful submission
- Form resets after submission

### 5. Location Cards & Map
- 10 location cards in a scrollable container
- Clicking a card updates the Google Maps iframe src
- Map iframe might show API key warnings in non-production environments

### 6. Navigation
- Sticky header with smooth scroll to anchor sections
- Mobile hamburger menu at 768px breakpoint
- "Menu" link opens external URL (ordersetups.com) in new tab

## Common Testing Pitfalls
- **Escape key**: The computer tool's `key` action requires a `text` parameter. Use the X button or backdrop click to close modals instead, or use `console` to dispatch keyboard events.
- **Scrolling to footer**: The page is long. Use `document.querySelector('footer').scrollIntoView()` via console instead of many scroll actions.
- **Mobile responsiveness**: Cannot physically resize browser in test environment. Verify via CSS media query inspection using `document.styleSheets` or `window.matchMedia()`.
- **Instagram embed loading**: The embed script loads asynchronously. If the embed appears as a plain blockquote, wait a few seconds and take another screenshot.

## Devin Secrets Needed
No secrets required for testing. The site is a static frontend with no authentication.
