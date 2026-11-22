# Accessibility test protocol — EPA 2, Campus Café

Course: CM-501 · Pages tested: `menu.html`, `contact.html` · Target: WCAG 2.2 AA

> **Status:** C1 and C5 are complete. C2, C3 and C4 contain the test plan with
> empty result columns — fill them in from your own test runs (see the run
> instructions under each section).

---

## C1 · Issue list, before → after

### menu.html

| # | Problem (before) | WCAG SC | Fix (after) |
|---|---|---|---|
| 1 | No `<!DOCTYPE html>`, so the browser renders in quirks mode | — (valid markup, R05) | Added `<!DOCTYPE html>` |
| 2 | No page language | 3.1.1 Language of Page | `<html lang="en">` |
| 3 | Title was "Home" on the menu page | 2.4.2 Page Titled | `Menu – Campus Café` |
| 4 | No viewport meta; page cannot reflow or be zoomed sensibly on small screens | 1.4.10 Reflow | Added `<meta name="viewport" content="width=device-width, initial-scale=1">` |
| 5 | Navigation was `<div onclick="location.href=…">` — not focusable, not a link to assistive tech | 2.1.1 Keyboard, 4.1.2 Name/Role/Value | `<nav>` with a `<ul>` of real `<a>` elements, `aria-current="page"` on the current one |
| 6 | No landmarks; the whole page was nested `<div>`s | 1.3.1 Info and Relationships | `<header>`, `<nav>`, `<main>`, `<footer>` |
| 7 | No way to bypass the header links | 2.4.1 Bypass Blocks | Skip link to `#main`, visible on focus |
| 8 | Heading order jumped `h1` → `h4` | 1.3.1 Info and Relationships | `h1` "Menu", `h2` per section |
| 9 | Today's special existed **only** inside `special.jpg` | 1.1.1 Non-text Content, 1.4.5 Images of Text | Special written as text (name, price, "only until 4 pm"); image now decorative |
| 10 | Both images had no `alt` attribute at all | 1.1.1 Non-text Content | `alt=""` on both — the special's content is now real text next to it, and the latte photo carries no information |
| 11 | Menu items were `<div>` + `<b>` + `<i>`, not a list | 1.3.1 Info and Relationships | `<ul class="menu-list">`; a screen reader now announces "list, 4 items" |
| 12 | `<table class="layout">` used purely for three columns | 1.3.1 Info and Relationships | Removed; three `<section>` elements in a CSS flex row |
| 13 | `<font color>` and inline `style` for colour and weight | — (R05, separation of concerns) | All presentation moved to `before.css` |
| 14 | Prices `#d6d6d6` on white = **1.45 : 1** | 1.4.3 Contrast (Minimum) | `#3f3f3f` = **10.5 : 1** |
| 15 | Body text `#b3b3b3` on white = **2.1 : 1** | 1.4.3 Contrast (Minimum) | `#4a4a4a` = **8.9 : 1** |
| 16 | Headings `#d9c6b4` on white = **1.66 : 1** | 1.4.3 Contrast (Minimum) | `#5a3a26` = **10.2 : 1** |
| 17 | Nav text `#8a6d5a` on `#3b2a20` = **2.87 : 1** | 1.4.3 Contrast (Minimum) | `#f1e6dc` = **11.1 : 1** |
| 18 | Footer text `#6b4a36` on `#3b2a20` = **1.73 : 1** | 1.4.3 Contrast (Minimum) | `#f1e6dc` = **11.1 : 1** |
| 19 | `* { outline: none !important }` killed every focus indicator | 2.4.7 Focus Visible, 2.4.11 Focus Not Obscured | Rule deleted; `:focus-visible` outline 3 px `#b45309` (5 : 1 against white), light `#ffd9a8` on the dark bars |
| 20 | Social icon links contained only an `<svg>` — announced as "link" with no name | 2.4.4 Link Purpose, 1.1.1 | Visible text "Campus Café on Facebook" / "…on Instagram"; `<svg aria-hidden="true" focusable="false">` |
| 21 | Base text 13 px at `font-weight: 200` | 1.4.4 Resize Text (supporting) | 16 px, weight 400, `line-height: 1.5` |

### contact.html

| # | Problem (before) | WCAG SC | Fix (after) |
|---|---|---|---|
| 22 | Same missing DOCTYPE, `lang`, viewport; title again "Home" | 3.1.1, 2.4.2, 1.4.10 | Same fixes as rows 1–4; title `Contact – Campus Café` |
| 23 | Same `onclick` navigation, no landmarks, no skip link | 2.1.1, 1.3.1, 2.4.1 | Same header, `<main>`, `<footer>` and skip link as the menu page |
| 24 | Phone number and e-mail existed **only** inside `contact.png` | 1.1.1, 1.4.5 Images of Text | `<address>` with the text, `tel:+498900000000` and `mailto:` links; image removed |
| 25 | Google Maps `<iframe>` with no `title`, no fallback | 4.1.2 Name/Role/Value, 2.4.1 | Replaced with a plain link to the address on OpenStreetMap — also stops a third-party map loading (and setting cookies) before the visitor asks for it |
| 26 | Form fields had `placeholder` text instead of `<label>`; the hint disappears as soon as you type | 1.3.1, 3.3.2 Labels or Instructions, 4.1.2 | A real `<label for="…">` per field; placeholders removed |
| 27 | Every field was `type="text"`, including e-mail, phone and birthday | 1.3.5 Identify Input Purpose, 3.3.2 | `type="email"`, `type="tel"`, `type="date"` — correct keyboard on mobile and native validation |
| 28 | No `autocomplete` attributes | 1.3.5 Identify Input Purpose | `autocomplete="name" / "email" / "tel" / "bday"` |
| 29 | Required fields not marked in any way | 3.3.2 Labels or Instructions | `required` plus a visible `*` explained once above the form; optional fields say so in a hint linked with `aria-describedby` |
| 30 | Submit control was `<div class="btn2" onclick="…submit()">` — not focusable, not a button | 2.1.1 Keyboard, 4.1.2 | `<button type="submit">` |
| 31 | `method="get"` put name, e-mail, phone and birthday into the URL | — (privacy; data minimisation) | `method="post"` |
| 32 | `<div class="h">` used as the form's section heading | 1.3.1 Info and Relationships | `<h2>`, referenced by the form's `aria-labelledby` |
| 33 | Input text `#bbb` and placeholder `#ddd` on white | 1.4.3 Contrast (Minimum) | Input text `#333`, border `#767676`, hint text `#595959` = 7 : 1 |
| 34 | Button `.btn2` `#999` on white = **2.8 : 1**, dotted 1 px border | 1.4.3, 1.4.11 Non-text Contrast | Solid `#5a3a26` button, white text = **10.2 : 1** |

**Total: 34 issues over both pages** (requirement: at least 12).

---

## C2 · Automated tests

### How to run these

1. **Publish first.** GitHub → repo → Settings → Pages → Source: *Deploy from a branch*,
   branch `main`, folder `/ (root)`. Wait for the green check, then note the URL:
   `https://farida123barakat.github.io/CM501-FARIDA/epa2-campus-cafe/menu.html`
2. **W3C validator** — <https://validator.w3.org/nu/> → *Check by address* → paste the page URL.
   (A local run of `npx html-validate menu.html contact.html` is already clean: **0 errors**.
   The Nu validator is the one the brief asks for, so run that too and screenshot it.)
3. **Lighthouse** — Chrome DevTools → *Lighthouse* tab → category *Accessibility* only → *Analyze page load*.
4. **WAVE** — <https://wave.webaim.org/> → paste the page URL. Record Errors / Contrast Errors / Alerts.
5. Screenshot each result and save it in `screenshots/` using the names in the table below.

### Results

| Tool | Page | Before | After | Screenshot |
|---|---|---|---|---|
| W3C Nu validator (errors) | menu.html | 14 (+1 warning) | 0 (no warnings) | `screenshots/validator-menu-before-summary.jpg`, `validator-menu-before-details.jpg` / `validator-menu-after.png` |
| W3C Nu validator (errors) | contact.html | 2 (+1 warning) | 0 (no warnings) | `screenshots/validator-contact-before-details.png`, `validator-contact-before-end.png` / `validator-contact-after.png` |
| Lighthouse accessibility score | menu.html | 46 | 100 | `screenshots/lighthouse-menu-before.jpg` / `lighthouse-menu-after.png` |
| Lighthouse accessibility score | contact.html | 47 | 100 | `screenshots/lighthouse-contact-before.png` / `lighthouse-contact-after.png` |
| WAVE errors | menu.html | 5 | 0 | `screenshots/wave-menu-before.jpg` / `wave-menu-after.jpg` |
| WAVE contrast errors | menu.html | 38 | 0 | (same screenshot) |
| WAVE alerts | menu.html | 5 | 1 | (same screenshot) |
| WAVE AIM score | menu.html | 3.6 | 10 | (same screenshot) |
| WAVE errors | contact.html | 9 | 0 | `screenshots/wave-contact-before.png` / `wave-contact-after.jpg` |
| WAVE contrast errors | contact.html | 3 | 0 | (same screenshot) |
| WAVE alerts | contact.html | 4 | 1 | (same screenshot) |
| WAVE AIM score | contact.html | 5.4 | 10 | (same screenshot) |

The one remaining alert on each page is WAVE's "possible heading" notice on the
logo paragraph; it is a suggestion, not an error.

> For the *before* column, check out the first commit in a second folder and run the
> tools against it locally (WAVE has a browser extension that works on `file://` and
> `localhost`; Lighthouse works on `localhost` — `npx serve .`):
> `git worktree add ../epa2-before <first-commit-sha>`

---

## C3 · Manual tests

### Keyboard walkthrough

Test with <kbd>Tab</kbd>, <kbd>Shift</kbd>+<kbd>Tab</kbd> and <kbd>Enter</kbd> only — mouse untouched.

**menu.html**

| Step | Expected | Actual | Pass? |
|---|---|---|---|
| 1 | First <kbd>Tab</kbd> reveals "Skip to main content" | | |
| 2 | <kbd>Enter</kbd> on the skip link moves focus past the header | | |
| 3 | Tab order: skip link → Menu → Contact → Facebook → Instagram | | |
| 4 | Focus outline clearly visible on every stop, on the dark bars too | | |
| 5 | Nothing focusable is skipped or trapped | | |

**contact.html**

| Step | Expected | Actual | Pass? |
|---|---|---|---|
| 6 | Tab reaches every form field in visual order | Yes | Pass |
| 7 | Clicking a label moves focus into its field | Yes | Pass |
| 8 | Submitting an empty form reports the missing required fields | Yes, the browser asks for the required fields | Pass |
| 9 | <kbd>Enter</kbd> in a text field submits the form | Yes | Pass |
| 10 | The Send button is reachable and operable by keyboard | Yes | Pass |

> Note on the environment: on macOS, <kbd>Tab</kbd> reaches only text fields until
> **Keyboard navigation** is switched on in System Settings → Keyboard. With that setting
> off, links and buttons are skipped. This is an operating-system setting, not a defect of
> the page; the test above was run with it switched on.

### Screen-reader test

Screen reader used: ____________ (e.g. NVDA 2024.x + Firefox, or VoiceOver + Safari)

| Task | What was announced | Result |
|---|---|---|
| Open menu.html and list the landmarks (NVDA: <kbd>D</kbd>) | | |
| List the headings (<kbd>H</kbd>) — is the order h1 → h2 logical? | | |
| Read the "Today's special" section | | |
| Enter the Coffee list — is it announced as "list, 4 items"? | | |
| Tab to the footer links — is the link name meaningful? | | |
| On contact.html, tab through the form — is each field's label read out? | | |
| Is the e-mail field announced as required, with its hint? | | |
| Is the Send control announced as a button? | | |

### Zoom 200 %

| Page | Browser zoom 200 % — any loss of content or function? | Notes |
|---|---|---|
| menu.html | | |
| contact.html | | |

> Honest note for this section: the pages still use the fixed `#wrap { width: 1100px }`
> from the starter kit, so at 200 % zoom on a narrow window a horizontal scrollbar
> appears. The brief says responsive layout is EPA 3, so record what you see rather
> than fixing it here.

---

## C4 · Peer test (Session 4)

Peer tester: ____________ Date: ____________

The blank sheet your tester fills in is `peer-test/peer-test-sheet.md`.
Transfer their findings here afterwards.

| # | What the peer tester found | Page | WCAG SC | What I changed | Commit |
|---|---|---|---|---|---|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |

**What I found when testing their pages:** ____________

---

## C5 · Limits of automated testing

Automated tools check what a machine can see in the markup: a missing `alt`, a colour
pair below the contrast threshold, a form control with no label. They cannot judge
whether what is there is *right*. Three things in these pages show the gap. First,
`alt=""` on `special.jpg` and `latte.jpg` passes every checker — but so would a wrong
`alt="image"`; only a person who knows that the special's text now sits next to the
image can say the empty alt is the correct choice. Second, before the repair,
`special.jpg` would have passed a contrast check with full marks, because the tool
measures CSS colours and cannot read the grey text baked into the JPEG — an image of
text (1.4.5) is close to invisible to automated testing. Third, a tool can confirm that
the two footer links have names, but not that "Campus Café on Facebook" is a *useful*
name, nor that the tab order through the form still matches the visual order. That is
why a 100 Lighthouse score is not proof of accessibility: it means no machine-detectable
failure was found, not that the page works for someone using a screen reader.

---

## AI use

I used Claude to explain WCAG success criteria, to review my markup, and to draft the
repairs to `menu.html` and `contact.html`, which I then went through change by change
so I can explain every one of them; the test runs, their screenshots and the peer test
are my own.

> Adjust that sentence so it matches what you actually did — it has to be true, and
> you have to be able to back it up in the oral.
