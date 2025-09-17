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

PROJECT STRUCTURE
nickeltap/

index.html

style.css

script.js

chad-nickel.png

tap-sound.mp3

TESTING CHECKLIST

Tap squish is instant, no lag at 10 taps/sec

Team selection works and persists

Streak system and stage escalation messages appear at correct tap counts

Multiple browser tabs sync with same global totals

Mobile works: no scroll/zoom, haptics, sound unlocks on first tap

Share button works on mobile and desktop

LICENSE
Proprietary. All rights reserved.
