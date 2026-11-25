# PS4SX2 PRO — game-focused test profiles

Target hardware: PlayStation 4 Pro (CUH-70xx/71xx/72xx family).

These are **test starting points**, not guaranteed fixes. The PS4SX2 port is alpha;
there is no honest way to promise zero lag for every PS2 title. Do not force one
speedhack profile onto every game.

## Shared baseline (all titles)

- Build: Release, JIT=ON, Fastmem=ON, MTVU=ON using `ps4/vm/build.ps1` defaults.
- Internal resolution: 1x for the first test. Try 2x only after 1x maintains full
  emulation speed for a repeatable 10–15 minute scene.
- Keep the frame limiter enabled; do not use frame-skip as a general performance fix.
- Keep game audio enabled. Audio crackle is useful evidence of emulation falling
  behind; muting audio does not make the game run faster.
- Leave EE timing at Normal/compatibility first. Test mild and then stronger EE
  underclocking separately only when a repeatable CPU bottleneck is measured; these
  modes can break timing-sensitive gameplay.
- Keep shader cache enabled. The first traversal may stutter while shaders compile;
  repeat the same scene after a full restart before judging sustained performance.
- Do not change multiple settings between runs. Record one change at a time.

## God of War (2005) and God of War II (2007)

Starting point: shared baseline, 1x internal resolution, Normal/compatibility EE
profile. These titles can stress both the EE/VU path and GS effects. If the game
runs below full speed at 1x, do not increase resolution. Compare MTVU ON/OFF only
as an isolated diagnostic; keep ON if it improves speed without visual/timing
regressions. Do not enable SMC-skip or undocumented timing hacks globally.

## Resident Evil 4 (PS2)

Starting point: shared baseline, 1x internal resolution, Normal/compatibility EE
profile. Prioritize stable gameplay and correct timing over a higher upscale. Test
2x only after the same combat/area scene remains full speed at 1x. If a scene has
visual glitches, record the exact area and whether it occurs after a cold boot or
only on the first shader-cache pass.

## Racing games

Starting point: shared baseline, 1x internal resolution, Normal/compatibility EE
profile. Test a repeatable race segment with several cars and effects on screen.
Prioritize consistent emulation speed and audio over resolution. Test mild EE underclocking
only as a separate run; revert if physics, input response, or audio timing changes.

## Heavy / demanding titles

Use the same conservative 1x baseline. If speed remains below full after a second
run with a warm shader cache, classify the bottleneck using the in-game performance
overlay and logs (EE, GS, VU, GPU). Do not assume that a GPU-looking slowdown is
fixed by EE underclocking, or vice versa.

## Required test report

For each game, record: exact title/region/serial, scene, internal resolution, EE
profile, MTVU state, first-run vs warm-cache run, reported speed/FPS, audio behavior,
visual issues, and whether the issue is repeatable. A profile should only become a
default after it passes multiple scenes and does not regress other games.

## Build and validation status

The source archive is not a prebuilt PKG. Build with the documented PS4 SDK and
validate the resulting package on the target console. A successful compile/package
check is not proof of full-speed emulation. No console performance test is claimed
by this document.
