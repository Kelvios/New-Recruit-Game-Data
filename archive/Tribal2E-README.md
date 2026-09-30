# TRIBAL 2nd Edition — New Recruit data files

Two files, built from your `TRIBAL_KB.md` (Sections: PART WARBAND, PART SKILL,
PART OPTION, PART HIST):

- **`Tribal2E.gst`** — the game system: Honour as the cost currency, a `Unit`
  profile type (Wounds / Skills / Notes), and the five unit categories
  (Warlord, Heroes, Warriors, Marksmen, Shaman) plus a Historical Rules category with their force-level
  min/max constraints.
- **`Tribal2E-Core.cat`** — the catalogue: the five unit types, all 27 named
  Skills, and all 12 Historical Special Rules, wired up as shared entries
  with root links, following the same shared-entry + entryLink pattern as
  Kemp's `SimpleForce` example and the "How to New Recruit" guide.

To use them: in New Recruit's data editor, import/open `Tribal2E.gst` first
(this creates the game system), then open `Tribal2E-Core.cat` against it.
Both are plain, unzipped XML (`.gst`/`.cat`), matching what NR's "Add from
GitHub" / local-import expects.

## Scope: core rules only

This covers **core Tribal 2nd Edition** — enough to build and cost a
legal warband from the base book. It does **not** yet include the
**Primeval** (Neanderthal/Cro-Magnon/Denisovan/Early Hominid) or **Brutal**
(Renaissance gangs, 5 Points, Masked Vigilantes, Mob Rule, Wasteland
Warriors, Smog & Soot) faction supplements — those layer *Faction*-part
content on top of this same chassis as their own catalogues linked to this
`.gst`. Say the word and I'll build one or more of those next; each is its
own scoped job similar in size to this one.

## Modelling decisions worth knowing

A few places where the book's rule doesn't map onto a BattleScribe
constraint cleanly. I picked the option that keeps the tool honest rather
than silently wrong:

- **"1 Hero per Formation of Warriors/Marksmen"** — NOT automatically
  enforced. BattleScribe *can* do this kind of scaling limit via a
  modifier/repeat construct, but I didn't have a way to test it against
  the actual NR engine, so shipping an unverified version risked it
  silently failing in a way you'd never notice while building a list. I
  used a flat, generous cap (20) instead, and put the real rule in plain
  English on the Hero entry's Notes. **You'll need to eyeball this
  yourself** when building a roster. If you want, once you've got NR open
  I can walk through building the dynamic version with you and you can
  test it live.
- **Light Armour's "1 Honour per 2 Units"** is modelled as **0.5 Honour per
  Unit** — equipping 2 Units still costs 1 Honour total, but it's now a
  clean per-unit purchase instead of a "pick 2 units to share one token"
  mechanic BattleScribe has no native way to express.
- **Counting Coup's "max 2 Units in the warband"** IS reliably enforced —
  it's the same shared entry linked under both Warriors and Heroes, with
  one roster-wide max=2 constraint on the entry itself, so it caps
  correctly regardless of which unit type you attach it to.
- **"Character"** is read strictly as the book defines it in
  `T2E.WARBAND.THE-WARBAND` — Warlord and Heroes only. The Shaman (an
  OPTION-part addition) is therefore *not* eligible for general
  "Characters only" Skills (Duellist, Champion, Berserker, Strong, Tough,
  Long Shot) or the Warlord-only ones, only for its own 5 Shaman Skills
  plus the "any unit" ones. This is a judgment call where the book doesn't
  spell it out explicitly for the Shaman.
- **Card Pools skills** (Respected/Revered) and the **Historical Special
  Rules** are all included and costed, but per the book they only matter
  if you and your opponent have agreed to use that optional rule/sub-system
  — the tool doesn't know which house rules your table is using, so it
  offers everything and trusts you to only pick what applies.
- A couple of rule *interactions* are noted in text only, not hard-blocked:
  Stalking the Prey vs. the Concealment Skill, and War Dance/Boasts vs.
  Card Pools (the book just recommends against combining them).
- Flavour text (the saga quotations, Iliad excerpts, bibliographies) was
  deliberately left out of every rule description — only the functional
  mechanics are reproduced, since that's what a roster tool actually
  needs and your KB's own README flags this as licensed text to keep
  private.

## Structure at a glance

- Skills, weapon-type markers, and Historical Special Rules are each
  defined **once** as a shared entry, then linked in wherever they're
  eligible — so editing a Skill's text or cost in one place updates it
  everywhere it appears.
- Each unit entry (Warlord/Hero/Warriors/Marksmen/Shaman) has its own
  `Weapon (choose 1)` group where relevant, a `Skills (choose up to N)`
  group with the correct per-unit-type eligible list (including the
  Adept/Duellist/Champion and Respected/Revered exclusivity subgroups
  where more than one option in the exclusive set is actually available),
  and a `Historical Special Rules` group for the per-unit purchases
  (Armour, Assegai, Cavalry, Chariots, Counting Coup).
- Warband-wide, once-per-game Historical Rules (Boasts, Raid from the
  Water, Stalking the Prey, Trophy Hunters, War Dance) sit as root-level
  picks under their own "Historical Rules" category, each capped at 1 per roster. Rally Around the Flag is a free
  pick under Heroes, capped at 1 per roster.

## Before you trust it for a real game

Everything here validates as well-formed XML and every ID cross-references
correctly, and the element ordering, attribute shapes and shared-entry/
entryLink pattern all match confirmed, real, working BattleScribe/New
Recruit files (I checked against both the `SimpleForce` teaching example
and several production BSData Warhammer 40k catalogues to nail down
schema details I wasn't 100% certain of from the guide alone). What I
*can't* do from here is actually click through it in New Recruit's live
roster builder — so before you rely on it, I'd open it there and sanity
check: the Skills counts and exclusivity groups behave as expected, the
Historical Rules costs look right, and the Hero cap reminder above.
