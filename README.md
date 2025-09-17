NICKELTAP

A single-screen progressive web app that settles the Nickelback debate by tapping.
Users pick Team Love or Team Hate, smash the Chad Nickel button, and watch the global tally climb in real time.
Designed to be a perfect digital fidget toy: satisfying, addictive, and stupidly simple.

URL: https://nickeltap.com

Platform: Progressive Web App (mobile-first, works everywhere)
Dev/Hosting: Replit (all-in-one hosting, backend, database)

EXECUTIVE SUMMARY
Nickeltap gamifies a cultural debate with one mechanic: tap to vote. Users select Team Love or Team Hate and tap a silver nickel button featuring Chad Kroeger. Global team totals update smoothly. Built as a lightweight PWA with vanilla HTML, CSS, and JS.

PROBLEM STATEMENT
The Debate: The internet wants a definitive answer to the Nickelback question.
The Need: People want mindless, satisfying micro-interactions during boredom gaps.
The Gap: No app has turned a cultural debate into a simple, addictive tapping loop.

COLOR PALETTE
Background: #1E1E2E
Text Primary: #F8F8FF
Team Love: #FF0080
Team Hate: #00D9FF
Nickel Light: #E5E5E5
Nickel Dark: #B8B8B8
Glow Love: #FF008033
Glow Hate: #00D9FF33
Footer Text: #F8F8FF4D

SUCCESS METRICS
Phase 1 (Month 1): 10k taps, 1k unique visitors, 50 percent return rate, 30+ taps per session
Phase 2 (Months 2–3): 100k taps, 10k unique visitors, 50+ taps per session, 10 percent reach Legendary
Phase 3 (Month 6): 1M taps, 50k unique visitors, 20 percent share rate, Teams stay within 60/40 split

USER JOURNEY
First visit:

Sees shared score.

Lands on nickeltap.com and understands instantly.

Picks a team.

Starts tapping.

Feels hooked by the effects.

Shares score with friends.

Return visit:

Team remembered.

Sees lifetime stats and personal best.

Starts tapping immediately.

FUNCTIONAL REQUIREMENTS

Layout is mobile-first, viewport locked, no scrolling or zooming.

Sound toggle in top right, ON by default.

Footer terms/privacy/help/share at bottom with low opacity.

Team selection pill buttons in hot pink and cyan, saved to localStorage.

Chad Nickel button is center stage, 150px mobile / 200px desktop, with squish physics, micro-expressions, escalating rewards, random bonuses, visual glow effects, and sound effects.

Counters: global server totals updated every 2s, personal session counter, lifetime counters saved locally.

Share: Web Share API on mobile, clipboard fallback on desktop.

TECHNICAL ARCHITECTURE
Frontend:

Vanilla HTML, CSS, JS

Single file index.html under 50KB

PWA ready with manifest and service worker

localStorage for team, stats, and Legendary status

Backend:

Node.js with Express

API endpoints:
GET /api/counts
POST /api/tap (or batched /api/tapBatch)

Database: Replit DB key-value store

Upgrade path to Postgres later if needed

Data model (Replit DB keys):
total:love -> count
total:hate -> count
ratelimit:{ip}:{minute} -> tap count

Rate limiting: 300 taps per minute per IP, silent failure (UI still responsive)

PERFORMANCE TARGETS
First paint under 300ms
Interactive under 500ms
Tap response under 16ms
Bundle size under 50KB
No frameworks, no dependencies, no bloat

PRIVACY AND SECURITY
We track: team totals only
We do not track: personal data, analytics, cookies, accounts, or emails
Security: HTTPS only, rate limiting, sanitization, no user data surface

DEVELOPMENT PHASES
Phase 1: Static Prototype (local counters, button feel)
Phase 2: Live (backend, Replit DB, global counts, rate limiting)
Phase 3: Addiction Layer (escalating effects, rewards, Legendary status, sound, local records)
Phase 4: Polish (sharing, PWA install, performance optimization, cross-browser/device testing, launch)

PROJECT STRUCTURE
nickeltap/

index.html

style.css

script.js

chad-nickel.png

tap-sound.mp3
Phase 2 adds:

server.js

Replit DB entries

GETTING STARTED (REPLIT)
Phase 1:

Create new Repl with HTML/CSS/JS template

Add index.html, style.css, script.js, chad-nickel.png, tap-sound.mp3

Run project and confirm layout and tap feel

Phase 2:

npm init -y

npm install express

Add server.js with endpoints

Update Replit run command to "node server.js"

Frontend polls GET /api/counts every 2s and sends batched taps to POST /api/tapBatch

TESTING CHECKLIST

Tap squish is instant, no lag at 10 taps/sec

Team selection works and persists

Streak system and stage escalation messages appear at correct tap counts

Multiple browser tabs sync with same global totals

Mobile works: no scroll/zoom, haptics, sound unlocks on first tap

Share button works on mobile and desktop

RISK MITIGATION
Bot abuse: limited to 300/min/IP
Server overload: Replit autoscaling, upgrade to Postgres when needed
Team imbalance: UI messaging to encourage competition
Retention risk: Legendary status, personal bests, prestige loop
Mobile bugs: test early on physical devices

LICENSE
Proprietary. All rights reserved.
