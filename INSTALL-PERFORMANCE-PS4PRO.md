# PS4SX2 PRO Edition Plus — PS4 Pro setup

This archive contains the PS4SX2 source tree and the PS2 BIOS file supplied by the user.
It is **not** a prebuilt PKG and has not been built or tested on a PS4 console in this session.

## Install BIOS data

Launch the app once, then copy:

`userdata/PS4SX2/bios/scph10000.bin`

to:

`/data/PS4SX2/bios/scph10000.bin`

The BIOS is user data; the PKG builder intentionally does not embed BIOS or game images.

## Performance baseline

- Use the Release build with the PS4 build defaults: JIT, Fastmem and MTVU where enabled by the build configuration.
- Keep internal resolution at 1x while diagnosing slowdowns.
- Keep the frame limiter and shader cache enabled. The first pass through a scene can stutter while shaders compile; repeat the same scene after restarting the game before judging sustained speed.
- The global default EE timing profile is Normal (compatibility-first). This is the safest shared baseline for a mixed game library.
- To test a mild underclock, create `/data/PS4SX2/vm-ee-cycle-mild` and remove the normal/strong-underclock markers. To test the stronger underclock, create `/data/PS4SX2/vm-ee-cycle-underclock` and remove the normal/mild markers. Underclocking can alter timing, physics, audio, or compatibility; use it only as a per-game experiment and revert if anything regresses.
- To explicitly restore the normal profile, create `/data/PS4SX2/vm-ee-cycle-normal` and remove the other two markers.
- Do not enable EE cycle skip, SMC-skip, or fast-CDVD globally. These remain opt-in because they can reduce compatibility or fail to improve speed.

## Starting points by game

- God of War 1/2: 1x, Normal first; compare mild underclock only if the game is CPU-bound and repeatable tests show a gain. Keep MTVU only if it improves speed without regressions.
- Resident Evil 4 PS2: 1x, Normal first; prioritize stable gameplay and correct timing over upscaling.
- Racing games: 1x, Normal first; judge a repeatable race segment with multiple cars/effects. Revert any underclock if physics, controls, or audio timing changes.

These are diagnostic starting points, not guaranteed fixes. No setting can guarantee zero lag for every PS2 game on PS4 Pro.

## Validation

A PS4 SDK build and real-console tests are still required. Record the game serial/region, scene, profile, resolution, reported speed, audio behavior and repeatability before promoting a profile to a default.
