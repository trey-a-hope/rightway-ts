# Rightway TS

A one-page marketing website for **Right Way Traffic Solutions Inc.**, a Denver, Colorado company that provides temporary traffic control (lane closures, work zone setup and flagging crews). The site introduces the company, its leadership team and services, lists career openings, and lets visitors send a message through a PHP contact form.

Built in 2015 with [Materialize CSS](https://materializecss.com/) and jQuery; the footer credits Trey Hope as the site's designer.

## Features

- **Single scrolling page** with a fixed navbar (`Intro`, `About`, `Services`, `Careers`, `Contact`) that uses Materialize's `scrollSpy` to highlight the current section and a slide-out side nav on mobile.
- **Intro section** with eight value cards (Safety Protocols, Reliability, Professional Presence, Sustainability, Quality Assurance, Efficiency, Professional Relationships, Best Practices).
- **About section** describing the company plus bio cards for the President & CEO and the VP of Operations, with photos in `img/profile_*.jpg`.
- **Services section** covering work zone setup and maintenance, 24/7 availability and ATSSA-certified crews.
- **Careers section** with hiring copy and links to outside resources (Colorado traffic, AASHTO, flagger training).
- **Contact form** (name, email, message) that posts to `send.php` with jQuery AJAX, plus a click-to-call phone number.
- **Animated headline** effects and a full-height hero that resizes to the window (`js/init.js`).

## How it works

Everything is static HTML except the contact form:

1. `index.html` holds all page content and an inline script that collects the form fields and sends them to `send.php` with `$.ajax`.
2. `send.php` checks that every field is filled in and the email is valid, then calls PHP's `mail()` to email the message to the site owner, echoing a green success or red error message.
3. `js/init.js` sets up Materialize components (side nav, scrollspy), the rotating headline animation and the hero height.

## Tech stack

- HTML5 and CSS3, with custom styles in `css/style.css`
- [Materialize CSS](https://materializecss.com/) (`css/materialize*.css`, `js/materialize*.js`) for layout, cards and navigation
- jQuery (loaded from the Google and jQuery CDNs) and Modernizr (`js/modernizr.js`)
- Font Awesome icons (`css/font-awesome.min.css`, `font/`, `fonts/`)
- PHP for the contact form (`send.php`)

## Getting started

### Prerequisites

- Any static web server to view the page.
- PHP with a working `mail()` setup (sendmail or SMTP) if you want the contact form to send email.

### Running locally

```bash
git clone https://github.com/trey-a-hope/rightway-ts.git
cd rightway-ts
php -S localhost:8000
```

Then open <http://localhost:8000>. Opening `index.html` directly in a browser works for the layout, but the contact form needs PHP.

### Configuration

The recipient address is hard-coded in `send.php` (`$to`). Change it there to send form submissions somewhere else.

## Project structure

```
rightway-ts/
├── index.html        # The whole site: sections, contact form and its AJAX handler
├── send.php          # Contact form endpoint (validates input and calls mail())
├── app.js            # Leftover AngularJS experiment; not loaded by index.html
├── css/              # Materialize, Font Awesome and custom style.css
├── js/               # Materialize, Modernizr and init.js (UI setup and animations)
├── img/              # Logo, team photos and background images
└── font/, fonts/     # Icon and web fonts
```

## Known limitations

- `send.php` also sends a hard-coded "Test" email on every request (`@mail(..., "Test", "Test Message")`); remove that line before using the form in production.
- The inline submit handler and `send.php` still contain `alert()` debugging calls.
- jQuery is loaded twice (a pinned 1.6.1 build and `jquery-latest.js`) over plain HTTP; pin a single HTTPS copy if the site is revived.
- `app.js` is an unused AngularJS snippet and can be deleted.
- There's no license file in the repo.
