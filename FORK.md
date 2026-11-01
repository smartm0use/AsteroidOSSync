# AsteroidOS Sync (Fork)

This repository is an unofficial fork of [AsteroidOS Sync](https://github.com/AsteroidOS/AsteroidOSSync). It integrates fixes for compatibility with modern Android versions (Android 12–16) and quality-of-life improvements while upstream pull requests are pending.

## Included Improvements

This fork integrates the changes proposed in the following upstream pull requests:

- **Build Restoration ([PR #233](https://github.com/AsteroidOS/AsteroidOSSync/pull/233))**: Vendors EasyWeather 1.3 sources locally (JitPack dependency no longer resolves) and fixes a Java variable-scope issue in `SynchronizationService`.
- **Dimensionless App Icons ([PR #232](https://github.com/AsteroidOS/AsteroidOSSync/pull/232))**: Assigns a 48 dp fallback to drawables without intrinsic dimensions (e.g. `ColorDrawable`), preventing startup crashes and reducing memory allocation.
- **Location Permissions on Android 12+ ([PR #234](https://github.com/AsteroidOS/AsteroidOSSync/pull/234))**: Ensures `ACCESS_COARSE_LOCATION` and `ACCESS_FINE_LOCATION` are requested together during onboarding, complying with Android 12+ requirements.
- **Watch Battery in Notification ([PR #235](https://github.com/AsteroidOS/AsteroidOSSync/pull/235))**: Displays the connected watch's battery level in the ongoing notification (e.g. `Connected to dory (battery 73%)` / `Connesso a dory (batteria 73%)`).
- **Bluetooth Handling**: Fixes Bluetooth error handling, permission checks before BLE scans, and triggers the system dialog when Bluetooth is disabled.

## Installation & Updates

Pre-built, signed APKs are available on the [GitHub Releases](https://github.com/smartm0use/AsteroidOSSync/releases) page.

> [!IMPORTANT]
> This fork is signed with a personal certificate different from F-Droid's.
> You must **uninstall the official F-Droid version** before installing this APK. Subsequent releases of this fork can be updated in-place.

## Building from Source

Requirements:
- JDK 17
- Android SDK (API Platform 33)

To assemble an unsigned debug APK:
```sh
./gradlew assembleDebug
```

To run unit tests:
```sh
./gradlew test
```

### Release Signing

To build a signed release APK, define the following environment variables:

| Variable | Description |
|---|---|
| `ASTEROIDOS_KEYSTORE` | Absolute path to the keystore file |
| `ASTEROIDOS_STORE_PASSWORD` | Keystore password |
| `ASTEROIDOS_KEY_ALIAS` | Key alias |
| `ASTEROIDOS_KEY_PASSWORD` | Key password |

Then run:
```sh
./gradlew assembleRelease
```
Without these variables, `assembleRelease` produces an unsigned APK.

Release certificate SHA-256 fingerprint:  
`a53f7ecbdca47656ff20123f58a6634fec0142aca0b8ca33e87781eec4565724`
