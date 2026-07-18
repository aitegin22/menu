# Plov House — site map & file guide

Read this first. It lists every file in the project, then walks through each
HTML page tag-by-tag so you can verify the whole site without opening a browser.

The site is **plain HTML + one CSS file**. There is **no JavaScript** and no
framework. Three pages, linked to each other through a shared top navigation.

```
menu/
├── index.html        Home page + the food menu
├── drinks.html       Drinks list
├── reserve.html      Reserve-a-table form
├── style.css         The one stylesheet, shared by all three pages
├── MENU.md           This file
└── images/
    ├── plov.png      Your real photo of plov (unchanged)
    ├── lagman.svg    Placeholder illustration for lagman — swap for a photo
    └── tea.svg       Placeholder illustration for green tea — swap for a photo
```

**About the images:** `plov.png` is your original photo, untouched. I only had
that one photo, so `lagman.svg` and `tea.svg` are simple hand-drawn placeholders
(plain shapes, no photo). Drop real photos in `images/` and update the `src`
attributes when you have them — the spots are marked below.

**Your original content, preserved:** the home page still says *"Plov House"*,
shows `images/plov.png`, and keeps your exact menu lines *"Plov — rice, carrots,
lamb. $12"* and *"Lagman — hand-pulled noodles. $10"*. The drinks page keeps
*"Green tea — by the pot. $3"* and the *"Back to the menu"* link. Everything
else is new scaffolding around that content.

---

## Shared building blocks (appear on all three pages)

Every page starts and ends the same way, so these are explained once here:

- `<!DOCTYPE html>` — declares the file as modern HTML5.
- `<html lang="en">` — root element; `lang="en"` tells browsers/readers the
  language is English.
- `<head>` — page metadata, not shown on the page itself:
  - `<meta charset="utf-8">` — character encoding, so accents/dashes render.
  - `<meta name="viewport" …>` — makes the layout scale correctly on phones.
  - `<title>` — the text shown in the browser tab.
  - `<link rel="stylesheet" href="style.css">` — pulls in the one stylesheet.
- `<body>` — everything visible on the page.
- `<header class="site-header">` — the maroon bar at the top, containing:
  - `<a class="brand" …>Plov House</a>` — restaurant name, links home.
  - `<nav class="site-nav">` — the three links: Menu, Drinks, Reserve. On each
    page, the link for the current page carries `class="current"` so the CSS can
    underline it.
- `<footer class="site-footer">` — the address / hours / phone line at the
  bottom. Identical on all three pages. (Details are placeholders — edit freely.)

---

## `index.html` — home page

The `<head>`, `<header>`, and `<footer>` are the shared blocks above. The unique
part is inside `<main>`:

- `<main>` — the centered content column (width capped by CSS).
- `<section class="hero">` — the top banner, image beside text:
  - `<img class="hero-photo" src="images/plov.png" alt="…">` — **your plov
    photo**. `alt` describes it for screen readers / if the image fails to load.
  - `<div class="hero-text">`
    - `<h1>Plov House</h1>` — the main page heading (your restaurant name).
    - `<p class="tagline">` — the italic one-line description.
    - `<a class="button" href="reserve.html">Reserve a table</a>` — a link
      styled as a button, sending visitors to the reservation page.
- `<section class="menu">` — the food menu:
  - `<h2>The Menu</h2>` — section heading.
  - `<ul class="dish-list">` — the list of dishes. Each dish is one `<li>`:
    - `<li class="dish">` #1 — **Plov**
      - `<img class="dish-photo" src="images/plov.png" …>` — thumbnail.
      - `<div class="dish-body">` → `<h3>Plov</h3>` + `<p class="dish-desc">`
        holding your line *"Plov — rice, carrots, lamb."*
      - `<span class="price">$12</span>` — your price, on the right.
    - `<li class="dish">` #2 — **Lagman**
      - `<img … src="images/lagman.svg" …>` — placeholder thumbnail (swap for a
        real photo).
      - `<h3>Lagman</h3>` + `<p>` with your line *"Lagman — hand-pulled
        noodles."* + `<span class="price">$10</span>`.
  - `<p class="menu-note">` — a sentence linking to the Drinks page.

---

## `drinks.html` — drinks list

Same shared blocks. Inside `<main>`:

- `<section class="menu">` — reuses the same menu styling as the home page.
  - `<h1>Drinks</h1>` — page heading (kept from your original page).
  - `<img class="banner-photo" src="images/tea.svg" …>` — a wide banner image
    (placeholder tea illustration; swap for a real photo).
  - `<ul class="dish-list">` — three drinks, each an `<li class="dish">`:
    - **Green tea** — `<h3>` + `<p>` with your original line *"Green tea — by
      the pot."* + `<span class="price">$3</span>`. (No image on these rows, so
      the text sits flush left — that's intentional.)
    - **Ayran** — *"chilled salted yogurt drink."* + `$4` (new item).
    - **Compote** — *"house-brewed dried fruit."* + `$3` (new item).
  - `<p class="menu-note">` → `<a href="index.html">Back to the menu</a>` — your
    original back-link, kept.

---

## `reserve.html` — reserve-a-table form

Same shared blocks. Inside `<main>`:

- `<section class="reserve">`
  - `<h1>Reserve a table</h1>` — page heading.
  - `<p class="reserve-intro">` — explains what submitting does (see below).
  - `<form class="reserve-form" action="mailto:reservations@plovhouse.example"
    method="post" enctype="text/plain">` — the form.
    - **How it works, and why there's no JavaScript:** a bare HTML site has no
      server to receive a submission, so the form uses `action="mailto:…"`.
      Pressing the button opens the visitor's own email app with the field
      values filled in; they hit send, and it arrives as an email. This needs
      **zero JavaScript**. Replace the `mailto:` address with your real inbox.
      When you later add a booking backend, change `action` to that URL — the
      fields below already send the right data.
    - Each field is a `<p class="field">` wrapping a `<label>` + an input. The
      `for` on each label matches the input's `id`, so tapping the label focuses
      the field. Native browser validation (no script) is done via attributes:
      - **Name** — `<input type="text" required>` — must be filled in.
      - **Email** — `<input type="email" required>` — must look like an email.
      - **Phone** — `<input type="tel">` — optional; brings up a phone keypad on
        mobile.
      - **Date** — `<input type="date" required>` — native date picker.
      - **Time** — `<input type="time" required min="12:00" max="22:00">` —
        native time picker, limited to opening hours.
      - **Party size** — `<input type="number" required min="1" max="12"
        value="2">` — 1 to 12 guests, defaults to 2.
      - **Notes** — `<textarea>` — optional free text (high chair, allergies…).
    - `<button class="button" type="submit">Request table</button>` — submits
      the form. `required` fields block submission until they're valid, shown by
      the browser itself — again, no JavaScript.

---

## `style.css` — the one stylesheet

Shared by all three pages via the `<link>` in each `<head>`. It's organized into
numbered sections (see the comments at the top of the file):

1. **Base** — page font (a serif), colors, the centered `main` column.
2. **Header + navigation** — the maroon top bar, brand, and nav links; the
   `.current` class underlines the active page's link.
3. **Buttons** — the shared `.button` style used by the "Reserve a table" link
   and the form's submit button.
4. **Home** — the `.hero` layout and the `.dish-list` / `.dish` menu rows.
5. **Drinks** — the `.banner-photo` (drinks pages reuse the menu styles).
6. **Reserve** — the `.field` label-over-input form layout and focus outlines.
7. **Footer** — the centered bottom line.
8. **Small screens** — a `@media` block so the hero image and dish rows stack
   neatly on narrow phones.

There are no other CSS or JavaScript files — this is the whole site.
