# Troubleshooting

## Game Capture is black

1. Run OBS **as Administrator**
2. Try switching Game Capture mode:
   - `Capture specific window` → select the game
   - `Capture any fullscreen application`
3. If still black, switch to **Window Capture** instead
4. Last resort: use **Display Capture** (captures entire screen)
5. For Dragonwilds specifically, try adding `-dx11` to Steam launch options

## No game audio

1. Confirm **"Capture Audio (BETA)"** is checked in Game Capture properties
2. If using Application Audio Capture instead, make sure the correct process is selected
3. Check Windows Sound settings — game should be using your default output device
4. Make sure game audio isn't muted in Windows Volume Mixer

## Hearing desktop audio on stream (Discord, browser, etc.)

1. OBS → Settings → Audio → **Desktop Audio = Disabled**
2. Only use **Capture Audio (BETA)** on the Game Capture source, not Desktop Audio
3. If using Application Audio Capture, ensure only the game process is selected

## Mic is being captured

1. OBS → Settings → Audio → **Mic/Auxiliary Audio = Disabled**
2. Audio Mixer → right-click any mic source → **Remove**
3. Confirm no mic meter appears in Audio Mixer

## Stream is laggy / dropping frames

1. Lower bitrate: try **6000 Kbps** instead of 9000
2. Lower FPS: try **30** instead of 60
3. Use hardware encoder if available (NVENC for NVIDIA, AMF for AMD)
4. Close other bandwidth-heavy apps
5. Switch to Ethernet if on Wi-Fi

## X says "no stream detected"

1. Confirm OBS shows **green square** in bottom-right (streaming active)
2. Check RTMP URL and Stream Key — re-copy from Producer
3. Use **RTMPS** URL if plain RTMP isn't connecting
4. Wait 10–15 seconds after starting OBS stream before starting Producer broadcast

## Stream drops after a few minutes

1. Check OBS → View → Stats for **dropped frames**
2. If > 5% dropped: lower bitrate
3. If network-related: switch to Ethernet, pause cloud sync
4. X has a max bitrate of ~12000 — don't exceed this

## Blur filter not available

- OBS 30.1+ should have a built-in blur
- If not, install [StreamFX](https://github.com/Xaymar/obs-StreamFX)
- Alternative: use a **Color Correction** filter with low opacity to darken the desktop instead

## Dragonwilds shows weird colors / hue shift

Steam → Dragonwilds → Properties → Launch Options:
```
-dx11
```
Remove if it reduces FPS. This forces DX11 rendering which is more compatible with OBS capture.
