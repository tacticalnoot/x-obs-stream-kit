# 🎮 X Live Stream Kit — OBS → X (RTMP)

**Game-audio-only streaming to X/Twitter Live via OBS Studio.**
No mic. No desktop noise. Just the game.

> Built for **RuneScape: Dragonwilds** but works with any game — just swap the game name in your config.

---

## Features

- 🎯 **Game Capture** with audio isolation (no mic, no Discord, no notifications)
- 🔲 **Blurred desktop fallback** — when the game isn't focused, viewers see a blurred desktop instead of your tabs
- 📡 **X Media Studio RTMP** integration
- ⚙️ **Fully customizable** — edit `config.env` to change game, bitrate, resolution, etc.
- 🔒 **No secrets in repo** — stream keys stay in `.env` (gitignored)

---

## Quick Start

### 1. Clone & configure

```bash
git clone https://github.com/tacticalnoot/x-obs-stream-kit.git
cd x-obs-stream-kit
cp config.env.example config.env
```

Edit `config.env` with your details:

```env
STREAM_KEY=your_stream_key_here
RTMP_URL=rtmps://your-ingest-url.x.com/rtmp/
GAME_NAME=RuneScape: Dragonwilds
```

### 2. Import the OBS Scene Collection

1. Open OBS Studio
2. **Scene Collection → Import** → select `obs-scene-collection.json`
3. Switch to the imported collection

### 3. Configure Stream Settings

In OBS → **Settings → Stream**:
- Service: **Custom**
- Server: your RTMP URL from `config.env`
- Stream Key: your stream key from `config.env`

### 4. Go Live

1. **OBS** → Start Streaming
2. **X Media Studio → Producer** → Start Broadcast
3. Verify on your phone (use cell data, not same Wi-Fi)
4. End: Stop Broadcast in Producer → Stop Streaming in OBS

---

## File Structure

```
├── README.md                    # This file
├── config.env.example           # Template — copy to config.env
├── .env                         # Your secrets (gitignored)
├── .gitignore                   # Keeps secrets out of git
├── obs-scene-collection.json    # Importable OBS scene (Game + Blurred Desktop)
├── SETUP_GUIDE.md               # Detailed step-by-step walkthrough
├── CHECKLIST.md                 # Pre-stream checklist
└── TROUBLESHOOTING.md           # Common fixes
```

---

## Recommended OBS Settings

| Setting | Value | Notes |
|---------|-------|-------|
| Rate Control | CBR | Required for RTMP |
| Video Bitrate | 9000 Kbps | Range: 6000–12000 |
| Keyframe Interval | 3 seconds | X requirement |
| Audio Codec | AAC | — |
| Audio Bitrate | 128 Kbps | — |
| Output Resolution | 1280×720 | 1080p works but heavier |
| FPS | 60 | Drop to 30 if unstable |

---

## Customization

Everything is designed to be swapped out:

- **Different game?** Change the Game Capture window target in OBS
- **Want mic?** Re-enable Mic/Aux in OBS → Settings → Audio
- **Different platform?** Swap the RTMP URL (works with Twitch, YouTube, etc.)
- **Higher quality?** Bump resolution to 1920×1080 and bitrate to 12000

---

## Blurred Desktop Fallback

The scene has two layers:

| Layer | Source | Purpose |
|-------|--------|---------|
| Top | Game Capture | Shows game when running |
| Bottom | Display Capture + Blur Filter | Shows blurred desktop when game is minimized |

This is automatic — no scene switching needed.

### Blur Setup (manual step after import)

OBS doesn't export filters in scene collections reliably, so after importing:

1. Right-click **"Desktop Blurred"** source → **Filters**
2. **Effect Filters → + → Blur** (OBS 30.1+)
   - Type: **Gaussian**
   - Size: **20–30**
3. If no built-in blur: install [StreamFX](https://github.com/Xaymar/obs-StreamFX) plugin

---

## Pre-Flight

Before your first stream, verify:

- [ ] X account is **public** (not protected)
- [ ] You have access to [X Media Studio Producer](https://studio.x.com/producer)
- [ ] OBS is updated to 30.1+
- [ ] Stable internet connection (Ethernet preferred)

---

## License

MIT — do whatever you want with it.
