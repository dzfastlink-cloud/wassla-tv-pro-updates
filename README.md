# Wassla TV Pro updates

This public repository is the data endpoint for Wassla TV Pro. The app fetches `catalog.json` over HTTPS and keeps the last valid catalogue in local storage if a later request fails.

## Channel catalogue

`catalog.json` uses schema version 1:

- `schemaVersion`: integer; currently `1`.
- `catalogVersion`: monotonically increasing integer for catalogue changes.
- `updatedAt`: UTC ISO-8601 timestamp.
- `channels`: array of channel metadata objects.

Example channel object:

```json
{
  "id": "example-channel",
  "number": 1,
  "name": "Example channel",
  "group": "عام",
  "logo": "https://example.org/logo.png",
  "streamUrl": "https://example.org/authorized-stream.m3u8"
}
```

`id`, `name`, and `group` are required. `number`, `logo`, and `streamUrl` are optional. Only add channel streams you are authorized to distribute. This repository is public: never commit private subscription URLs, usernames, passwords, access tokens, or other credentials. Use only public/authorized media links. The current app preview reads catalogue metadata; playback is not implemented yet.

## App release metadata

`app-release.json` documents the current app version and points users to GitHub Releases. The preview app does not yet perform automatic app-update checks. Android installation/update requires user confirmation; do not place signing keys or passwords in this repository.

## Publishing a catalogue update

1. Validate JSON and keep `schemaVersion` at `1` unless the app is updated to support a new schema first.
2. Increment `catalogVersion` and update `updatedAt`.
3. Keep channel IDs stable so favourites can remain associated with channels.
4. Test with the app before publishing.
