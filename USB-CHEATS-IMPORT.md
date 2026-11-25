# USB cheat-file import (PS4SX2)

The in-game pause menu includes **Add cheat files from USB**. The importer accepts PCSX2 `.pnach` files and copies the selected file into the emulator's active `EmuFolders::Cheats` directory (`/data/PS4SX2/cheats` in this PS4 profile).

## USB layout

The scan checks the root and these common folders on mounted USB devices `/mnt/usb0` through `/mnt/usb7`:

- `/`
- `/cheats/`
- `/patches/`
- `/PS4SX2/cheats/`

Files must have the `.pnach` extension and be no larger than 1 MiB. Up to 64 matching files are listed. The file list is scanned when the submenu opens; press **Triangle** to refresh it after connecting or changing a USB drive.

## Controller steps

1. Pause the game with **L3 + R3**.
2. Highlight **Add cheat files from USB** and press **Cross**.
3. Use **Up/Down** to choose a `.pnach` file.
4. Press **Cross** to copy it into the emulator's cheats folder and reload the current game's cheat list.
5. Press **Circle** to return to the pause menu.

After import, the current game's detected cheat groups are selected and cheats are enabled. A file only takes effect if its PNACH serial/CRC matches the running game and its contents are valid for that game. This importer does not generate cheat codes or validate that a code is safe for a particular game.

## Validation status

The menu-state packing round-trip was tested locally. This source was not built with the PS4 SDK and the USB mount/import flow has not yet been tested on a physical PS4; treat it as a source change pending a PS4 build and device test.
