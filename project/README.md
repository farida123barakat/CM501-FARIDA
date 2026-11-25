# Discover Egypt

**A thousand stories. One destination.**

A travel guide for first-time visitors to Egypt: where to go, what to eat and how to travel with confidence.
Student project for **CM-501 Frontend Web Development** (MUDT, Winter 2026). Not an official website of the Ministry of Tourism and Antiquities.

---

## Pages

| Page | File | Status |
| --- | --- | --- |
| Home | `index.html` | EPA 3 Part B |
| Style guide | `styleguide.html` | EPA 3 Part A |
| Discover | `discover.html` | placeholder, built later |
| Plan | `plan.html` | placeholder, built later |
| Experience | `experience.html` | placeholder, built later |
| Travel smart | `travel-smart.html` | placeholder, built later |
| Community | `community.html` | placeholder, built later |
| My Egypt | `my-egypt.html` | placeholder, built later |

## Planned features

| Section | Features |
| --- | --- |
| **Discover** | Find Your Egypt quiz, interactive map, destination pages, Walk Through Time timeline, Golden Hour Finder, weather and crowd chart, events calendar, Ramadan guide, Watch & Discover films, bucket list |
| **Plan** | Smart Trip Builder, budget calculator, itinerary PDF, currency converter, packing checklist, suggested routes, preparation guide |
| **Experience** | Memory Hunt, postcards, memory album, Memory Passport, print partners, Hieroglyphics Explorer, Taste Egypt by region, recipes, Speak a little Egyptian, culture and etiquette, Egypt Through the Senses |
| **Travel Smart** | Emergency numbers and embassies, Cairo Metro guide, walking routes, solo women guide, accessibility guide, fair price guide |
| **Community and My Egypt** | Ask a Local, traveller stories, My Egypt, travel passport stamps, visitor accounts |
| **Admin** | Moderation, price editor, event manager, featured destinations, recipe review, bucket list manager, film manager, print partners and print queue |
| **Site-wide** | Search, proverb of the day, accessibility controls, mobile layout, security, contact form, newsletter, privacy, credits and sources pages |

## Design

Discover Egypt is for first-time visitors who feel a little unsure about travelling to Egypt, and it should feel like a calm travel magazine at golden hour: warm photos, an elegant serif (Fraunces) for headlines and a readable sans-serif (Inter) for text.
All colours, font sizes and spaces are tokens in `css/tokens.css`, and every colour token has a light and a dark value through `light-dark()`, so the site follows the visitor's system theme.
Gold is used as a spotlight, not a paint bucket: it marks only the one main action on the hero photo, and text on the photo always sits on an 85 % dark layer so it stays readable (at least 11 : 1).
The layout is mobile first with Grid for the page and Flexbox inside components, two breakpoints in rem (40rem for two cards per row, 64rem for three) and a container query that turns the dish card sideways when its own box is at least 30rem wide.
Headings are fluid with `clamp()`, and paragraphs stop at 65 characters per line.
I tested the pages at 320, 768, 1280 and 1920 px and at 400 % zoom with no horizontal scrolling, checked every colour pair with the WCAG contrast formula, and ran the axe accessibility checker in light and dark mode with 0 violations.
AI use: I used Claude (AI) to help me shape my ideas, understand my own vision for the site and add features to it.
