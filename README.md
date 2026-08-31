# MacsyZones - local Pro fork

MacsyZones is a macOS window-management utility inspired by Windows FancyZones. It lets you create layouts, divide them into zones, and snap windows into those zones.

This repository is a personal fork of [MacsyZones](https://github.com/rohanrhu/MacsyZones).

## Changes in this fork

- Removed the recurring donation reminder popup.
- Added a `LOCAL_PRO` build mode for personal Debug and Release builds.
- Local Pro builds display `MacsyZones Pro` and do not require a license key.

`LOCAL_PRO` is a local fork build setting. It does not create or represent an official commercial license from the original MacsyZones project.

## Requirements

- macOS 11.5 or newer
- Xcode with the macOS SDK
- An Apple Developer signing identity for normal use with Accessibility permissions

## Build

Open the project in Xcode:

```sh
open MacsyZones.xcodeproj
```

Select the `MacsyZones` scheme and choose `Product → Build` (`⌘B`). The Debug and Release configurations already enable `LOCAL_PRO`.

The command-line equivalent is:

```sh
xcodebuild \
  -project MacsyZones.xcodeproj \
  -scheme MacsyZones \
  -configuration Debug \
  build
```

The resulting application is created at:

```text
Build/Products/Debug/MacsyZones.app
```

If Xcode reports a signing error, open the `MacsyZones` target's `Signing & Capabilities` settings and select your own Apple Developer Team. A build made with `CODE_SIGNING_ALLOWED=NO` is useful for compile checks but may not work correctly with macOS Accessibility permissions.

## Build and ship into `/Applications`

For a local release build, first select your own Apple Developer Team in the target's `Signing & Capabilities` settings, then run:

```sh
xcodebuild \
  -project MacsyZones.xcodeproj \
  -scheme MacsyZones \
  -configuration Release \
  build
```

The release application is created at:

```text
Build/Products/Release/MacsyZones.app
```

Quit any currently running MacsyZones instance before replacing it. You can install the new build in Finder by dragging `MacsyZones.app` into `/Applications` and choosing `Replace`.

The equivalent Terminal command is:

```sh
ditto --rsrc --extattr --acl \
  Build/Products/Release/MacsyZones.app \
  /Applications/MacsyZones.app
```

Launch the installed build with:

```sh
open -n /Applications/MacsyZones.app
```

Do not use `CODE_SIGNING_ALLOWED=NO` for the installed build. macOS may refuse to grant Accessibility access to an unsigned or incorrectly signed application.

## Install and Accessibility permission

After installing the application, allow it to control the computer:

1. Open `System Settings → Privacy & Security → Accessibility`.
2. Click `+`.
3. Press `⌘⇧G` and select `/Applications/MacsyZones.app`.
4. Enable MacsyZones and restart the app.

If MacsyZones is already enabled in Accessibility but still asks for permission, quit the app and run:

```sh
tccutil reset Accessibility MeowingCat.MacsyZones
```

Then launch MacsyZones again and enable it in Accessibility if prompted.

The application needs Accessibility access because macOS requires explicit permission for window management and accessibility APIs.

## Contributing

Issues and pull requests are welcome. Keep changes focused and preserve the upstream license and copyright notices.

## License

This fork is distributed under the [GNU General Public License v3.0](LICENSE).

The original MacsyZones copyright and license notices remain in the source files. Modified versions must remain under GPLv3 and include the corresponding source code and build instructions.
