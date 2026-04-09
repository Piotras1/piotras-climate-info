# 🎨 Tile CSS Builder — How to use

A standalone visual editor for designing `tile_color` values for **Piotras Climate Info** (Layout 3 & 4).

## Launch

1. Download `tile_css_editor.html` from the repository
2. Open it in any browser — no server, no installation needed

## Gradient tab

- Choose **linear** or **radial** gradient type
- Adjust **angle** (linear only)
- Add up to unlimited **color stops** — each with its own color, opacity, and position
- Use **+ Add stop** to add more, **✕** to remove (minimum 2 stops)
- Live preview updates instantly on the tile

## Box Shadow tab

- Toggle **inset** for inner shadow
- Adjust **Offset X / Y**, **Blur**, **Spread**
- Set shadow **color** and **opacity**
- Live preview updates instantly on the tile

## Copy & paste

1. When satisfied, click **📋 Copy CSS**
2. Paste directly into your YAML config:

```yaml
# Card-level — all tiles
tile_color: "linear-gradient(135deg, rgba(26,26,46,1) 0%, rgba(255,152,0,0.30) 100%)"

# Per-device — single tile
devices:
  - name: "Living Room"
    tile_color: "linear-gradient(135deg, rgba(26,26,46,1) 0%, rgba(255,152,0,0.30) 100%)"
```

## Tips

- Use **low opacity** color stops (10–30%) for a subtle tinted look
- Combine a dark base color with a faint accent for a premium feel
- Switch to **Mode: Light** in the top right corner to preview on light HA themes
