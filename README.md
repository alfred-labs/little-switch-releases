# LittleSwitch releases

Public release channel for **Model Switch** (the LittleSwitch product):
the Sparkle appcast and the notarized DMG of every version. No application
source code lives here — the app repository is private and stays separate.

## How a release lands here

1. The app repository's release pipeline builds and notarizes
   `Model-Switch-<version>-arm64.dmg`.
2. `tools/release/publish-update.sh` in the app repository signs the DMG
   with the project's Ed25519 key, publishes the DMG as a
   `v<version>` GitHub release, and prepends its item to `appcast.xml`.
3. Installed applications read `appcast.xml` (served from this branch)
   and verify each download against the `SUPublicEDKey` baked into the
   app bundle.

## Key policy

The `SUPublicEDKey` in the app's `Info.plist` is the only public half of
the appcast signing key. The private half lives outside every repository;
losing it permanently breaks updates for every installed copy, so it is
never regenerated, never committed, and never printed.
