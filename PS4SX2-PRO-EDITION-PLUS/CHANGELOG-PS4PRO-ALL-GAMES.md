# PS4SX2 PS4 Pro — all-games compatibility update

This source update changes the shared EE timing baseline from a mild underclock to
Normal (100%) so timing-sensitive games are not globally forced into a speedhack.
The launcher Settings panel now also displays Normal when no EE timing marker exists.
Mild and stronger underclock modes remain available for isolated experiments.

Other existing build options (JIT, Fastmem, MTVU, Vulkan, shader cache) are preserved.
No new claim is made that these options eliminate lag. This change is intended to
reduce avoidable compatibility/timing regressions across a mixed library, not to
magically raise every game's emulation speed.

## Validation status
- Source-level edits applied.
- Whitespace/diff checks performed when packaging.
- No PS4 SDK build, PKG build, or real-console game test was performed in this session.

## In-game save states and cheat switch
- Added a controller-operated in-game Save State / Load State action with ten per-game slots. Left/Right selects the slot; X saves or loads the selected slot.
- Enabled the existing PCSX2 save-state pipeline for the interpreter-only PS4 VM. The VU JIT freeze hook is a no-op in this build because interpreter VU registers and execution state are already serialized by `vuMicroFreeze()`.
- Added an in-game master switch for PNACH cheat support. Cheat files are read from `/data/PS4SX2/cheats` using the PCSX2 serial/CRC filename convention; this switch enables/disables all detected PNACH groups for the running game together; individual cheat-group selection is not exposed in the PS4 menu yet.
- This source change has not been built with the OpenOrbis PS4 SDK or tested on a PS4 Pro. Save-state compatibility and game-specific cheat behavior still require device testing.
