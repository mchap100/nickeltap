Nickeltap

A single-screen PWA that settles the Nickelback debate by tapping.
Pick Team Love or Team Hate, smash the Chad Nickel button, and watch the global tally climb in real time. Designed to be a perfect digital fidget toy: satisfying, addictive, and stupidly simple.

URL: https://nickeltap.com

Platform: Progressive Web App (mobile-first, works everywhere)

Dev/Hosting: Replit (all-in-one hosting, backend, database)

Table of Contents

Executive Summary

Problem Statement

Color Palette

Success Metrics

User Journey

Functional Requirements

Technical Architecture

API

Data Model

Rate Limiting

Performance Targets

Privacy & Security

Development Phases

Project Structure

Getting Started (Replit)

Testing Checklist

Risk Mitigation

License

Executive Summary

Nickeltap gamifies a cultural debate with a single mechanic: tap to vote. Users select Team Love or Team Hate and tap a silver nickel button (Chad Kroeger face). Global team totals update smoothly. The entire Phase-1 build runs as a lightweight PWA with vanilla HTML/CSS/JS.

Problem Statement

The Debate: The internet wants a definitive answer to the Nickelback question.

The Need: People crave mindless, satisfying micro-interactions during boredom gaps.

The Gap: No app has turned a cultural debate into a simple, addictive tapping loop.

Color Palette
/* Nickeltap Color System */
--background:    #1E1E2E;  /* Purple-gray base */
--text-primary:  #F8F8FF;  /* Ghost white */
--team-love:     #FF0080;  /* Hot pink */
--team-hate:     #00D9FF;  /* Electric cyan */
--nickel-light:  #E5E5E5;  /* Nickel gradient top */
--nickel-dark:   #B8B8B8;  /* Nickel gradient bottom */
--glow-love:     #FF008033;/* Pink glow (20% opacity) */
--glow-hate:     #00D9FF33;/* Cyan glow (20% opacity) */
--footer-text:   #F8F8FF4D;/* Ghost white 30% opacity */

Success Metrics

Phase 1 (Month 1): 10k taps · 1k unique visitors · 50% return rate · 30+ taps/session
Phase 2 (Months 2–3): 100k taps · 10k uniques · 50+ taps/session · 10% reach Legendary
Phase 3 (Month 6): 1M taps · 50k uniques · 20% share rate · Teams stay within 60/40

User Journey

First Visit

Sees shared score (e.g., “Team Love: 32M vs Team Hate: 28M”)

Lands on nickeltap.com and instantly groks the premise

Picks a team (pink/cyan) and starts tapping

Addictive feel/sound/effects kick in

Shares “I just cast 47 votes for Team Love at nickeltap.com”

Return

Team remembered, sees lifetime/local bests, starts tapping immediately

Functional Requirements

Layout (Mobile-First)

                                  [🔊]
             Nickeltap

 Team Love               Team Hate
 32,847,294              28,492,018

     Tap to settle the debate

        [ Love ] [ Hate ]

          ((( 5¢ )))
        [ Chad Nickel ]

        Your taps: 47

 Terms · Privacy · Help · Share


Core Layout Rules

Viewport locked (100vh/100dvh), no scrolling/zooming

All content visible (no hidden UI)

Sound toggle top-right (ON by default)

Footer ~30% opacity

Team Selection

Pink/cyan pill buttons

Saved to localStorage; can switch anytime (taps count for current team)

Smooth “whoosh” feedback

Chad Nickel Button (the star)

Size: 200×200px (desktop), 150×150px (mobile)

Squish Suite: finger-weighted warp, deeper inner shadow on press, spring on release, edge-tap asymmetry, multi-touch warp points

Randomized micro-expressions: ~1 in 50 taps

Escalation:

1–100: momentum

101–250: On Fire!

251–500: Unstoppable

501–999: Godlike

1000+: LEGENDARY STATUS → then Prestige loop

Visuals: glow ring, +1 floaters, particles, shifting shadow, wobble, wear marks after 1000 taps (saved locally)

Random Bonuses: ~every 47 taps golden +1; ~every 100 special animation; 1/200 CRITICAL HIT! (2x)

Sound

Crisp “pop” per tap; milestone chimes; slight pitch escalations with streaks

Counters

Global: poll server every 2s; instant local increment, smooth animate to server truth

Session: “Your taps: N” (resets on refresh) + “Personal Best!” if topped

Lifetime (localStorage):

{
  "totalTaps": 2847,
  "personalBest": 347,
  "legendaryAchieved": true,
  "prestige": 2
}


Share

Web Share API (mobile) + clipboard fallback (desktop)

Dynamic text includes current team and contributed taps

Technical Architecture

Frontend (Phase 1)

Vanilla HTML + CSS + JS in a single page (index.html < 50KB)

PWA: manifest + service worker

localStorage for team choice, personal bests, legendary flag

Backend (Phase 2)

Node.js + Express (Replit)

Minimal API:

POST /api/tap (plan uses batched variant /api/tapBatch)

GET /api/counts

Database: Replit DB (string keys)

Upgrade path to Postgres (only when needed)

API
GET /api/counts

Response

{ "love": 32847294, "hate": 28492018 }

POST /api/tap

Phase 2 uses a batch endpoint; name can be /api/tapBatch.

Request

{ "team": "love" }


Response

{
  "success": true,
  "totals": { "love": 32847294, "hate": 28492018 }
}


Batch (recommended)

{
  "team": "love",
  "count": 5,
  "sessionId": "abc123",
  "seq": 42
}

Data Model

Replit DB string keys (Phase 2):

"total:love" -> 32847294
"total:hate" -> 28492018
"ratelimit:{ip}:{minute}" -> 47

Rate Limiting

300 taps/minute/IP

Silent failure: UI stays responsive; server simply stops incrementing beyond limit

Performance Targets

First paint: < 300ms

Interactive: < 500ms

Tap response: < 16ms (instant feel)

Bundle size: < 50KB

No frameworks, no dependencies, no bloat

Privacy & Security

We Track

Team vote counts only

We Don’t Track

No personal data

No analytics

No cookies (beyond functional localStorage)

No accounts, emails, or behavioral tracking

Security

HTTPS only

Rate limiting

Input sanitization

Minimal data surface → minimal breach risk

Development Phases

Phase 1: Static Prototype

Perfect layout (locked viewport)

Team toggle

Local counter

Button animation & feel

Phase 2: Make it Live

Add backend (Express)

Replit DB totals

Global counters + smooth sync

Rate limiting

Phase 3: Addiction Layer

Escalating effects (1–1000)

Random rewards

Legendary status & Prestige

Sound effects

Personal records

Phase 4: Polish

Share (Web Share API + clipboard)

PWA installable

Perf passes

Cross-browser/device tests

Public launch

Project Structure

(Phase-1 simple static; Phase-2 adds server and DB.)

nickeltap/
├─ index.html          # Single page app (PWA)
├─ style.css           # Visuals + motion
├─ script.js           # Tap logic + UI
├─ chad-nickel.png     # Button image
├─ tap-sound.mp3       # Tap sound
# Phase 2 additions:
├─ server.js           # Express API
└─ (Replit DB)         # Key-value totals (managed by Replit)

Getting Started (Replit)

Phase 1 (Static)

Create Repl → HTML/CSS/JS template

Add files: index.html, style.css, script.js, chad-nickel.png, tap-sound.mp3

Run → verify locked viewport, tap feel, local counter

Phase 2 (Server)

npm init -y
npm install express
# Add server.js per plan
# Set Replit run command to: node server.js


Frontend polls GET /api/counts every ~2s

Taps batched via POST /api/tapBatch (5 taps or 300ms)

Testing Checklist

Feel

Tap squish is instant, springy on release

+1 floats from tap position

No missed taps at 10 taps/sec

Teams

Selecting Love/Hate updates styles; persists in localStorage

Tapping without a team prompts selection

Streak & Stages

Streak shows after 5 taps; resets ~2s idle

Stage badges at 101/251/501/1000+ as specified

Global Sync

Multiple tabs see totals converge smoothly every ~2s

Batch sends land on server; rate limiting respected

Mobile

No scroll/zoom; haptics work; audio unlocked on first interaction

Share

Web Share on mobile; clipboard on desktop

Risk Mitigation
Risk	Mitigation
Bot abuse	300/min/IP, silent limiting
Server overload	Replit auto-scaling; simple upgrade path
One team dominates	Competitive copy/visuals in UI
Weak retention	Legendary status, personal bests, prestige
Mobile quirks	Test on real devices early
License

Proprietary. All rights reserved unless explicitly licensed otherwise.

Notes for Contributors

Stay within scope: one screen, one mechanic, zero bloat.

No frameworks in Phase 1. Minimal Express + Replit DB in Phase 2.

PRs that add complexity without user-perceived feel/performance gains will be rejected.
