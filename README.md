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
  calculations, newest first, 8 fixed-height rows per page with ▲ / ▼
  page arrows and a page indicator ("1–8 of 23"), saved between sessions.
  Tap a row to load its answer back into the calculator. History opens
  as a sheet over the keypad — the display stays visible — with a fixed
  44px header and its own scroll; tap the display again, or the sheet's
  "← Calc" button, to go back. There is no HIST button and no top bar.
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

Current release: **ConCalc 1.8** — version 1.8, versionCode 9, package
`com.mmrice.concalc`, minSdk 21, targetSdk 33, self-signed.

This is a new, personal app — a fresh package and a fresh signing key.
It will NOT update over the old builds (v0.1–v0.3):
uninstall the old app first, then install this one fresh.

The APK binary is not in this repo — GitHub's text push can't carry binaries.
Download `ConCalcV1.8.apk` from the chat / release and sideload it, or build
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
permission, no other permissions.

## Status

Untested on real Kompakt hardware as of v1.3.
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
