# Custom launcher profile photo

This source modification adds the user-provided portrait to the PS4SX2 Library home screen.

## Changes
- Adds `ps4/vm/assets/ui-png/profile_photo.png` (a resized copy of the supplied photo).
- Loads `profile_photo` through the launcher's existing UI image/texture pipeline.
- Displays the portrait in a framed profile panel on the Library home screen.
- Changes the visible game grid from four columns to three so the profile panel has room without covering game cards.

## Packaging
`ps4/vm/build-package.ps1` already copies every PNG from `ps4/vm/assets/ui-png` into `resources/ui`, so the new image is included automatically when the normal package script is run.

## Validation status
Source and asset paths were inspected. A PS4 PKG was **not** built or tested here; building still requires the OpenOrbis PS4 toolchain and the project's other build dependencies.
