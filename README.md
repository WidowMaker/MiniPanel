# MiniPanel - Home Assistant Dashboard

A sleek, full-screen Home Assistant dashboard designed for the Shelly Wall Display X2i, wall-mounted tablets, and kiosk mode.

![MiniPanel Home view](screenshots/01-home.jpg)

## Features

- **Full-screen panel mode** with a custom background image
- **Kiosk mode** support that hides the header and sidebar for selected users
- **5 main views**: Home, Lys (Lights), Klima (Climate), Musik (Music), and Status
- **Real-time clock and weather** on the Home view
- **Family presence** indicators with avatar photos
- **Dishwasher status** pill when a program is running
- **Mini music player** with playback controls on the Home view
- **Fixed navigation menu** with active-state highlighting and a light-on indicator
- **Lights view** with room controls, scenes, and a master switch
- **All Lights drill-down** with controls for every configured room or light group
- **Climate view** with two heating zones, presets, and shared controls
- **Music view** with playlist shortcuts, playback controls, and volume control
- **Status view** for appliances and robot vacuum cleaners
- **Idle return** that automatically navigates back to Home after 60 seconds of inactivity

## Screenshots

### Home

The main overview with clock, weather, family presence, mini media controls, and the fixed navigation menu.

**Dashboard path:** `/dashboard-minipanel/home`

![MiniPanel Home view](screenshots/01-home.jpg)

### Lights

The primary lighting view with scenes, room-level controls, an All Lights shortcut, and a master switch.

**Dashboard path:** `/dashboard-minipanel/lys`

![MiniPanel Lights view](screenshots/02-lights.jpg)

#### All Lights

A drill-down page opened from the Lights view. It is not a separate item in the right-side navigation menu.

![MiniPanel All Lights drill-down](screenshots/03-all-lights.jpg)

### Climate

Two climate zones with current and target temperatures, power controls, temperature adjustment, and preset buttons.

**Dashboard path:** `/dashboard-minipanel/klima`

![MiniPanel Climate view](screenshots/04-climate.jpg)

### Music

Playlist shortcuts, source controls, a full media player, and vertical volume control.

**Dashboard path:** `/dashboard-minipanel/musik`

![MiniPanel Music view](screenshots/05-music.jpg)

### Status

Status information for the dishwasher, refrigerator/freezer, and robot vacuum cleaners.

**Dashboard path:** `/dashboard-minipanel/status`

![MiniPanel Status view](screenshots/06-status.jpg)

## Views

| View | Path | Description |
|------|------|-------------|
| Home | `/dashboard-minipanel/home` | Clock, weather, family presence, mini player, and navigation |
| Lys | `/dashboard-minipanel/lys` | Scenes, room controls, All Lights drill-down, and master switch |
| Klima | `/dashboard-minipanel/klima` | Climate controls and presets |
| Musik | `/dashboard-minipanel/musik` | Playlists, volume, and full music player |
| Status | `/dashboard-minipanel/status` | Appliance and system status |

## Required HACS Custom Cards

- [button-card](https://github.com/iantrich/button-card): Primary card used throughout the dashboard
- [kiosk-mode](https://github.com/NUCleverHA/kiosk-mode): Hides the Home Assistant header and sidebar

## Installation

### 1. Install the required HACS components

Install `button-card` and `kiosk-mode` through HACS, then restart Home Assistant if required.

### 2. Copy the background image

Copy `minipanelbackground.png` to your Home Assistant `www` folder:

```bash
cp minipanelbackground.png /config/www/
```

The image will then be available in Home Assistant as:

```text
/local/minipanelbackground.png
```

### 3. Create the dashboard

1. Go to **Settings > Dashboards**
2. Create a new dashboard
3. Open the new dashboard
4. Select **Edit dashboard**
5. Open the three-dot menu
6. Select **Raw configuration editor**
7. Replace the existing content with the contents of `minipanel.json`
8. Save the dashboard

Direct editing of files inside `/config/.storage/` is not recommended.

### 4. Configure kiosk mode

The dashboard is configured to hide the interface for the Home Assistant user named `Shelly`.

Edit the `kiosk_mode` section in `minipanel.json` to match the user account used by your wall display.

### 5. Replace the example entities

The dashboard uses entity IDs from my own Home Assistant installation. Replace them with the corresponding entities from your setup.

## Customization

### Entity IDs

| Dashboard reference | Replace with |
|---------------------|--------------|
| `light.stue_lights` | Living room light group |
| `light.kontor_lights` | Office light group |
| `light.kokken_lights` | Kitchen light group |
| `light.nordtronic_a_s_rotdimz_98424072` | Bathroom light |
| `light.caroline_lights` | Bedroom or family-room light group |
| `light.sovevaerelse` | Main bedroom light |
| `media_player.kokken_hub_2` | Media player |
| `sensor.udendors_temperatur` | Outdoor temperature sensor |
| `weather.forecast_home` | Weather entity |
| `person.*` or `device_tracker.*` | Presence entities |
| `sensor.opvaskemaskine_current_program_remaining_time` | Dishwasher remaining-time sensor |

### Scripts

The music shortcut buttons reference these scripts:

- `script.1783163503917`: Brians Mix
- `script.gods_of_metal`: Gods of Metal
- `script.musik_liked_songs_pa_kokken_hub`: Spotify Liked Songs

Replace them with your own Music Assistant or media-control scripts.

### Background image

Replace `minipanelbackground.png` in `/config/www/` with your own image while keeping the same filename, or update the image path in the dashboard configuration.

## Notes

- The layout is optimized for the Shelly Wall Display X2i in landscape orientation.
- Commands such as switching a light are executed immediately. Any visible delay is typically the dashboard waiting for the updated entity state from Home Assistant.
- The All Lights page belongs to the Lights section and is not a sixth main navigation view.

## License

MIT
