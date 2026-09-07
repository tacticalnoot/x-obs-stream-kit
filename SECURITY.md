# Stream security and privacy

This kit handles live-stream credentials and can expose whatever OBS captures. Treat the stream key like a password and test the scene collection before going live.

## Stream keys

- Keep stream keys only in local configuration; never commit them.
- If a key is exposed in a commit, screenshot, log, or stream, revoke/rotate it at the streaming provider immediately. Removing it from the latest file is not enough because Git history may retain it.
- Do not paste real stream keys into issues, pull requests, chat logs, or screenshots.

## Capture privacy

- Verify every visible OBS source before each broadcast.
- A blurred Display Capture is a convenience fallback, not a security boundary. Shapes, notifications, large text, or sensitive context may still be recognizable.
- For higher privacy, disable Display Capture entirely and use a static image/color source as the fallback scene.
- Disable or hide sources that can expose notifications, browser tabs, chat windows, file paths, account names, or other personal information.

## Before going live

1. Use OBS Studio's preview mode and inspect the full frame.
2. Confirm the intended game/application audio is the only active audio source.
3. Confirm Mic/Aux and other unwanted audio sources are muted or disabled.
4. Trigger the fallback state deliberately and inspect what viewers would see.
5. Start with an unlisted/private test destination when the platform supports it.

## If something leaks

1. Stop the broadcast.
2. Rotate any exposed stream key or credential.
3. Remove the sensitive source from OBS before reconnecting.
4. If a secret was committed to Git, rotate it first, then remove it from repository history as needed.

Security reports about this repository can be filed as a GitHub issue when they do not contain secrets. Never include live credentials in a report.
