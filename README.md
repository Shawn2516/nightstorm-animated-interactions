# Nightstorm Animated Interaction Visuals

Replaces static interaction illustrations with looping videos in campaign dialogs (the large visual on the right side at stations/markets/planets).

This mod uses `VideoLib` texture overrides, so no Java compilation is required.

## Requirements

- Starsector `0.98a-RC8`
- `VideoLib` (`id: video_lib`) installed and enabled

## Installation

1. Put this folder at `Starsector/mods/Nightstorm/`.
2. In the launcher, enable:
   - `VideoLib`
   - `Nightstorm Animated Interaction Visuals`
3. Start the game once.

## Quick Start

1. Put your first video in:
   - `data/videos/illustrations/`
2. Name it to match an illustration stem (example: `orbital.mp4`).
3. Run:
   - `python tools/build_videolib_overrides.py`
4. Restart Starsector.

## Add Custom Videos Per Illustration

1. Put your files in:
   - `data/videos/illustrations/`
2. Name each file to match an illustration stem exactly:
   - `orbital.mp4` -> `graphics/illustrations/orbital.jpg`
   - `pirate_station.mp4` -> `graphics/illustrations/pirate_station.jpg`
   - `jangala_station.mp4` -> `graphics/illustrations/jangala_station.jpg`
3. Rebuild mappings:
   - `python tools/build_videolib_overrides.py`
4. Restart Starsector.

Supported extensions: `.mp4`, `.webm`, `.gif`, `.mkv`, `.avi`

## How Mapping Works

- Generated config: `data/config/settings.json`
- If a matching per-illustration file is found, that video is used.
- If no matching video exists, Starsector shows the original static illustration.
- The builder only maps texture keys observed in `starsector.log` to avoid VideoLib startup crashes from unavailable wrappers.

## Quality and Performance

- Standard interaction illustrations are generated with `1920x1200` backing textures for better detail.
- Recommended encode settings:
  - 20-40 fps
  - H.264 MP4 for broad compatibility
  - Keep loops reasonably short (5-15s) and compressed
- If performance dips, use lower bitrate or lower source resolution.

## Troubleshooting

- **Static image instead of video**
  - Confirm both mods are enabled.
  - Confirm exact filename match in `data/videos/illustrations/`.
  - Run `python tools/build_videolib_overrides.py`.
  - Fully restart Starsector.

- **Startup crash after adding videos**
  - Do not hand-edit large override blocks unless necessary.
  - Re-run `python tools/build_videolib_overrides.py` to regenerate a safe config.

- **Video looks blurry**
  - Use higher-resolution source video and lower compression.
  - Confirm the game was restarted after rebuilding settings.

## Folder Layout

```text
Nightstorm/
  mod_info.json
  README.md
  data/
    config/
      settings.json
    videos/
      README.txt
      illustrations/
        orbital.mp4
        pirate_station.mp4
        ...
  tools/
    build_videolib_overrides.py
```

## Compatibility Notes

- Designed for Starsector `0.98a-RC8` + VideoLib `0.1.1a`.
- Data-driven override approach; generally high compatibility.
- If another mod overrides the same `graphics/illustrations/*` textures, last loaded override wins.
