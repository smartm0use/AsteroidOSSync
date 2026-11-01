# Personal AsteroidOS Sync builds

This is smartm0use's unofficial fork of AsteroidOS Sync. The application keeps
the original display name **AsteroidOS Sync** and package `org.asteroidos.sync`.
Fork development is on `fork-main`; upstream `master` is kept separate.

## Version 0.29.1-fork.1

Android `versionCode`: **30**. Future fork releases must increment this number.
The `-fork.N` suffix distinguishes these APKs from upstream releases.

Includes local EasyWeather sources to restore builds, icon rendering fixes,
paired location permission requests, Bluetooth permission/error handling and
the system Bluetooth enable dialog. Discovery keeps the AsteroidOS service
filter and applies it in software. Diagnostic scanning/logging of all nearby
devices is not included.

The connected notification displays the watch's battery after the first valid
reading, for example `Connected to dory (battery 73%)`. Unknown battery values
are omitted; the cache is cleared for a new connection. English and Italian
strings are included.

These changes are related to upstream PRs #232, #233, #234 and #235.
They do not represent an official AsteroidOS release.

## Installation and updates

Download the signed APK from this fork's GitHub Releases page. It has a different
signing certificate from F-Droid: uninstall the F-Droid app before installing
this APK (uninstalling removes its local settings). The earlier Sync Test build
uses a different package and may also be removed. Configure permissions and
the watch connection again after installation.

Later releases signed with the same fork key and a higher versionCode can update
this APK in place. An official/F-Droid APK cannot update it directly because the
signatures differ. Avoid running multiple sync clients connected to the watch.

## Building

Use JDK 17 and Android SDK 33. For a signed release set these environment variables:

```text
ASTEROIDOS_KEYSTORE       absolute path to the release keystore
ASTEROIDOS_STORE_PASSWORD keystore password
ASTEROIDOS_KEY_ALIAS      signing key alias
ASTEROIDOS_KEY_PASSWORD   signing key password
```

Then run `./gradlew build`. Without the signing variables, the release APK is
unsigned. No private key or signing password is stored in this repository.
Keep a secure backup of your keystore and passwords: they are required to publish
updates installable over this fork's previous releases.

Release signing-certificate SHA-256:
`a53f7ecbdca47656ff20123f58a6634fec0142aca0b8ca33e87781eec4565724`.

Battery-notification regression tests are in `app/src/test/` and run with
`./gradlew :app:testDebugUnitTest`. They exercise actual notification content,
battery bounds, reconnect behavior, localization and message feedback avoidance.
