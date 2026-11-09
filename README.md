# ConCalc

Construction calculator, in stock Mudita style.
For use on a Mudita Kompakt (4.3" E Ink, 800x480)
and any Android phone.

- Feet-inch-fraction math, just as you say it: `6 Feet 9 Inch 1/2` = 6' - 9 1/2"
- Fractions to 1/64, decimal feet/inches, yards, metric
- Rise / Run / Diag / Pitch, Hip/Val, Jack, Rake-Wall, Stair layout,
  circles/arcs, board feet, concrete, flooring, drywall, studs, roofing,
  baluster spacing, cost, memory, history
- One value at a time on a single display.
  Punch Diag and you get Diag. Punch it again and you get Diag again.
  No tables, no scrolling, no panels underneath.
- History (replaces Tape): tap the display to open a paged list of past
  calculations, newest first, 8 fixed-height rows per page, saved between
  sessions. Tap a row to load its answer back into the calculator. History
  opens as a sheet over the keypad — the display stays visible — with two
  tabs at the top, History and Guide (active tab solid black); tap the
  display again to go back. There is no HIST button and no top bar. A
  vertical scroll bar runs down the right edge of the list (thin light
  track, thick black thumb, ▲ at the top and ▼ at the bottom — those
  triangles are the pager buttons; tap the track or drag the thumb to
  move). There is no page label — the ▲/▼ pager and the scroll bar
  are the navigation.
  History auto-prunes to the last 100 entries — oldest drops automatically,
  so there is no wipe control. (The calculator's Clear All, Conv+×, is
  separate: it resets stored riser/tread/o.c./wt-vol defaults.)
- Conv is the second-function key: press it and the keys that have a
  second function swap their label to show it (a small dot marks those
  keys); press it again, or use the second function, and the labels go
  back. No small-print second functions on the face. While Conv is on,
  the indicator in the sub row under the display reads CONV.
- Clear lives on the backspace key, labelled "⌫ / C" (the ⌫ is set a
  little larger than the key text): tap deletes one character, hold
  ~0.6 seconds clears the display, hold again clears temporary values.
  There is no Clear button. The CONV / RCL / MEM indicators live in the
  sub row under the display value, so there is no top bar at all — the
  display and keypad get the room.
- Mudita style: monochrome, paper-white, flat keys, no ads, no tracking,
  no pop-ups. Works offline once loaded.

## Files

- `index.html` — the whole calculator as one self-contained web page.
  Open it in a browser, or Add to Home Screen on Android.
- `android/` — the Android wrapper that makes the APK:
  - `AndroidManifest.xml` — package `com.mmrice.concalc`, label ConCalc
  - `src/com/mmrice/concalc/MainActivity.java` — single Activity, full-screen
    WebView loading `android/assets/index.html`, JavaScript on, no permissions
  - `assets/index.html` — same file as `index.html` at the repo root
- `icon.svg` — launcher icon: two overlapping triangles — a speed square
  overlayed on a gable roof pitch. Monochrome black on paper
  #F4F1EA, no text. Centred in the 512 frame with even margins
  (left/right 40 px, top/bottom 141 px — the design is wide and
  shallow, so the top/bottom paper is larger, but equal).
  The APK build uses PNGs rendered from this at mdpi 48, hdpi 72,
  xhdpi 96, xxhdpi 144, xxxhdpi 192 px (standard 48 dp legacy
  launcher icon; no adaptive icon — a launcher mask would clip
  the wide design's tips, and the Kompakt uses plain PNGs).
  (PNGs are not in this repo — this push is text files only.)
  A Mudita stock-tile variant (81 px tile, 40 px symbol, 19 px
  radius border) is saved as an option in the workspace, not used.

## APK

Current release: **ConCalc 1.19** — version 1.19, versionCode 20, package
`com.mmrice.concalc`, minSdk 21, targetSdk 33, self-signed.

This is a new, personal app — a fresh package and a fresh signing key.
It will NOT update over the old builds (v0.1–v0.3):
uninstall the old app first, then install this one fresh.

The APK binary is not in this repo — GitHub's text push can't carry binaries.
Download `ConCalcV1.19.apk` from the chat / release and sideload it, or build
it yourself below. Keep the keystore at
`~/workspace/apk-build/concalc-personal.keystore` — updates must use the
same key.

## v1.0 — audited against the reference guide

v1.0 (and v0.3 before it) was checked key-by-key against a standard
construction calculator reference v3.1 and fixed where it differed. The
big ones:

- Numbers are plain until tagged: type a number, then Feet/Inch/Yds/m/cm/mm
  tags it. An untagged number is a plain count (so `3 × 15 ft` is a length,
  and `25% of 1575` is plain math).
- Pitch: dimension = in/12, plain number = degrees, Conv+Pitch = ratio,
  % then Pitch = grade. Pressing Pitch cycles in → degrees → % grade →
  slope, as the reference does.
- Circle: enter a Diameter, press Circ for DIA, again for AREA, again for
  CIRC. Arc (Conv+Circ): diameter + arc length → degrees; diameter +
  degrees → arc length.
- Stair: uses stored Rise/Run + desired riser/tread; pressing Stair steps
  through the reference 12 results (riser, risers, overage, tread, treads,
  overage, stringer, incline, run, rise, stored riser, stored tread).
- Jack and Rake-Wall: first press shows the stored on-centre spacing, then
  each press gives the next jack / stud, down to 0 / base, then the angle.
- Weight: plain number = pounds; Conv+Weight converts a volume to weight
  using the stored weight-per-volume (default 1.5 Ton/cu yd, Conv+0 to
  change, Rcl+0 to recall); Weight then cycles Ton → LB → MET Ton → kG.
- Cost (Conv+·): quantity × unit price; board-feet quantities are priced
  per Mbm (per 1000 BF).
- Tape: Rcl+= (or Conv+=) opens it — total first, + / − scroll the last
  20 entries, = exits and you can keep calculating from the total.
- Prefs (Conv+%): the reference six settings — fractional resolution, area
  display, volume display, meter linear display, decimal degree display,
  fractional mode. % steps settings, + / − changes the option, On/C exits.
  Conv+1/2/3/4/6/8 temporarily changes fractional resolution.
- On/C: first press clears the display, second press clears temporary
  values (Rise/Run, etc.). Clear All (Conv+×) resets stored values to the
  reference defaults (riser 7-1/2", tread 10", o.c. 16", wt/vol 1.5 Ton/cu yd).
- Memory: Rcl+M+ recalls the total; M+ after recall shows the average,
  then the count. Rcl+Rcl shows the total and clears memory.
- Repeated presses cycle only where the reference says so (above). Diag,
  Hip/V and the rest stay one-value-at-a-time: press again, same answer.

Still open / judgement calls: the irregular-jack lengths in the reference
worked example don't match the plane-B common-difference formula this
build uses (see the code comments) — flag if it matters on a real roof.
Flooring has no key in the reference, so the old Flooring solver was removed;
flooring is area × (1 + waste%) with the % key. The "Fractional Mode:
COnSt" preference is stored but the reference doesn't define its effect in
the pages read, so it changes nothing yet.

## Sideload on a Mudita Kompakt

1. Copy the APK to the computer with Mudita Center installed.
2. Connect the Kompakt by USB and open Mudita Center.
3. Use Mudita Center's sideload / install-APK option and pick the APK.
4. Allow installation from this source if prompted — Android will warn it's
   from an unknown developer because it's self-signed. That's expected.
5. Works fully offline, including in Offline+ mode. Sideloaded apps are
   reached through Settings on the Kompakt, not the home screen.

## Build the APK yourself

Needs JDK 17 and the Android SDK (build-tools 33.0.2, platform android-33).
Build with aapt2 → javac → d8 → aapt2 link → zipalign → apksigner,
signing with the personal keystore
(`~/workspace/apk-build/concalc-personal.keystore`, alias
`concale-personal`). No Google services, no internet
permission. The one permission is VIBRATE (v1.18): the short
haptic pulse on key presses needs it declared, or the WebView
vibration call does nothing. It is a normal permission, granted
automatically at install.

## Status

Untested on real Kompakt hardware as of v1.3.
v1.19 is UI only, no math changes: the "Page X of Y" label at the bottom of the History tab is gone entirely — the ▲/▼ pager and the scroll bar are the navigation now, and the layout closes up cleanly with no blank gap left behind.
v1.18 is UI only, no math changes: pressing a key now shows it — the key inverts (solid black with white text) while held, and keys that are already solid at rest (Conv when off, backspace, =) invert the other way, white with black text, so a press is always visible; the same inversion applies to the History/Guide tabs, the ▲/▼ pager triangles and History rows. A press also gives one short haptic pulse (navigator.vibrate, 10 ms, feature-detected so nothing breaks where vibration is unavailable) — the app now declares the VIBRATE permission, which the WebView vibration call needs; it is a normal permission, granted automatically at install. Pressed state never sticks (cleared on release, leave or cancel) and never shifts the layout.
v1.17 is UI only, no math changes: an invalid selection never shows an error message — pressing a solver key with nothing to solve shows its name as a label prompt instead (Pitch, Rise, Run, Diag, Hip/V, Jack, R/Wall, Stair, Circle, Arc, Weight, Cost, ...), and typing clears the label and the entry continues. Keys with no prompt to show (memory recall with an empty memory, Conv conversions of a plain number) stay fully silent: no message, no display change. Confirmations of something done successfully (Memory · cleared, Cleared) are kept. The guide's Roof section now shows the Pitch prompt.
v1.16 is UI only, no math changes: the label on the left of the display stays blank during normal entry — no more "Ready" / "Entering" / "Entered" and no arithmetic echoes — it only shows when something is worth naming (a solved value's name, like Diagonal or Run, or a message like "Store a Rise and a Run first"). The CONV / RCL / MEM indicators no longer push the UI down: they always take their space in the sub row (invisible until armed) and the sub row has a fixed minimum height, so the display and keypad stay exactly where they are whether the indicators are showing or not.
v1.15 fixes the triangle solver so it works in any order: store any two of Pitch, Rise and Run, then press the third key to solve for it — Pitch (6 in) + Rise (12 ft) then Run gives 24 ft, Run (12 ft) + Rise (12 ft) then Pitch gives 12 in. Entering a Rise no longer wipes the stored pitch, and entering a leg with a pitch stored solves the missing leg. The guide's Roof section now says any two, with the Pitch+Rise then Run example worked through. Also the History scroll bar now matches the stock bar: the black thumb is the same width as the track (it no longer sticks out wider), the ▲/▼ are plain small solid triangles with no button box, and an arrow shows as a dot-matrix dither at the end it cannot go past (▲ on the first page, ▼ on the last) and returns to solid black when you can move again — black dots on white, no grey pixels, since the display is black and white only.
v1.14 is UI only, no math changes: History and Guide are now two tabs at the top of the sheet (History / Guide, active tab solid black) — the ⚙ Guide pill and the Guide's "← History" button are gone; tap the display to open the sheet (History tab first), tap it again to close it from either tab. The header count ("1–8 of 12") is gone — the page info stays at the bottom in the pager. The History list has a vertical scroll bar down its right edge (thin light track, thick black thumb, ▲ at the top end and ▼ at the bottom end — those triangles are the pager buttons) — tap the track or drag the thumb to move through History. The bar is hidden entirely when there is nothing to scroll (empty, or everything fits on one page); the thumb is sized by the visible fraction (8 entries shown out of the total), so more entries means a smaller thumb.
v1.13 is UI only, no math changes: the History header is a 3-column grid so the title sits truly centred and the pills sit centred in the 44px header; the History list never scrolls — a page is exactly the 8 rows that fit, and the ▲/▼ pager buttons are the only way to move between pages; the "← Calc" back button is gone — tap the display to open History, tap it again to close it. The Guide's own "← History" button stays.
v1.12 is UI only, no math changes: 3px outlines on ALL keys — plain keys, operators and the guide key icons alike (Mitch, after seeing the stock calculator's thick operator outlines). Solid keys stay solid with no outline ring: Conv when off, backspace / C, and =. Still monochrome, no fill, no colour.
v1.11 is UI only, no math changes: the Conv key goes back to its v1.9 look — solid black when off, plain when armed (v1.10 had flipped it and Mitch asked for the old way back); the backspace / C key gets the same treatment, solid black as its resting style; and the key outlines are a little bolder than v1.10 — plain keys 1.5px, operators 2px, still thin monochrome black with no fill. = stays solid black as before.
v1.10 is UI + guide, no math changes: the unit cap under the display now
names only the units actually on screen (18' - 7 1/2" shows "FEET - INCH",
7" shows "INCH", 18' shows "FEET", a plain number shows nothing); the Conv
key's lit state is fixed (plain until armed, solid black when armed — =
stays solid black as before); every key now has a thin black outline, no
fill. The in-app user guide is rewritten as a thorough second-person
step-by-step guide: 15 short sections, "Press: … / You see: …" one action
per line, with the key presses shown as little key icons, and every worked
example checked against the calculator itself. Conversion is documented as
Conv first, then the unit.
v1.9 fixes one thing Mitch found while testing v1.8: pressing a different
unit key after a value is already tagged now converts it — 18 + Inch, then
Feet, shows 1′ - 6″, and 6 + Feet, then Inch, shows 72″. Pressing the same
unit key again still raises the dimension instead (Inch, Inch = square
inches, again = cubic inches), and entering a value still keeps the unit
entered (12 + Inch stays 12″). The in-app user guide is unchanged in v1.9 —
a thorough step-by-step rewrite is coming in a later release.
v1.8 fixes four things Mitch found while testing v1.7: only the display
value is copyable — long-press copy and text selection are locked down
everywhere else; entering a value keeps the unit entered (12 + Inch
shows 12\u2033, not 1\u2032); feet-and-inches values show a dash between
the parts (12\u2032 - 7 \u215e\u2033); and a user guide was added behind a
settings pill in the History header. No math changes. Core math spot-checked
(6' 9 1/2", 6/12 rafter, 9 ft stairs, 10x10 ft x 4" concrete), and
v1.0 passed 50/50 headless tests against the reference worked examples.
v1.7 is UI only, no math changes: tap the display to open History (no HIST button), backspace is now "⌫ / C" — tap deletes one character, hold ~0.6s clears the display, hold again clears temporary values — so there is no Clear button and no top bar at all; the CONV / RCL / MEM indicators moved into the sub row under the display value, the Conv indicator reads CONV (not SHIFT), and the display and keypad get the freed space (with a comfortable margin, not flush to the top).
v1.6 is a one-bug fix, no math changes: the FEET · INCH unit cap is pinned to the right of the display — in v1.5 it jumped to the left whenever the solver sub line was empty, because the row is space-between and the cap became the sole flex child. v1.5 is UI only, no math changes: the display shows the value only — the
explanatory subtext under it is gone (no unit conversions, no pitch
explanation, no instructions); the sub line carries only the solver
position ("1 of N") when stepping through multi-result solvers. Clear
moved to the top-right corner of the face (top bar) and no longer has a
row of its own, so the keypad rows are taller. Styling follows the stock
calculator inspo: airy rows, plain-text keys with no fill or border,
operators in thin outlined rounded squares, = solid black; 5 columns
stay, and Clear stays top-right.
v1.4 is UI only, no math changes: Conv swaps key labels instead of small-print second functions (dot marks keys with a second function), Clear is a regular single key like the others, keys are bigger with more air, History is a sheet over the keypad (display stays visible, fixed 44px header, own scroll), and multi-result solvers now step through all their answers — Concrete/Bd Ft/etc. used to stay stuck on item 0 while advertising "1 of N". v1.3 brings History into line with Mudita Mindful Design: fixed-height rows, discrete paged scrolling (8 per page, ▲/▼ arrows, page indicator), one header row shared by the calculator and History screens, no grey text, no dark mode, larger second-function labels in black, Clear key 44px. The wipe control is removed — history auto-prunes to the last 100. v1.2 replaces Tape with a full History screen (HIST button, top-left of the display: a list, newest first, tap a row to reuse its answer, saved between sessions) and renames the On/C key to Clear (same behaviour). v1.1 changed only the launcher icon.
Personal project, not associated with any business.
