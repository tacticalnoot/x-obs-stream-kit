# Setup Guide — X Live Stream Kit

## Full walkthrough: OBS → X (RTMP) with game-audio-only

---

## Step 1 — Install OBS Studio

Download from [obsproject.com](https://obsproject.com). Version **30.1+** recommended (has built-in audio capture on game sources).

Reboot after install to clear audio device weirdness.

---

## Step 2 — Import Scene Collection

1. Open OBS
2. **Scene Collection → Import**
3. Select `obs-scene-collection.json` from this repo
4. **Scene Collection → X Live — Dragonwilds**

This gives you:
- **Dragonwilds Game** (Game Capture, top layer, audio enabled)
- **Desktop Blurred** (Display Capture, bottom layer)

---

## Step 3 — Add Blur Filter (manual step)

OBS doesn't reliably import filters, so do this once:

1. Right-click **"Desktop Blurred"** in Sources → **Filters**
2. Under **Effect Filters** → click **+**

### Option A: OBS 30.1+ built-in
- Add **"Blur"** → Type: **Gaussian** → Size: **20–30**

### Option B: StreamFX plugin
- Install [StreamFX](https://github.com/Xaymar/obs-StreamFX)
- Add **"Blur"** → Type: **Gaussian** → Size: **24**

### Option C: No blur available (low-effort alternative)
- Add **"Color Correction"** → set **Opacity to 0.3**
- This darkens the desktop instead of blurring — still hides content

---

## Step 4 — Audio Setup (CRITICAL)

### 4a: Disable everything you don't want
OBS → **Settings → Audio**:
- **Desktop Audio → Disabled**
- **Mic/Auxiliary Audio → Disabled**
- All other devices → **Disabled**

### 4b: Enable game audio on capture source
- Click **"Dragonwilds Game"** in Sources → **Properties**
- Check **"Capture Audio (BETA)"** ✅
- This captures ONLY the game's audio output

### 4c: Verify in Audio Mixer
- Launch the game
- You should see the **game audio meter moving** on the Game Capture source
- You should see **NO other meters** (no Mic, no Desktop Audio)

---

## Step 5 — Output Settings

OBS → **Settings → Output** → Output Mode: **Advanced**

### Streaming tab:
| Setting | Value |
|---------|-------|
| Encoder | x264 (or NVENC if available) |
| Rate Control | CBR |
| Bitrate | 9000 Kbps |
| Keyframe Interval | 3 sec |
| Profile | main |
| Tune | zerolatency |

### Audio tab:
| Setting | Value |
|---------|-------|
| Audio Bitrate | 128 Kbps |
| Audio Codec | AAC |

---

## Step 6 — Video Settings

OBS → **Settings → Video**:

| Setting | Value |
|---------|-------|
| Base (Canvas) | Your monitor resolution |
| Output (Scaled) | **1280×720** |
| Downscale Filter | Lanczos |
| FPS | **60** |

---

## Step 7 — X Media Studio Setup

1. Go to [studio.x.com/producer](https://studio.x.com/producer)
2. **Sources → Create Source**
   - Type: **RTMP**
   - Name: `OBS-DRAGONWILDS` (or whatever you want)
   - Region: closest to you
3. Open the source and copy:
   - **RTMP URL** (or RTMPS URL — prefer RTMPS)
   - **Stream Key**

---

## Step 8 — Connect OBS to X

OBS → **Settings → Stream**:
- Service: **Custom**
- Server: paste your **RTMP/RTMPS URL**
- Stream Key: paste your **Stream Key**

Save these in `config.env` for reference (gitignored, never committed).

---

## Step 9 — Go Live

**Order matters:**

1. ▶️ OBS → **Start Streaming**
2. 📡 X Producer → Create Broadcast → select your source → **Start**
3. 📱 Check on phone (cell data) — confirm video + audio
4. 🛑 End: Stop Broadcast in Producer → Stop Streaming in OBS

---

## Dragonwilds-Specific Fix

If Game Capture shows a black screen or weird colors:

**Steam → Dragonwilds → Properties → General → Launch Options:**
```
-dx11
```
This forces DirectX 11 (DX12 sometimes breaks capture). Remove if it hurts FPS.
