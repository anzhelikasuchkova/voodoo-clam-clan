# Voodoo Clam Clan — Claude Code Handover
**Project:** Kassie's Bachelorette Planning Website  
**Date:** May 2026  
**Brainstorming chat:** Continue in Claude.ai  
**Deployment & dev:** Continue in Claude Code  

---

## Project Overview

A bachelorette planning hub website for "Voodoo Clam Clan" — Kassie's bachelorette party in New Orleans, October 3–6, 2026. 8–10 girls. MOH is the primary user of this codebase.

**Live site (temporary):** https://unrivaled-praline-9a49ae.netlify.app  
**Primary file:** `index.html` — single self-contained HTML/CSS/JS file, no dependencies, no build step  
**Hosting:** Netlify (needs permanent account — currently on 1-hour free drop)  
**Repo:** Not yet created — needs GitHub repo `voodoo-clam-clan`  

---

## Immediate Next Steps for Claude Code

1. **Create GitHub repo** `voodoo-clam-clan` (public, for free Netlify auto-deploy)
2. **Push `index.html`** to repo root
3. **Connect Netlify** to GitHub repo for auto-deploy on push
4. **Set custom Netlify URL** → `voodoo-clam-clan.netlify.app`
5. **Add Google Form link** → swap `href="#"` on the form button (line ~search "Open the Planning Form")
6. **Add pending sections** (see below)

---

## File Structure (current)

```
index.html          ← entire site, single file
HANDOVER.md         ← this file
```

**Planned structure once on GitHub:**
```
index.html
HANDOVER.md
assets/
  images/
    logo.png              ← designer's voodoo clam logo (pending)
    airbnb-pool.jpg       ← Airbnb backyard photo
    moodboards/           ← Pinterest inspo images
  design/
    voodoo-clam-logo.ai   ← designer source files
```

---

## The Event — Full Context

**Airbnb:** 2012 Oretha Castle Haley Blvd, New Orleans LA 70113  
- Lower Garden District / Central City border  
- Private pool, teal/dark mural wall, outdoor dining  
- $3,066 total · 4 nights · ~$341/person at 9 girls  
- Girls confirm participation by July — if 3+ drop, find alternative  

**Flights:** Southwest direct  
- Depart: Oct 3, 11:10am → arrive 2:40pm  
- Return: Oct 6, 2:20pm → arrive 4:20pm  
- Current price: ~$327/person  

**Group size:** 8–10 girls paying. Kassie (bride) goes free — her costs covered optionally by the group.

---

## Four Themed Nights

### Night 1 — The Convoy 🕶️ (Saturday Oct 3)
- **Kassie:** White flowy dress · pearl accessories · black sunglasses
- **Clan:** All black everything · pearl jewelry · black sunglasses
- **Plan:** Arrive 3pm · settle in · French Quarter bar crawl + street food in Voodoo Clam tees · meet the boys (groom's ~10 friends, their last night) · The Rabbit Hole dance bar (8 min walk, open til 4am Sat)
- **Boys join:** ~20 people total this night only — no sit-down restaurant, street food/bar crawl format

### Night 2 — The Shells 🦪✨ (Sunday Oct 4)
- **Kassie:** Iridescent/pearl wrap dress
- **Clan:** Full glam · each girl picks her own sequin/iridescent color · boas · glitter · big hair
- **Morning:** Drag Brunch at The Country Club (1pm) OR Spa day at Spa Isbell (Magazine St, walking distance) — **vote pending**
- **Afternoon:** Pool time at Airbnb, re-glam
- **Night:** Dinner (vote pending) → Oz on Bourbon + Café Lafitte in Exile (no cover)
- **Daytime outfit:** Voodoo Clam Clan custom tees

### Night 3 — The Coven 🔮 (Monday Oct 5)
- **Kassie:** Deep emerald or plum boho maxi · goddess energy
- **Clan:** Flowing dark fabrics · jewel tones · crystals · layered jewelry · boots
- **Morning:** Activity vote (swamp tour / Tea Room / French Market / Spa)
- **Dinner:** French Quarter area (vote pending) — before 8pm ghost tour
- **8pm:** Ghost, Crime, Voodoo & Vampire Tour VIP HELLVISION — booked on Viator
- **Nightcap:** Bayou Bar (7 min walk) or Frenchmen Street

### Night 4 — The Uncursing 🌊 (Tuesday Oct 6)
- Checkout 11am · Southwest flight 2:20pm

---

## Confirmed Bookings (URGENT)

| Priority | What | Action |
|---|---|---|
| 🔴 NOW | Drag Brunch — The Country Club | Call (504) 832-1930 · Sunday Oct 4 · 1pm · group of 8–10 |
| 🔴 NOW | Ghost Tour VIP HELLVISION | Viator.com · Monday Oct 5 · 8pm · $44pp |
| 🟡 4–6 wks | Airboat Swamp Tour | Viator.com · Monday Oct 5 · Large Airboat Drive Out $67pp |
| 🟡 Soon | Monday Dinner | Muriel's (504) 568-1885 OR Café Amelie · group of 8–10 |
| 🟡 Soon | Voodoo Clam Clan Tees | Etsy or local printer · collect sizes from Google Form first |

---

## Website Sections (current `index.html`)

1. **Hero** — animated, iridescent gradient, date chips
2. **Itinerary** — accordion cards per night, outfit strips, event timelines
3. **The Looks** — outfit guide per night, Kassie rules, Clan code
4. **Budget Calculator** — fully interactive JS tracker (see below)
5. **For Kassie** — goal tracker with progress bars, linked to budget
6. **Book Now** — priority booking list with urgent flags
7. **Clan Rules** — 6 rules
8. **The Form** — Google Form link (currently `href="#"` — NEEDS REAL LINK)
9. **Footer**

### Sections TO ADD (planned, not yet built)

- **Pay Your Share** section — Venmo / PayPal.me / Apple Pay buttons
- **Photo Album** — link to shared Google Drive folder
- **Inspo Board** — link to Pinterest board + embedded mood board images
- **Designer's Logo** — once received, add to nav + hero (designer friend, ~$40, pending)
- **Gallery** — post-trip photo wall (future)

---

## Budget Tracker — Full Data (JS variables in index.html)

The entire budget calculator is vanilla JS rendered into `#budget-app`. Key variables:

```javascript
var ng = 9; // paying girls, adjustable

// Fixed costs (all checked by default, can uncheck)
var fixedItems = [
  { name:"Airbnb", total:3066, on:true },
  { name:"Voodoo Clam Clan custom tees", pp:25, on:true },
  { name:"Group sunglasses", total:75, on:true },
  { name:"Snacks & Drinks — whole weekend", total:200, on:true },
];

// Saturday dinner options (single select)
var satD = [
  { lbl:"French Quarter bar crawl + street food", pp:35 },
  { lbl:"Dinner + bourbon bar or cigar bar", pp:70 },
  { lbl:"Arnaud's", pp:100 },
  { lbl:"DoorDash at the Airbnb (gag option)", pp:20 },
];

// Sunday morning (single select)
var sunM = [
  { lbl:"Drag Brunch — The Country Club", pp:65, uber:14 },
  { lbl:"Spa day — Spa Isbell", pp:100, uber:0 },
  { lbl:"Free pool day", pp:0, uber:0 },
];

// Sunday lunch (single select)
var sunL = [
  { lbl:"Turkey & Wolf", pp:25 },
  { lbl:"Willa Jean", pp:35 },
  { lbl:"DoorDash at the Airbnb", pp:22 },
];

// Sunday dinner (single select) — all confirmed open Sundays
var sunD = [
  { lbl:"Juan's Flying Burrito", pp:20 },       // walkable, cheap
  { lbl:"Peche Seafood Grill", pp:60 },          // James Beard winner
  { lbl:"Cochon", pp:62 },                        // Michelin Bib Gourmand
  { lbl:"Gris-Gris", pp:70 },                    // upscale Southern Creole
];

// Sunday night clubs (multi-select checkboxes)
var clubs = [
  { lbl:"Oz New Orleans", pp:12, on:true },
  { lbl:"Café Lafitte in Exile", pp:20, on:true },
  { lbl:"Uber home from French Quarter", pp:16, on:true },
];

// Monday morning (multi-select checkboxes — smart Uber logic)
var monActs = [
  { lbl:"Airboat swamp tour + gators", pp:77, uberKey:"swamp", on:true },  // $67 + $10 Uber baked in
  { lbl:"Bottom of the Cup Tea Room", pp:35, uberKey:"fq", on:false },     // shares Uber with French Market
  { lbl:"French Market + shopping", pp:0, uberKey:"fq", on:false },        // Free, shares Uber with Tea Room
  { lbl:"Belladonna Spa", pp:75, uberKey:"walk", on:false },               // walking distance
];
// Note: Tea Room + French Market share one $15pp Uber if both selected

// Monday dinner (single select)
var monD = [
  { lbl:"Muriel's Jackson Square", pp:95 },   // haunted, steps from ghost tour
  { lbl:"Cafe Amelie", pp:65 },               // candlelit courtyard
  { lbl:"Compere Lapin", pp:65 },             // Michelin, Warehouse District
];

// Ghost tour (single select — yes/no)
var ghostOpts = [
  { lbl:"Ghost Tour VIP HELLVISION", pp:60 },  // $44 + $16 Uber
  { lbl:"Skip", pp:0 },
];

// Nightcap (single select)
var nightOpts = [
  { lbl:"Bayou Bar", pp:25, uber:0 },           // 7 min walk
  { lbl:"Frenchmen Street", pp:30, uber:16 },   // + Uber
  { lbl:"Head home", pp:0, uber:0 },
];

// Kassie contributions (click to toggle, share button or custom input)
var kassItems = [
  { name:"Kassie's Airbnb share", total:341 },
  { name:"Kassie's ghost tour ticket", total:44 },
  { name:"Kassie's flight", total:327 },
  { name:"Kassie's morning activity", total:82 },
  { name:"Kassie's dinner — one night", total:80 },
  { name:"Kassie's bridal sash + extras", total:55 },
];
// Kassie goal tracker in #kassie section updates live from kassItems
```

---

## Google Form — Status

**Not yet built.** A guide was written in a previous artifact (`voodoo-clam-clan-google-form-guide.html`).

Form should collect:
- Full name + phone
- T-shirt size (XS–3XL) — for Voodoo Clam Clan tee
- Airbnb confirmation (yes/no/not sure) — answer by July
- Activity votes: Sunday morning (Drag Brunch / Spa / IDC / other suggestion)
- Activity votes: Monday morning (ranked or checkbox)
- Saturday dinner vote (3 options)
- Sunday dinner vote (ranked 1–4)
- Monday dinner vote (ranked 1–3)
- Club preference Sunday night
- Swamp tour in/out + transport preference (shuttle vs drive-out)
- Drink preferences (checkboxes)
- Food allergies (short answer)
- Favorite drunk snack (short answer — important)
- Kassie contribution pledges per item
- Anything MOH should know (long answer)
- Hype level 1–10

**Settings:** No sign-in required · anyone with link can fill · allow response editing · show progress bar

**After form is built:** Replace `href="#"` in index.html form section with real Google Form link.

---

## Results Presentation — Not Yet Built

After Google Form closes, build a results deck showing:
- Pie charts / bar charts for each vote
- Winner announced per category
- Could be a second HTML page (`results.html`) in the same repo

---

## Design System

```css
--black: #080608;
--pearl: #f0ece4;
--pearl-dim: rgba(240,236,228,0.55);
--pearl-faint: rgba(240,236,228,0.12);
--teal: #5ecfcf;
--teal-dim: rgba(94,207,207,0.2);
--teal-faint: rgba(94,207,207,0.07);
--gold: #c9a84c;
--pink: #D4537E;
--border: rgba(240,236,228,0.1);
--border-teal: rgba(94,207,207,0.25);

/* Fonts */
'Cinzel Decorative' — display headings
'Cinzel' — labels, nav, eyebrows
'Cormorant Garamond' — italic subheadings, body elegance
'DM Sans' — body text, notes
```

---

## Key People

| Person | Role | Notes |
|---|---|---|
| Kassie | The Bride | 2 babies in 3 yrs, body-conscious, boho/flowy style, absolutely must be hyped |
| MOH (user) | Organizer | Running this whole operation |
| Grace | MOH's co-organizer | Sharing 2nd bedroom at Airbnb |
| Designer friend | Logo + decor inspo | Paid ~$40–60, delivering voodoo clam logo + decor mood board |
| The Boys | Groom's crew (~10) | Join Saturday night only |

---

## Outfit Themes Summary

| Night | Kassie | Clan |
|---|---|---|
| The Convoy (Sat) | White flowy dress + pearl accessories + black sunglasses | All black + pearl jewelry + black sunglasses |
| The Shells (Sun) | Iridescent/pearl wrap dress | Each girl: own sequin/iridescent color · boas · glitter |
| The Coven (Mon) | Deep emerald or plum boho maxi | Dark flowing fabrics · jewel tones · crystals · boots |
| Daytime (Sun) | Voodoo Clam tee (styled) | Voodoo Clam tee (styled) |

---

## Kassie Rules (non-negotiable, in website)

1. Kassie goes first — every mirror, photo, compliment
2. Hype is mandatory — designate a hype captain each night
3. No body talk — zero, not even about yourself
4. Everyone gets photographed — rotate camera duty
5. Emergency kit is shared — fashion tape, safety pins, blister pads, dry shampoo
6. The theme always wins — unsure? Add a crystal, add a pearl

---

## What Was Discussed But Not Built

- **Results presentation** with pie charts (post-form)
- **Kassie goal tracker as standalone section** — partially built into index.html, linked to budget
- **"White Lies" t-shirt** — front says "White Lies", back has designer's voodoo clam illustration + custom font "Voodoo Clam Clan" + date. Designer friend handling.
- **Carrd vs GitHub Pages** — chose GitHub + Netlify instead
- **Room assignments** — intentionally not included in the site (too much drama potential). MOH handles offline.

---

## Notes for Claude Code

- The entire site is **one HTML file** with embedded CSS and JS. No framework, no build step, no npm.
- The budget tracker uses **vanilla JS DOM manipulation** (not innerHTML for inputs — learned the hard way, caused rendering bugs).
- The Kassie goal tracker reads from `kassItems` array and updates via `renderGoal()` called inside `renderBudget()`.
- Night accordion uses simple `classList.toggle` — keep it simple.
- All Google Fonts loaded via CDN link in `<head>` — no local fonts.
- **Do not** introduce a JS framework unless the complexity demands it. Keep it deployable as a single file drag-and-drop.
- Mobile nav links hidden at 640px — hamburger menu not yet implemented, low priority.
- When designer delivers logo: add as `<img>` in nav and hero, store in `assets/images/`.
- When Google Form link is ready: find `href="#"` on the form button and replace.


---

## Additional Context (Critical — Do Not Lose)

### The Airbnb
- Initially thought to be corner of Thalia & Baronne (Lower Garden District)
- Then thought to be Canal & S Rocheblave (Mid-City)
- **Confirmed address: 2012 Oretha Castle Haley Blvd** — Lower Garden District/Central City border
- Hosted by Samuel on Airbnb
- Check-in: Sat Oct 3, 3pm · Checkout: Tue Oct 6, 11am
- Key feature: dark teal mural wall in backyard + pool — this IS the Voodoo Clam aesthetic
- **Room assignment strategy (offline, not on website):** Kassie = master king (non-negotiable, announced by MOH). MOH + Grace = 2nd bedroom. Rest = not formally assigned to avoid drama. Frame as "lottery" if needed.

### About Kassie (Critical for Every Outfit/Activity Decision)
- Has had **2 babies in the last 3 years** — body-conscious, needs constant lifting up
- Style comfort zone: **boho & flowy** — wrap silhouettes, off-shoulder, flutter sleeve, flowing midis/maxis
- Never bodycon, never tight — not because she can't, because she shouldn't have to think about it
- Every outfit suggestion for her is chosen with this in mind: wrap = adjustable, flattering, effortlessly sexy
- The Clan's job: hype her like she's the most beautiful woman in every room. She will be.
- **No body talk rule** — zero. Not even about your own body. Not even jokingly.

### The T-Shirt
- **Front:** "White Lies" (the bachelorette game where everyone wears a lie about themselves on their shirt)
- **Back:** Designer's voodoo clam illustration + custom font "Voodoo Clam Clan" + date (Oct 3–6, 2026)
- **Designer:** Friend of MOH, being paid ~$40–60 for logo + decor mood board
- **Fair rate note:** $40 is low for custom illustrated logo + typography. $60–75 is more appropriate if she's also doing decor inspo. MOH's call since she knows the friend.
- **Order timeline:** Collect sizes via Google Form FIRST, then order — 6–8 weeks out minimum
- Worn: Saturday night (bar crawl with the boys) + Sunday morning (drag brunch or spa)

### The Boys — Saturday Night Joint Night
- Kassie's groom + his crew = ~10 people
- It's their **last night** (bachelor party ending) and **our first night** simultaneously
- Total group: ~20 people
- **No sit-down restaurant for 20** — street food + bar crawl format is the answer
- They drift off whenever, we keep going
- The Rabbit Hole is the late-night option (8 min walk from Airbnb, open til 4am Saturdays)
- **Check Rabbit Hole Sunday hours** before using it as a Sunday option — some sources show closed Sundays

### Why Sunday for Drag Brunch (Not Monday)
- Drag brunch at The Country Club is **weekends only**
- This is why the schedule is: Shells (Sun) → Coven (Mon), not the other way around

### Restaurants Researched and Eliminated
- **Coquette** — permanently closed. Do not suggest.
- **Purloo** — permanently closed. Do not suggest.
- **Mister Oso** — considered for cheap Sunday dinner, replaced by Juan's Flying Burrito
- All Sunday dinner options confirmed open Sundays: Juan's ✅, Pêche ✅, Cochon ✅, Gris-Gris ✅

### Bottom of the Cup Tea Room — Flagged
- Reviews are mixed for group events
- MOH flagged it as "a little gimmicky, can't tell if worth the price for a group"
- Kept as a Monday morning option but not strongly recommended
- Ghost tour (Haunted History Tours / Viator) is a much stronger activity

### Payment Links — To Be Added to Website
- MOH needs to provide: Venmo handle, PayPal.me link
- Apple Pay works via Venmo/PayPal
- A "Pay Your Share" section is planned for the website
- Claude Code should build this section once MOH provides her payment handles

### Google Drive + Pinterest — To Be Added to Website
- MOH wants a link to a shared Google Drive folder for trip photos
- MOH wants a link to a Pinterest board for outfit inspo
- Both are planned website sections — Claude Code to implement once links are provided

### Google Form — July Deadline
- The Airbnb confirmation question specifically needs a **"please answer by July"** framing
- If 3+ girls drop out of the Airbnb, will look for alternative accommodation
- Form collects: sizes, votes, drink prefs, allergies, drunk snack, Kassie pledges, Airbnb confirmation

### Voodoo Clam Clan Name
- Fully the MOH's idea, completely original
- The "clam" is the central motif — voodoo + clam = dark bayou glamour meets coastal camp
- A mysterious sea creature that holds secrets, grants wishes (or curses), lives in the murky bayou
- This mythology should carry through all copy on the website

### Netlify Deployment Notes
- Current live URL (temporary, 1hr): https://unrivaled-praline-9a49ae.netlify.app
- Password: My-Drop-Site
- Needs permanent Netlify account + GitHub repo to stay live
- GitHub repo name: `voodoo-clam-clan`
- Once connected: every GitHub push = automatic Netlify redeploy
- Single file deployment: `index.html` — no build step, no npm, no framework
- **Do not introduce a JS framework** — keep it deployable as single file drag-and-drop

### Kassie Goal Tracker
- Lives in `#kassie` section of index.html
- Progress bars per expense item, updates live when contributions toggled in budget section
- Connected via `kassItems` array and `renderGoal()` function called inside `renderBudget()`
- Goal items mirror `kassItems` in the budget tracker exactly

### What Was Explicitly Decided Against
- **Gamma presentation** — tried it, not clickable enough, moved to Google Form instead
- **Bottom of the Cup** as group activity — too gimmicky, replaced by ghost tour
- **Commander's Palace** — originally considered for farewell dinner, replaced by French Quarter options
- **Café Du Monde** — mentioned as a landmark but not a meal option
- **Room assignment on website** — intentionally excluded to avoid drama
- **Matching merch beyond tees** — sashes for Kassie/MOH only, no full group matching

