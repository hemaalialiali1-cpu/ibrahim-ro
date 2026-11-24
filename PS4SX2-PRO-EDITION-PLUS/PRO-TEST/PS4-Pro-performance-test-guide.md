# PS4SX2 PRO - Performance test candidate (PS4 Pro)

This bundle is a source candidate, NOT a validated performance release. No claim of
zero lag or guaranteed full-speed emulation is made. A console build and per-game
tests are required.

## Build-time options already present in the project
The build script exposes JIT, Fastmem, and MTVU:
- PCSX2_VM_JIT=ON
- PCSX2_VM_FASTMEM=ON
- PCSX2_VM_MTVU=ON

These are enabled by default in the supplied build script. Avoid blindly changing
timing hacks or GPU synchronization globally; such changes can break games.

## Suggested PS4 Pro test matrix
1. Start with internal resolution 1x and the default frame limiter.
2. Test one game for 15 minutes in the same scene, noting FPS/overlay, audio,
   freezes, and visual errors.
3. Repeat at 2x only if 1x is stable and full-speed.
4. Compare the same scene after restarting, to distinguish shader-cache stutter
   from sustained performance problems.
5. Keep per-game notes; do not apply a setting globally if it breaks other titles.

## Updated compatibility-first default
The current source defaults the EE cycle rate to Normal (100%) for the whole library.
Mild and stronger underclock settings remain selectable for isolated per-game tests,
but should not be assumed to improve every title. The launcher Settings panel should
show Normal when no timing marker file is present.

## Current limitations
- This archive has not been compiled in a PS4 SDK environment here.
- No PKG was generated or tested on a PS4 Pro.
- The 2.6.3 desktop PCSX2 archive is a reference source, not a drop-in PS4 core.
- Performance depends on each game's CPU/GPU workload and compatibility.
