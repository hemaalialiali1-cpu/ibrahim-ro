# PS4SX2 PRO - customization notes

- Replaced the PS4 package ICON0 artwork with the new purple/cyan PS4SX2 PRO cover.
- Updated launcher accent colors and navigation SVG assets to a coordinated purple/cyan theme.
- Preserved the existing profile-photo asset, game-cover loading behavior, emulator code, and build workflow.
- No speculative audio-thread or timing-hack changes were made: the supplied source alone does not prove a safe fix for the reported audio-mode behavior or game-specific slowdowns.
- Build remains a GitHub Actions task using the repository's existing workflow. A successful source archive check is not the same as a successful PS4 PKG build.
