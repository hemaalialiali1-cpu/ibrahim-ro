# PS4SX2 PRO Edition — upgrade audit

## Target
PS4 Pro. This is a source-level first pass, not a tested PKG.

## Changes in this package
- Applied a new graphite / violet / cyan visual identity to the launcher and in-game menu in `ps4/vm/GameMenu.cpp`.
- Updated the launcher identity text to `PS4SX2 | PRO EDITION`.
- No emulation timing, memory, GPU synchronization, or game-compatibility behavior was changed in this visual pass.

## Findings from the supplied sources
1. `PS4SX2` is an experimental PS2 emulator port. Its own README states that compatibility and speed vary by game and full-speed emulation is not guaranteed.
2. The build already exposes JIT, Fastmem, and MTVU switches. The PowerShell build defaults them to ON, while the CMake option declaration for Fastmem defaults OFF; the WSL build script explicitly passes the environment value (default ON). Keep this discrepancy in mind when reproducing builds.
3. The supplied `ps4-kit` is a shared PS4 runtime/toolchain/Mesa/RADV base, not an emulator core. It contains newer runtime, diagnostics, GPU, and WSI work. It is not a safe drop-in copy: the current PS4SX2 tree has its own toolchain/runtime/VideoOut path and a different Mesa build contract.
4. `ps4-kit/docs/gpu-thread-performance.md` reports that moving Vulkan command recording to another thread can help when the render thread alone is saturated, but can make performance worse when emulated CPU threads are already the bottleneck. Therefore, blindly enabling a driver thread is not a safe universal optimization.
5. The kit's profiling and diagnostics are valuable for the next phase: measure EE/VU, GS, audio, I/O, and frame pacing on the PS4 Pro before changing scheduling or synchronization.

## Next engineering phase
- Port selected diagnostics/profiling pieces from `ps4-kit` behind build-time switches.
- Benchmark JIT/Fastmem/MTVU combinations on the PS4 Pro and compare frame-time percentiles, not only average FPS.
- Inspect shader-cache misses, GS queue waits, audio underruns, and storage stalls.
- Only then selectively migrate compatible runtime/Mesa/WSI changes.
- Add per-game profiles with conservative defaults and a safe fallback profile.

## Build and validation status
This environment does not contain the required OpenOrbis toolchain, PS4 libc++ sysroot, and PS4 Mesa static libraries described by the source README. I therefore cannot honestly claim that an EBOOT/PKG was built or tested on hardware here. The visual source edit must be compiled and checked on the target development environment before installation.

## Important limitation
No source change can guarantee zero lag for every PS2 game on PS4 Pro. The practical goal is to reduce avoidable stalls and maximize speed while preserving timing and compatibility.
