# MiniPanel - Home Assistant Dashboard

A sleek, full-screen panel dashboard for Home Assistant designed for wall-mounted tablets and kiosk mode.

![MiniPanel](minipanelbackground.png)

## Features

- **Full-screen panel mode** with background image
- **Kiosk mode** support (hides header/sidebar for specific users)
- **5 views**: Home, Lys (Lights), Klima (Climate), Musik (Music), Status
- **Real-time clock & weather** on the home screen
- **Family presence** indicators with avatar photos
- **Dishwasher status** pill when running
- **Mini music player** with playback controls on home screen
- **Navigation menu** with active state highlighting and light-on indicator
- **Lights view** with per-room brightness sliders, color/temp toggles, and a master on/off switch
- **Music view** with playlist shortcuts and a full player with volume control
- **Idle return** — auto-navigates back to home after 60 seconds of inactivity

## Views

| View | Path | Description |
|------|------|-------------|
| Home | `/dashboard-minipanel/home` | Clock, weather, family, mini player, nav |
| Lys | `/dashboard-minipanel/lys` | All lights with dimmers and master switch |
| Klima | `/dashboard-minipanel/klima` | Climate controls |
| Musik | `/dashboard-minipanel/musik` | Playlists and full music player |
| Status | `/dashboard-minipanel/status` | Device/system status |

## Required HACS Custom Cards

- [button-card](https://github.com/iantrich/button-card) — primary card used throughout
- [kiosk-mode](https://github.com/NUCleverHA/kiosk-mode) — hides sidebar/header

## Installation

### 1. Copy files to Home Assistant

Copy `minipanelbackground.png` to your `www/` folder:
```bash
cp minipanelbackground.png /config/www/
```

### 2. Import the dashboard

**Option A — via UI:**
1. Go to **Settings → Dashboards**
2. Click the **+** button to create a new dashboard
3. Choose **Raw configuration editor**
4. Paste the contents of `minipanel.json`

**Option B — via file:**
1. Copy `minipanel.json` to `/config/.storage/lovelace.dashboard_minipanel`
2. Restart Home Assistant

### 3. Configure kiosk mode (optional)

The dashboard uses kiosk-mode to hide the header for user `Shelly`. Edit the `kiosk_mode` section in the JSON to match your user name.

## Customization

### Entity IDs

This dashboard uses entity IDs specific to my setup. You will need to replace them with your own:

| Dashboard reference | What to find |
|---------------------|-------------|
| `light.stue_lights` | Living room light group |
| `light.kontor_lights` | Office light group |
| `light.kokken_lights` | Kitchen light group |
| `light.nordtronic_a_s_rotdimz_98424072` | Bathroom light |
| `light.caroline_lights` | Caroline's room light |
| `light.sovevaerelse` | Bedroom light |
| `media_player.kokken_hub_2` | Kitchen media player |
| `sensor.udendors_temperatur` | Outdoor temperature sensor |
| `weather.forecast_home` | Weather forecast entity |
| `person.*` / `device_tracker.*` | Family members |
| `sensor.opvaskemaskine_current_program_remaining_time` | Dishwasher sensor |

### Scripts

Music playlist buttons reference scripts:
- `script.1783163503917` — Brians Mix
- `script.gods_of_metal` — Gods of Metal
- `script.musik_liked_songs_pa_kokken_hub` — Spotify liked songs

Replace these with your own Music Assistant / media scripts.

### Background image

Replace `minipanelbackground.png` in `www/` with your own image. The dashboard references it as `/local/minipanelbackground.png`.

## License

MIT
