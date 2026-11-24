# Accessibility test protocol — EPA 2, Campus Café

Course: CM-501 · Pages tested: `menu.html`, `contact.html` · Target: WCAG 2.2 AA

---

## C1 · Issue list, before → after

### menu.html

| # | Problem (before) | WCAG SC | Fix (after) |
|---|---|---|---|
| 1 | Page frame missing: no `<!DOCTYPE html>`, no page language, no viewport meta, and the title read "Home" | 3.1.1 Language of Page, 2.4.2 Page Titled, 1.4.10 Reflow (+ valid markup, R05) | `<!DOCTYPE html>`, `<html lang="en">`, `<meta name="viewport" …>`, title `Menu – Campus Café` |
| 2 | Navigation was `<div onclick="location.href=…">` — not focusable, no link role | 2.1.1 Keyboard, 4.1.2 Name/Role/Value | `<nav>` with a `<ul>` of real `<a>` elements, `aria-current="page"` on the current one |
| 3 | No landmarks; the whole page was nested `<div>`s | 1.3.1 Info and Relationships | `<header>`, `<nav>`, `<main>`, `<footer>` |
| 4 | No way to bypass the header links | 2.4.1 Bypass Blocks | Skip link to `#main`, visible on focus |
| 5 | Heading order jumped `h1` → `h4` | 1.3.1 Info and Relationships | `h1` "Menu", `h2` per section |
| 6 | Images: neither image had an `alt` attribute, and Today's special existed **only** as grey text baked into `special.jpg` | 1.1.1 Non-text Content, 1.4.5 Images of Text | Special written out as text (name, price, "only until 4 pm"); `alt=""` on both images, which are now decorative |
| 7 | Menu items were `<div>` + `<b>` + `<i>`, not a list | 1.3.1 Info and Relationships | `<ul class="menu-list">`; a screen reader announces "list, 4 items" |
| 8 | `<table class="layout">` used purely to make three columns | 1.3.1 Info and Relationships | Removed; three `<section>` elements in a CSS flex row |
| 9 | `<font color>` and inline `style` for colour and weight | — (R05, separation of concerns) | All presentation moved to `before.css` |
| 10 | Five text colours below 4.5 : 1 — prices `#d6d6d6` on white **1.45**, body `#b3b3b3` **2.1**, headings `#d9c6b4` **1.66**, nav `#8a6d5a` on `#3b2a20` **2.87**, footer `#6b4a36` on `#3b2a20` **1.73** | 1.4.3 Contrast (Minimum) | Prices `#3f3f3f` **10.5**, body `#4a4a4a` **8.9**, headings `#5a3a26` **10.2**, nav and footer `#f1e6dc` on `#3b2a20` **11.1** |
| 11 | `* { outline: none !important }` killed every focus indicator | 2.4.7 Focus Visible | Rule deleted; `:focus-visible` outline 3 px `#b45309` (5 : 1 on white), light `#ffd9a8` on the dark bars |
| 12 | Social icon links held only an `<svg>` — announced as "link" with no name | 2.4.4 Link Purpose, 1.1.1 | Visible text "Campus Café on Facebook" / "…on Instagram"; `<svg aria-hidden="true" focusable="false">` |
| 13 | Base text 13 px at `font-weight: 200` | 1.4.4 Resize Text (supporting) | 16 px, weight 400, `line-height: 1.5` |

### contact.html

| # | Problem (before) | WCAG SC | Fix (after) |
|---|---|---|---|
| 14 | Same page frame and navigation problems as the menu page: no DOCTYPE, `lang` or viewport, title "Home", `onclick` nav, no landmarks, no skip link | 3.1.1, 2.4.2, 1.4.10, 2.1.1, 1.3.1, 2.4.1 | Same fixes as rows 1–4; title `Contact – Campus Café` |
| 15 | Phone number and e-mail existed **only** inside `contact.png` | 1.1.1, 1.4.5 Images of Text | `<address>` with the text, plus `tel:+498900000000` and `mailto:` links; the image removed |
| 16 | Google Maps `<iframe>` with no `title` and no fallback | 4.1.2 Name/Role/Value, 2.4.1 | Replaced with a plain link to the address on OpenStreetMap — this also stops a third-party map loading, and setting cookies, before the visitor asks for it |
| 17 | Form structure: fields had `placeholder` text instead of `<label>`, so the hint vanishes as soon as you type, and "Newsletter & reservations" was a styled `<div>` | 1.3.1 Info and Relationships, 3.3.2 Labels or Instructions, 4.1.2 | A real `<label for="…">` per field, placeholders removed; the section heading is an `<h2>`, referenced by the form's `aria-labelledby` |
| 18 | Every field was `type="text"` — including e-mail, phone and birthday — and no field had `autocomplete` | 1.3.5 Identify Input Purpose, 3.3.2 | `type="email"`, `type="tel"`, `type="date"`; `autocomplete="name" / "email" / "tel" / "bday"` |
| 19 | Required fields were not marked in any way | 3.3.2 Labels or Instructions | `required`, plus a visible `*` explained once above the form; optional fields say so in a hint tied to the field with `aria-describedby` |
| 20 | Submit control was `<div class="btn2" onclick="…submit()">` — not focusable, not a button | 2.1.1 Keyboard, 4.1.2 | `<button type="submit">` |
| 21 | `method="get"` put name, e-mail, phone and birthday into the URL | — (privacy; data minimisation) | `method="post"` |
| 22 | Form colours below threshold: input text `#bbb` and placeholder `#ddd` on white, button text `#999` on white **2.8 : 1** with a dotted 1 px border | 1.4.3 Contrast (Minimum), 1.4.11 Non-text Contrast | Input text `#333`, border `#767676`, hint text `#595959` **7 : 1**; solid `#5a3a26` button with white text **10.2 : 1** |

**Total: 22 issues over both pages** (the brief asks for at least 12). Several rows group
problems that share one cause, such as the page frame or the contrast failures.

---

## C2 · Automated tests

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


---

## C3 · Manual tests

### Keyboard walkthrough

Test with <kbd>Tab</kbd>, <kbd>Shift</kbd>+<kbd>Tab</kbd> and <kbd>Enter</kbd> only — mouse untouched.

**menu.html**

| Step | Expected | Actual | Pass? |
|---|---|---|---|
| 1 | First <kbd>Tab</kbd> reveals "Skip to main content" | Yes, it appears at the top left | Pass |
| 2 | <kbd>Enter</kbd> on the skip link moves focus past the header | Yes, the address gains `#main` and the next Tab lands in the footer, so the navigation is skipped | Pass |
| 3 | Tab order: skip link → Menu → Contact → Facebook → Instagram | Yes, in that order | Pass |
| 4 | Focus outline clearly visible on every stop, on the dark bars too | Yes, light outline on the brown header and footer, orange on white | Pass |
| 5 | Nothing focusable is skipped or trapped | Yes | Pass |

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

Both keyboard walkthroughs were run in Chrome on macOS.

### Screen-reader test (accessibility tree)

Tool used: **Chrome DevTools accessibility tree**, inspected on the live pages.
The tree is the information a screen reader reads out. It shows each element's
role, name and state. No screen reader was run for this table; a VoiceOver run
is still outstanding.

| Task | What the accessibility tree shows | Result |
|---|---|---|
| menu.html: which landmarks are there? | banner, navigation "Main", main, contentinfo | Pass |
| Is the heading order h1 → h2 logical? | h1 Menu, then h2 Today's special, Coffee, Tea & more, Food | Pass |
| Is the "Today's special" section real text? | Static text with name, price and time; the image is ignored (`alt=""`) | Pass |
| Is the Coffee section a list with 4 items? | Role list with four list items | Pass |
| Do the footer links have meaningful names? | Link "Campus Café on Facebook" / link "Campus Café on Instagram" | Pass |
| contact.html: does each form field have a label? | Every field has its label as its name: Name, E-mail, Birthday, Phone, Message | Pass |
| Is the e-mail field required, with its hint? | State required; description = the hint text (via `aria-describedby`) | Pass |
| Is the Send control a button? | Role button, name "Send" | Pass |

### Zoom 200 %

| Page | Browser zoom 200 % — any loss of content or function? | Notes |
|---|---|---|
| menu.html | No text is lost and nothing overlaps; all content stays readable. Because of the fixed 1100 px wrapper the page needs horizontal scrolling at this width. | Reflow (1.4.10) is not met; the brief places responsive layout in EPA 3. |
| contact.html | Same: labels, hints and fields stay readable and in order, with horizontal scrolling needed. | As above. |

> The pages keep the starter kit's fixed `#wrap { width: 1100px }`, so at 200 % zoom on a
> narrow window a horizontal scrollbar appears. Responsive layout is EPA 3, so this is
> recorded here rather than fixed.

---

## C4 · Peer test (Session 4)

Peer tester: ____________ Date: ____________

**Not yet carried out** — to be completed in the Session 4 peer-testing slot.

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

I used AI to ask about things I did not understand, to advise me whether what I had done
was right or not, and to check whether I was missing something.
