# ConCalc

Construction calculator, in stock Mudita style.
For use on a Mudita Kompakt (4.3" E Ink, 800x480)
and any Android phone.

- Feet-inch-fraction math, just as you say it: `6 Feet 9 Inch 1/2` = 6' 9 1/2"
- Fractions to 1/64, decimal feet/inches, yards, metric
- Rise / Run / Diag / Pitch, Hip/Val, Jack, Rake-Wall, Stair layout,
  circles/arcs, board feet, concrete, flooring, drywall, studs, roofing,
  baluster spacing, cost, memory, paperless tape
- One value at a time on a single display.
  Punch Diag and you get Diag. Punch it again and you get Diag again.
  No tables, no scrolling, no panels underneath.
- Conv is the Shift key for the small-print second functions.
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
- `icon.svg` — speed-square launcher icon, monochrome black on paper #F4F1EA.
  The APK build uses PNGs rendered from this at mdpi/hdpi/xhdpi/xxhdpi/xxxhdpi.
  (PNGs are not in this repo — this push is text files only.)

## APK

Current release: **ConCalc 1.0** — version 1.0, versionCode 1, package
`com.mmrice.concalc`, minSdk 21, targetSdk 33, self-signed.

This is a new, personal app — a fresh package and a fresh signing key.
It will NOT update over the old builds (v0.1–v0.3):
uninstall the old app first, then install this one fresh.

The APK binary is not in this repo — GitHub's text push can't carry binaries.
Download `ConCalcV1.0.apk` from the chat / release and sideload it, or build
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

Untested on real Kompakt hardware as of v1.0. Core math spot-checked
(6' 9 1/2", 6/12 rafter, 9 ft stairs, 10x10 ft x 4" concrete), and
v1.0 passed 50/50 headless tests against the reference worked examples.
Personal project, not associated with any business.
