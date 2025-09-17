# Nickeltap

**A single-screen PWA that settles the Nickelback debate by tapping.**  
Pick **Team Love** or **Team Hate**, smash the **Chad Nickel** button, and watch the global tally climb in real time. Designed to be a perfect digital fidget toy: **satisfying, addictive, and stupidly simple.**

- **URL:** https://nickeltap.com  
- **Platform:** Progressive Web App (mobile-first, works everywhere)  
- **Dev/Hosting:** Replit (all-in-one hosting, backend, database)

---

## Table of Contents
- [Executive Summary](#executive-summary)
- [Problem Statement](#problem-statement)
- [Color Palette](#color-palette)
- [Success Metrics](#success-metrics)
- [User Journey](#user-journey)
- [Functional Requirements](#functional-requirements)
- [Technical Architecture](#technical-architecture)
- [API](#api)
- [Data Model](#data-model)
- [Rate Limiting](#rate-limiting)
- [Performance Targets](#performance-targets)
- [Privacy & Security](#privacy--security)
- [Development Phases](#development-phases)
- [Project Structure](#project-structure)
- [Getting Started (Replit)](#getting-started-replit)
- [Testing Checklist](#testing-checklist)
- [Risk Mitigation](#risk-mitigation)
- [License](#license)

---

## Executive Summary
Nickeltap gamifies a cultural debate with a single mechanic: **tap to vote**. Users select **Team Love** or **Team Hate** and tap a **silver nickel** button (Chad Kroeger face). Global team totals update smoothly. The entire Phase-1 build runs as a lightweight PWA with **vanilla HTML/CSS/JS**.

---

## Problem Statement
- **The Debate:** The internet wants a definitive answer to the Nickelback question.  
- **The Need:** People crave mindless, satisfying micro-interactions during boredom gaps.  
- **The Gap:** No app has turned a cultural debate into a simple, addictive tapping loop.

---

## Color Palette
```css
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

Sees shared score (e.g., “Team Love: 32M vs Team Hate: 28M”).

Lands on https://nickeltap.com and instantly groks the premise.

Picks a team (pink/cyan) and starts tapping.

Addictive feel/sound/effects kick in.

Shares “I just cast 47 votes for Team Love at nickeltap.com”.

Return

Team remembered, sees lifetime/local bests, taps immediately.

Functional Requirements
Layout (Mobile-First)

css
Copy code
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

Chad Nickel Button

Size: 200×200 (desktop), 150×150 (mobile)

Squish Suite: finger-weighted warp, deeper inner shadow on press, spring on release, edge-tap asymmetry, multi-touch warp points

Micro-expressions: ~1 in 50 taps

Escalation: 1–100 momentum · 101–250 On Fire! · 251–500 Unstoppable · 501–999 Godlike · 1000+ LEGENDARY → Prestige

Visuals: glow ring, +1 floaters, particles, shifting shadow, wobble, wear marks after 1000 taps

Random Bonuses: ~every 47 taps golden +1; ~every 100 special animation; 1/200 CRITICAL HIT! (2x)

Sound

Crisp tap “pop”, milestone chimes, slight pitch escalation with streaks

Counters

Global: poll server every ~2s; instant local increment; smooth animate to server truth

Session: “Your taps: N” (resets on refresh) + “Personal Best!” when topped

Lifetime (localStorage):

json
Copy code
{
  "totalTaps": 2847,
  "personalBest": 347,
  "legendaryAchieved": true,
  "prestige": 2
}
Share

Web Share API (mobile) + clipboard fallback (desktop) with dynamic text

Technical Architecture
Frontend (Phase 1)

Vanilla HTML + CSS + JS (index.html < 50KB)

PWA: manifest + service worker

localStorage for team, records, legendary flag

Backend (Phase 2)

Node.js + Express (Replit)

API: POST /api/tap (or /api/tapBatch), GET /api/counts

DB: Replit DB (KV). Upgrade to Postgres later if needed.

API
GET /api/counts
Response

json
Copy code
{ "love": 32847294, "hate": 28492018 }
POST /api/tap (Phase 2 baseline)
Request

json
Copy code
{ "team": "love" }
Response

json
Copy code
{ "success": true, "totals": { "love": 32847294, "hate": 28492018 } }
POST /api/tapBatch (recommended)
Request

json
Copy code
{ "team": "love", "count": 5, "sessionId": "abc123", "seq": 42 }
Data Model (Replit DB)
rust
Copy code
"total:love"              -> 32847294
"total:hate"              -> 28492018
"ratelimit:{ip}:{minute}" -> 47
Rate Limiting
300 taps/minute/IP

Silent failure: UI stays responsive; server simply stops incrementing beyond limit

Performance Targets
First paint < 300ms · Interactive < 500ms · Tap response < 16ms

Bundle < 50KB · No frameworks, no deps, no bloat

Privacy & Security
We Track: team totals only
We Don’t Track: personal data, analytics, accounts, emails, behavioral data
Security: HTTPS only, rate limiting, input sanitization, minimal data surface

Development Phases
Phase 1 – Static Prototype: locked viewport, team toggle, local counter, button feel

Phase 2 – Live: backend + Replit DB, global totals, rate limiting

Phase 3 – Addiction Layer: escalating effects, random rewards, Legendary + Prestige, sound, personal records

Phase 4 – Polish: share, PWA install, perf, cross-browser/device, launch

Project Structure
pgsql
Copy code
nickeltap/
├─ index.html
├─ style.css
├─ script.js
├─ chad-nickel.png
├─ tap-sound.mp3
# Phase 2:
├─ server.js
└─ (Replit DB)
Getting Started (Replit)
Phase 1 (Static)

Create Repl → HTML/CSS/JS template

Add files above

Run → verify locked viewport, tap feel, local counter

Phase 2 (Server)

bash
Copy code
npm init -y
npm install express
# Add server.js per plan and set run to `node server.js`
Frontend polls GET /api/counts (~2s) and batches taps to POST /api/tapBatch.

Testing Checklist
Instant squish + spring; +1 from tap point; no missed taps at 10 tps

Team selection persists; prompts if tapping without a team

Streak after 5 taps; stages at 101/251/501/1000+

Multiple tabs converge on same global totals within ~2s

Mobile: no scroll/zoom; haptics; audio unlocked on first interaction

Share: Web Share on mobile; clipboard on desktop

Risk Mitigation
Risk	Mitigation
Bot abuse	300/min/IP, silent limiting
Server overload	Replit auto-scaling; simple upgrade path
One team dominates	Competitive copy/visuals in UI
Weak retention	Legendary status, personal bests, prestige
Mobile quirks	Test on real devices early

License
Proprietary. All rights reserved.

sql
Copy code

## (Optional) One-liners to add/commit/push
```bash
git add README.md
git commit -m "Add properly formatted README.md"
git push origin main
