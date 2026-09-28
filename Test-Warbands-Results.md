# TRIBAL 2nd Edition — Test Warbands REULTS

A set of builds to run through New Recruit once `Tribal2E.gst` +
`Tribal2E-Core.cat` (the corrected version, re-downloaded just now — it
fixes a real bug: Skills and some Historical Rules had no limit stopping
you from adding the same one to a unit twice) are loaded. Each test names
a goal, what to build, and what should happen. Set the game/roster size to
**20 Honour** for all of these so cost limits never get in the way of
testing the structural rules (Test 1 and Test 7 are the exception, where
the Honour math itself is what's being checked).

Where something doesn't behave as described, that's exactly what I need
to hear back — paste the exact behaviour (or any error New Recruit shows)
and I'll fix the data.

---

## Test 0 — Minimum legal warband
**Goal:** confirm the Warlord's min=1 is enforced and nothing else is
forced on you.
- Build: an empty roster, add nothing.
- **Expect:** New Recruit should flag the roster as invalid/incomplete
  (0 Warlords, needs exactly 1).
  **Result:** Expected behaviour confirmed.  "Warband requires 1 selections more of Warlord."
- Now add exactly 1 Warlord and nothing else.
- **Expect:** roster becomes valid. Warlord shows 0 Honour cost before any
  Skills.
  **Result:** Expected behaviour confirmed. 
Top Bar of New Recruit List called Test does not show any honour values until at least 1 honour is allocated to a unit.

## Test 1 — Baseline legal warband (sanity + cost math)
**Goal:** everything loads, is selectable, and totals add up correctly.
- Warlord: Long Weapon, Skill: Agile → running total **1 Honour**
- tested, confirmed
- 1× Hero: Short Weapon, Skill: Cunning → **+2 Honour** (1 base + 1 skill)
- tested, confirmed
- 2× Warriors (Formation of 5): plain, no Skills → **+2 Honour**
- tested, confirmed
- On one of those Warriors Formations, add Skill: Fearsome → **+1 Honour**
- tested, confirmed
- 1× Marksmen (Formation of 5), Skill: Deadly Shot → **+2 Honour**
- tested, confirmed
- **Expect total: 8 Honour spent**, 12 remaining (out of 20). If the
  displayed total is anything else, tell me the number New Recruit shows
  and I'll trace which cost is wrong.
  **Result:** Expected behaviour confirmed. 

## Test 2 — Marksmen cap (max 2 Formations)
- Add a 3rd Marksmen (Formation of 5) after two are already in the roster.
- **Expect:** blocked / greyed out / flagged invalid at the 3rd.
- **Result:** Expected behaviour confirmed.

## Test 3 — Shaman cap + Shaman's restricted Skill list
- Add a 2nd Shaman after one is already in the roster.
- tested
- **Expect:** blocked at the 2nd (max 1 per warband).
- **Result:** Expected behaviour confirmed. 
- On the one legal Shaman, open its Skills list.
- **Expect to see:** the 11 "any unit" Skills plus Curse, Divination,
  Healing, Rat Cunning, Evil Eye (its 5 own Skills).
  **Result:** Expected behaviour confirmed.
  **Expect NOT to see:** Duellist, Long Shot, Tough, Berserker, Champion,
  Strong, Tactician, Concealment, Respected, Revered (all restricted to
  Warlord/Heroes only) — and no Weapon (Short/Long) choice at all.
  **Result:** Expected behaviour confirmed.

## Test 4 — Hero cap: the known gap
**Goal:** confirm (not fix) the limitation flagged in the README.
- Build a Warlord with **zero** Warriors or Marksmen Formations.
- Tested. Confirmed.
- Try adding 5+ Heroes anyway.
- Tested.
- **Expect (per the actual rulebook):** this should be illegal — you can
  only take 1 Hero per Formation of Warriors/Marksmen, so with 0
  Formations you should get 0 Heroes.
  **Result:** Allowed to add up to 20 heroes before honour cap was exceeded. No errors generated 
- **What the tool will actually do:** allow it, up to 20. This is the one
  constraint I deliberately left unenforced rather than ship an untested
  dynamic rule (see the README). If you'd like, once you've confirmed
  this is the only gap, I can build the proper scaling version and you
  can test that in isolation.
  **Result:** That is what happened. I want this fixed. if there when there are no other errors.

## Test 5 — Skill mutual-exclusion subgroups
5a. On a Warlord, try to add **both** Adept and Duellist (or Champion).
  Tested.
   **Expect:** blocked — only one of the three can be taken.
   **Result:** not blocked but works, when the check box for one is selected any active choice in that section **Weapon Mastery Skill** deselect. So this works as I want.
5b. On the same Warlord, try to add **both** Respected and Revered.
   **Expect:** blocked — only one of the two.
   **Result:** not blocked but works, when the check box for one is selected any active choice in that section **Card Pool Bonus Skill** deselect. So this works as I want.
5c. **Important one to watch closely:** give that Warlord Adept (from the
   exclusive group) plus 2 more ordinary Skills (e.g. Agile, Cunning) —
   3 Skills total, at the Warlord's max.
   - **Expect:** allowed, and the Skills group should now show as *full*
     (no more addable) — meaning the exclusive-group pick correctly
     counts toward the overall "up to 3" limit.
     **Result:** Expected behaviour confirmed.
   - **If instead** New Recruit lets you add a 4th Skill on top (i.e. it
     ignores the Adept pick when counting toward the max-3), that's a
     real structural issue with how I nested the groups — tell me exactly
     what happened here, this is the part of the file I was least certain
     of without live-testing it.
     **Result:** This error condition did not occur.

## Test 6 — Duplicate-Skill blocking (the bug just fixed)
6a. On a single Warriors Formation, try adding "Fearsome" a second time.
   **Expect:** blocked now (this was the bug — it wasn't blocked before).
   **Result:** Expected behaviour confirmed. Previous this was a a box with up and down arrows and a number, default of 0 and could be increased above 1. Now it is a check box.
6b. Add "Fearsome" to a **different** Warriors Formation in the same
   warband.
   **Expect:** allowed — the same Skill can be used by multiple different
   units, just not doubled up on one unit.
   **Result:** Expected behaviour confirmed.

## Test 7 — Historical Special Rules: eligibility, exclusivity, cost math
7a. On a Hero, try **both** Light Armour and Heavy Armour together.
   **Expect:** blocked — only one armour type per Unit.
   **Result:** Expected behaviour confirmed. Check boxes and only one can be on at a time. If the others is selected it deselects the other.
7b. Check a Warriors Formation's and a Marksmen Formation's Historical
   Rules options.
   **Expect NOT to see:** Heavy Armour or Chariots on either (Characters
   only). 
   **Result:** Expected behaviour confirmed.
   **Expect NOT to see:** Assegai on Marksmen or Shaman (they're
   armed with neither short nor long weapons).
   **Result:** Expected behaviour confirmed.
7c. Put Light Armour on 2 different units (e.g. a Hero and a Warriors
   Formation).
   **Expect:** 0.5 Honour each, **1 Honour total** — not 2.
   **Result:** Expected behaviour confirmed. Honour for that counts in 0.5 increments.

## Test 8 — Counting Coup's cross-unit-type cap (max 2 in the warband)
- Give Counting Coup to 2 Heroes, then try adding it to a Warriors
  Formation as well (a 3rd instance, spread across different unit types).
- **Expect:** blocked at 2, regardless of which unit types they're on.
- Also try adding Counting Coup twice to the *same* Hero.
- **Result:** Expected behaviour NOT confirmed. I was able to add Counting Coup to 3 heroes and to two warriors units and no error.
- **Expect:** blocked (max 1 per unit, separately from the max-2 total).
- **Result:** Selected via check boxes now so not able to be tested, but in effect is working.

## Test 9 — Rally Around the Flag (max 1 per warband)
- Give 2 different Heroes Rally Around the Flag.
- **Expect:** blocked at the 2nd — only one standard-bearer per warband.
- **Result:** Expected behaviour NOT confirmed. I was able to add Rally Around the Flag to 3 heroes and to two warriors units and no error.

## Test 10 — Warband-wide Historical Rules (once per warband each)
- First check: these five rules (Boasts, Raid from the Water, Stalking the
  Prey, Trophy Hunters, War Dance) now sit under a **Historical Rules**
  heading in the roster builder, not "Uncategorized".
- Tested Confirmed, works as expected.
- Try adding "War Dance" a second time (or bumping its quantity to 2).
- **Expect:** blocked.
- **Result:** not blocked but an error is generated which is fine.
- Now add Boasts, Trophy Hunters, and Raid from the Water all in the same
  warband (three *different* warband-wide rules together).
- **Expect:** allowed — nothing stops you combining different named
  rules, only repeating the same one (the book only advises against a
  couple of specific combinations in the rule text, it doesn't hard-block
  them).
- **Result:** Expected behaviour confirmed. 

---

## If something breaks that isn't listed here
The most useful thing you can send back is: which unit/Skill/rule, what
you clicked, and exactly what New Recruit did (an error message, a
greyed-out option, a cost that looks wrong, or something that *should*
have been blocked but wasn't). I can trace anything specific straight
back to the part of the generator that produced it.

No other faults found.
