# Claude Code Brief — VCC Phase 1 Rollout
**Date:** May 2026  
**Repo:** voodoo-clam-clan (private GitHub)  
**Files to touch:** `index.html` only (single-file site, no build step)  
**Deployment:** Netlify drag-and-drop when ready — do NOT auto-deploy  

---

## Context

The site is being sent to the girls in phases. Phase 1 = commitment round. We need their Airbnb decision, t-shirt size, and activity preferences before we finalize anything. The full site (itinerary, looks, budget, rules) is built but hidden for now.

---

## Task 1 — Add phase flag + show/hide logic

At the very top of the `<script>` block (before any other JS), add:

```js
var PHASE = 1; // 1 = commitment round · 3 = full site
```

Then wrap each section with a class that targets it:

**HIDE in Phase 1** (add `class="phase-3-only"` to the `<section>` or wrapping `<div>`):
- `#itinerary`
- `#looks`
- `#pack`
- `#playlist`
- `#album`
- `#rules`
- `#budget`
- `#kassie` (if it exists as standalone section)

**SHOW in Phase 1** (always visible):
- `#hero` — keep as-is, including countdown
- `#map` — keep
- `#poll` — new section (see Task 2)
- `#airbnb` — new section (see Task 3)
- `#pay` — keep
- `#form` — keep (link to form.html)
- footer

Add this CSS:

```css
.phase-3-only { display: none; }
```

And this JS after the `var PHASE` declaration:

```js
if (PHASE >= 3) {
  document.querySelectorAll('.phase-3-only').forEach(function(el) {
    el.style.display = '';
  });
}
```

Also update the nav links — in Phase 1 only show: Map · Poll · Pay · Form. Hide the rest with the same phase class approach.

**To launch Phase 3:** change `var PHASE = 1` to `var PHASE = 3` and redeploy. Everything unhides. No other changes needed.

---

## Task 2 — Build the Activity Poll section

Add a new `<section id="poll">` between `#map` and `#pay`. This replaces the Google Form poll approach — it's built directly into the page, results collected via the existing Formspree endpoint on form.html, or a simple mailto. See approach below.

### Section header

```
eyebrow: "Cast Your Vote"
title: "Help Us Plan the Weekend"
subhead (Cormorant Garamond italic): "Kassie has weighed in. Now it's your turn. Pick your favorites — the top votes win."
```

### Poll structure — 4 category groups

Each group has:
- A category label (Cinzel, teal, uppercase)
- A short instruction line
- Option cards (multi-select checkboxes, styled like the existing `.b-mrow` pattern)
- A "No preference — I'm down for anything" option at the bottom of each group

**Important:** Options Kassie ranked in her top 4 get a `🦪 Kassie's Pick` badge (pink tag, same style as `.b-tk`). Do not say "Kassie ranked #X" — just badge it.

---

#### Group 1 — Experiences & Activities

Label: `Experiences`  
Instruction: `Select everything you'd want to do — we'll go with what the group wants.`

Options (in this order — Kassie picks first):

| Option | Price | Kassie badge |
|---|---|---|
| Drag Brunch — The Country Club (Sunday 1pm) | ~$65pp | YES |
| Private tea leaf reading — Bottom of the Cup (Monday) | ~$35pp | YES |
| Ghost, Crime, Voodoo & Vampire Tour — VIP HELLVISION (Monday 8pm, walking tour) | ~$44pp | YES |
| Airboat swamp tour + gator feeding (Monday morning) | ~$67pp | NO |
| Ghost bar crawl (Monday evening — alternative to walking tour) | ~$25–40pp | NO |
| Spa morning — Spa Isbell, Magazine St (Sunday or Monday) | ~$100pp | NO |
| The Sazerac House — cocktail museum (any afternoon, free) | Free | NO |
| No preference — I'm down for anything | — | NO |

Note in the section (small, pearl-dim): `Drag brunch is Sunday only. Ghost tour options: pick one — walking tour OR bar crawl, not both.`

---

#### Group 2 — Food & Restaurants

Label: `Dinners & Meals`  
Instruction: `We'll use these votes to book. Pick as many as appeal to you.`

Sub-label: `Saturday Night` (gold, small Cinzel)

| Option | Price | Kassie badge |
|---|---|---|
| French Quarter bar crawl + street food (meet the boys) | ~$35pp | NO |
| Arnaud's — white tablecloth French Creole | ~$100pp | NO |
| No preference | — | NO |

Sub-label: `Sunday`

| Option | Price | Kassie badge |
|---|---|---|
| Drag brunch covers Sunday morning (if voted above) | — | — |
| The Rum House — Caribbean-Mexican, walkable | ~$30pp | NO |
| Pêche Seafood Grill — James Beard winner | ~$60pp | NO |
| Gris-Gris — upscale Southern Creole | ~$70pp | NO |
| No preference | — | NO |

Sub-label: `Monday Night`

| Option | Price | Kassie badge |
|---|---|---|
| Muriel's Jackson Square — haunted restaurant, steps from ghost tour | ~$95pp | NO |
| Café Amélie — candlelit courtyard | ~$65pp | NO |
| Compère Lapin — Michelin, Caribbean Creole | ~$65pp | NO |
| No preference | — | NO |

---

#### Group 3 — Nightlife & Music

Label: `Nightlife`  
Instruction: `What sounds good for going out?`

| Option | Price | Kassie badge |
|---|---|---|
| Oz New Orleans + Café Lafitte in Exile — Bourbon St clubs (Sunday) | ~$20pp drinks | NO |
| Spotted Cat Music Club — best jazz on Frenchmen St (any night) | No cover | YES |
| Bayou Bar — Pontchartrain Hotel, live jazz nightcap (Monday) | ~$25pp drinks | NO |
| Frenchmen Street bar hop — live jazz, no cover (any night) | ~$30pp + Uber | NO |
| No preference — surprise me | — | NO |

---

#### Group 4 — Pace & Vibe

Label: `Vibe Check`  
Instruction: `Help us get the energy right.`

Single-select (radio), not multi:

| Option |
|---|
| Go hard — every night, full send |
| Mix it up — one big night, one chill night |
| Keep it manageable — good food, good company, early-ish nights |
| I'll follow the group's lead |

---

### Poll submission

The poll is NOT a form submit — it's **read-only display on the page** plus a link to form.html where they do the actual submission. The poll section ends with:

```
[CTA button — teal, pill shape]: "Submit Your Votes in the Form →" → links to form.html
```

The votes are captured in form.html (already has the activity vote fields). The poll on index.html is purely visual/UX — it helps them think through their choices before they open the form. You do not need to wire up any JS state sync between the two pages.

---

## Task 3 — Add Airbnb commitment section

Add `<section id="airbnb">` between `#hero` and `#map`.

### Content

```
eyebrow: "The House"
title: "2012 Oretha Castle Haley Blvd"
```

Two-column layout (stack on mobile):

**Left:** Key facts card (teal-faint border)
- Private pool · teal mural wall · outdoor dining
- 4 nights · Oct 3 check-in 3pm · Oct 6 checkout 11am
- Hosted by Samuel on Airbnb
- $3,066 total → **$341/person** at 9 girls

**Right:** Deadline card (pink-dim border, urgent styling)
```
eyebrow (pink): "⚠ Confirm by July 1"
body: "We need to know if you're in before we can lock this. If 3 or more girls drop, we'll need to find an alternative — and all the good places in New Orleans book months out. Please confirm in the form below."
```

Below both columns, a single teal CTA button:
```
"Confirm Your Spot in the Form →" → links to form.html
```

Do not embed a Google Maps iframe here — the map section already covers it.

---

## Task 4 — Update nav for Phase 1

In Phase 1 the nav should only show links to sections that exist and are visible. Update the nav link list:

**Phase 1 nav:** Map · Poll · Airbnb · Pay · Form

The bottom sticky nav (`#bot-nav`) should also only show Phase 1 links. Apply the same `phase-3-only` class to the hidden nav items.

---

## Task 5 — Add July 1 deadline banner

Directly below the hero (above `#airbnb`), add a slim full-width banner:

```
background: rgba(212,83,126,0.12)
border-bottom: 0.5px solid rgba(212,83,126,0.3)
text: "🗓 Airbnb confirmation deadline: July 1 · Submit the form to lock your spot"
font: Cinzel, 11px, letter-spacing 0.15em, pink color
padding: 10px 24px
text-align: center
```

No section wrapper — just a `<div class="deadline-banner">` between the hero div and the first section.

---

## What NOT to touch

- `form.html` — leave completely alone
- Any existing JS logic in the budget tracker
- The countdown timer
- The weather widget
- The Spotify player
- The lightbox
- Any CSS variables or the design system

---

## Testing checklist before deploy

- [ ] `var PHASE = 1` → itinerary, looks, pack, playlist, album, rules, budget all hidden
- [ ] `var PHASE = 3` → everything shows, nothing broken
- [ ] Poll section renders correctly on mobile (375px)
- [ ] Airbnb section stacks correctly on mobile
- [ ] Deadline banner visible immediately on load
- [ ] Nav only shows Phase 1 links in Phase 1
- [ ] "Submit Your Votes in the Form →" button opens form.html
- [ ] "Confirm Your Spot in the Form →" button opens form.html
- [ ] No JS errors in console

---

## Deployment reminder

Do NOT connect GitHub to Netlify auto-deploy. When Phase 1 is ready:
1. Drag `index.html` to Netlify drop
2. Get the URL
3. Send to girls with the July 1 deadline message

When Phase 3 is ready:
1. Change `var PHASE = 1` → `var PHASE = 3`
2. Drag-and-drop again
