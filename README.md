##  Piotras Climate Info
### Release v1.2.0
A highly customizable Home Assistant card for monitoring climate conditions and energy usage.  
Designed with a modern UI, smooth color transitions, and a built-in visual editor.

Supports multiple layouts optimized for different dashboard styles — from compact lists to advanced visual gauges.

## ✨ Features
- 4 distinct layouts
- Fluid color interpolation
- Smart icon animations (anti-flicker system)
- Fully customizable per device
- Built-in visual editor support

---

## 🧩Layout 1: The Compact Row

![Zrzut ekranu (1041)](https://github.com/user-attachments/assets/bcf84482-5fc6-4504-9844-aecde4351f64)

### Description

Layout 1 is the most space-efficient mode of the card. All data — icon, name, temperature, humidity, and energy — is arranged in a single horizontal row.  
Perfect for sidebars or dashboards where multiple rooms need to be monitored without clutter.

### Dynamic Animations

Animations are opt-in and must be enabled with `show_anim: true`. An intelligent threshold system prevents flickering near boundary values:
- **Bouncing Icon** – activates when the value falls below 98% of `temp_cold_max`
- **Shaking Icon** – activates when the value exceeds 102% of `temp_comfort_max` (critical alert)

### Configuration

```yaml
type: custom:piotras-climate-info
header: "HOME CLIMATE"
layout: 1
show_icon_ring: true
show_linear_color: true
devices:
  - name: "Living Room"
    icon_ha: "mdi:sofa"
    entity_temp: sensor.living_room_temp
    entity_huma: sensor.living_room_humidity
    entity_kwh: sensor.kWh_meter_for_the_room
    entity_praca: binary_sensor.room_operation_sensor
```

---

## 🧩 Layout 2: The Modern Vertical Stack

![Zrzut ekranu (1042)](https://github.com/user-attachments/assets/4dd28d35-9961-4e04-968c-3e8d5201df8f)

### Description
Layout 2 provides a clean arrangement focused on readability. The display adapts automatically based on `icon_size`:
- **`icon_size > 30`** – horizontal mode: icon on the left, device name and measurements on the right
- **`icon_size ≤ 30`** – vertical mode: name at the top, icon below, measurements at the bottom

Devices are automatically organized into a responsive list.

### Visual Hierarchy
- **Header** – device name at the top  
- **Icon** – main visual element (use `icon_size > 30` to switch to horizontal mode)  
- **Data** – temperature, humidity, and energy displayed alongside or below the icon  

### Configuration

```yaml
type: custom:piotras-climate-info
header: "HOME CLIMATE"
layout: 2
show_icon_ring: true
show_linear_color: true
icon_size: 31
devices:
  - name: "Living Room"
    icon_ha: "mdi:sofa"
    entity_temp: sensor.living_room_temp
    entity_huma: sensor.living_room_humidity
    entity_kwh: sensor.kWh_meter_for_the_room
    entity_praca: binary_sensor.room_operation_sensor
```

---

## 🧩 Layout 3: The Multi-Column Grid

![Zrzut ekranu (1043)](https://github.com/user-attachments/assets/4db9ffee-fc4b-47e0-a49f-473b5740d83e)

### Description

Layout 3 organizes devices into a visually rich multi-column grid.
Each device is displayed in its own card with a clear structure: name at the top, icon in the center, and data below.

Ideal for large dashboards and wide screens.

### Visual Layout

- **Individual Cards** – clear separation between devices
- **Centered Structure** – Name → Icon → Data
- **Responsive Grid** – automatic wrapping based on available space

### Configuration

```yaml
type: custom:piotras-climate-info
header: "HOME CLIMATE"
layout: 3
show_icon_ring: true
show_linear_color: true
icon_size: 31
width_karta: 120
devices:
  - name: "Living Room"
    icon_ha: "mdi:sofa"
    entity_temp: sensor.living_room_temp
    entity_huma: sensor.living_room_humidity
    entity_kwh: sensor.kWh_meter_for_the_room
    entity_praca: binary_sensor.room_operation_sensor
```

---

## 🧩 Layout 4: Energy & Percentage Mode

![Zrzut ekranu (1044)](https://github.com/user-attachments/assets/b976186a-bb07-4d11-9ed8-4db0472a1ad7)

### Description

Layout 4 is a specialized monitoring module designed for precise tracking of energy consumption and percentage-based metrics. It features a unique vertical gauge system that provides immediate visual feedback on the state of your devices.

### Key Features

- **Vertical Gauge Bar:** A side-mounted progress bar with a dynamic gradient (Green-Yellow-Red).
- **Value Pointer:** A horizontal marker that physically moves along the gauge to represent the current state.
- **Metric Focused:** Optimized for high-frequency data like Watts, Amps, or Volts, using the `entity_kwh` field as a generic value source.
- **Status Bar:** When `show_job: true`, a small bar at the bottom of each tile indicates device activity (green = active, grey = inactive).
- **Unit Badge:** The unit of measurement (W, A, %, V) is displayed in a distinct badge below the value.

### Layout 4 Options

- **temp_comfort_max** – Acts as the 100% (top) point of the vertical gauge. Also defines the maximum for icon color interpolation.
- **temp_cold_max** – Defines the start color of the icon gradient (does not affect the gauge range — the gauge always starts from 0).
- **decimal_places** – Allows for high precision (e.g., `1` for `0.0` or `2` for `0.00`) for electrical measurements.

### Configuration

```yaml
type: custom:piotras-climate-info
header: "HOME CLIMATE"
layout: 4
form_icon: 1
show_icon_ring: true
show_linear_color: true
show_job: true
width_karta: 120
show_color_card: false
devices:
  - name: "Watts"
    entity_kwh: sensor.using_Watts_sensor
    icon_ha: mdi:lightning-bolt
    temp_cold_max: 100
    temp_cold_color: "#008000"
    temp_comfort_max: 500
    temp_comfort_color: "#ffff00"
    temp_hot_color: "#e74c3c"
```

---

## ⚙️ Installation

### Method 1: Via HACS (Recommended)

1. Click the button below to automatically add the repository to your HACS:

<a href="https://my.home-assistant.io/redirect/hacs_repository/?owner=Piotras1&repository=piotras-climate-info&category=plugin">
    <img src="https://my.home-assistant.io/badges/hacs_repository.svg" alt="Open your Home Assistant instance">
</a>

2. Click **Add** in the pop-up window.
3. Once the repository page opens, click **Download**.
4. After downloading, do a **Hard reload** of your browser.

### Method 2: Manual Installation

1. Download this repository as a ZIP file and extract it.
2. Inside your Home Assistant `config/www/` directory, create a new folder named `piotras-climate-info`.
3. Copy the compiled files (from `dist/` folder) into `config/www/piotras-climate-info/`.
4. Go to **Settings → Dashboards → Resources**.
5. Click **Add Resource** and enter:
```
/local/piotras-climate-info/piotras-climate-info-loader.js?v=1.2.0
```
- Resource type: **JavaScript Module**
6. Hard reload your browser (`Ctrl+Shift+R`).

---

## ⚙️ Configuration Reference

### Card-level options

| Option | Type | Default | Layouts | Description |
|---|---|---|---|---|
| `header` | string | `""` | all | Text displayed at the top of the card |
| `layout` | number | `1` | all | Layout mode: `1` = Compact Row, `2` = Vertical Stack, `3` = Grid, `4` = Energy Monitor |
| `show_header` | boolean | `true` | all | Show or hide the header text |
| `show_header_line` | boolean | `true` | all | Show or hide the separator line below the header |
| `show_name` | boolean | `true` | all | Show device name |
| `show_icon` | boolean | `true` | all | Show device icon |
| `show_temp` | boolean | `true` | all | Show temperature value |
| `show_huma` | boolean | `true` | all | Show humidity value |
| `show_kwh` | boolean | `true` | all | Show energy/power value |
| `show_job` | boolean | `false` | all | Show activity indicator (badge in L1, status bar in L4) |
| `show_icon_ring` | boolean | `false` | all | Show colored ring/background around the icon |
| `show_linear_color` | boolean | `false` | all | Enable smooth color interpolation (vs fixed thresholds) |
| `show_anim` | boolean | `false` | 1, 2, 3 | Enable bounce/shake icon animations |
| `show_color_card` | boolean | `false` | 2, 3, 4 | Tint tile background with the current temperature color |
| `tile_color` | string | — | 3, 4 | Fixed tile background — any CSS value (color, gradient). Overrides `show_color_card` when set. See [Tile Color Override](#-tile-color-override-tile_color) |
| `form_icon` | number | `1` | all | Icon shape: `1` = circle, `2` = rounded square |
| `layout` | number | `1` | — | Layout selector (see above) |
| `icon_size` | number | `28` | all | Icon size in px. In Layout 2, values `> 30` switch to horizontal mode |
| `width_karta` | number | `110` | 3, 4 | Tile width in px for grid layouts |
| `decimal_places` | number | `0` | 4 | Decimal places for the main value display |
| `device_gap` | number | `8` | 1, 2 | Gap between device rows (px) |
| `between_entry` | number | `10` | 1, 2, 3, 4 | Gap between tiles in the grid / elements within a row (px) |
| `tile_gap` | number | `4` | 3, 4 | Gap between elements inside a tile (px) |
| `name_width` | number | `100` | 1 | Fixed width of the name column (px) |

### Card appearance

| Option | Type | Default | Description |
|---|---|---|---|
| `background_color` | string | HA default | Card background color |
| `border_radius` | number | HA default | Card corner radius (px) |
| `border_width` | number | HA default | Card border width (px) |
| `border_color` | string | HA default | Card border color |
| `box_shadow` | string | HA default | Card box shadow |

### Typography

| Option | Type | Default | Description |
|---|---|---|---|
| `header_color` | string | `var(--primary-text-color)` | Header text color |
| `header_align` | string | `left` | Header alignment: `left`, `center`, `right` |
| `header_font_size` | number | `14` | Header font size (px) |
| `header_font_style` | number | `1` | Header font style (see `font_style`) |
| `name_color` | string | `var(--primary-text-color)` | Device name color |
| `name_font_size` | number | `13` | Device name font size (px) |
| `val_color` | string | `var(--primary-text-color)` | Value text color |
| `val_font_size` | number | `13` | Value font size (px) |
| `unit_color` | string | `var(--secondary-text-color)` | Unit text color |
| `unit_font_size` | number | `11` | Unit font size (px) |
| `font_style` | number | `1` | Global font style: `1` = default, `2` = small-caps, `3` = monospace, `4` = uppercase with letter spacing |

### Per-device options (under `devices:`)

| Option | Type | Default | Description |
|---|---|---|---|
| `name` | string | `""` | Display name of the device |
| `icon_ha` | string | `""` | Home Assistant MDI icon (e.g. `mdi:sofa`) |
| `entity_temp` | string | — | Entity ID for temperature sensor |
| `entity_huma` | string | — | Entity ID for humidity sensor |
| `entity_kwh` | string | — | Entity ID for energy/power sensor (also used as main value in Layout 4) |
| `entity_praca` | string | — | Entity ID for binary activity sensor (`on` = active) |
| `temp_cold_max` | number | `18` | Upper boundary of the "cold" range (°C). In Layout 4: defines start of icon color gradient |
| `temp_comfort_max` | number / string | `23` | Upper boundary of the "comfort" range (°C). In Layout 4: defines 100% of the gauge. Accepts a number or an **entity ID string** for a dynamic maximum (e.g. `"sensor.power_limit"`). See [Dynamic Gauge Maximum](#-dynamic-gauge-maximum-temp_comfort_max-in-layout-4) |
| `temp_cold_color` | string | `#3498db` | Color for cold range |
| `temp_comfort_color` | string | `#27ae60` | Color for comfort range |
| `temp_hot_color` | string | `#e74c3c` | Color for hot range |
| `tile_color` | string | — | Per-device tile background override — any CSS value (color, gradient). Takes priority over card-level `tile_color` and `show_color_card`. See [Tile Color Override](#-tile-color-override-tile_color) |

---

## 🎨 Tile Color Override (`tile_color`)

> Applies to: **Layout 3 and Layout 4**

The `tile_color` option allows you to set a fixed background color for device tiles, overriding the automatic temperature-based coloring from `show_color_card`.

The value accepts any valid CSS background value — solid color, gradient, or any other CSS background expression.

### 🛠️ Tile CSS Builder

Not sure what gradient or shadow to use? A dedicated visual editor is included in the repository:  
**`tile_css_editor.html`** — open it in any browser to design your tile background live.

It supports:
- **Gradient tab** — linear or radial gradient with unlimited color stops, opacity per stop, angle control, and live tile preview
- **Box Shadow tab** — inset toggle, X/Y offset, blur, spread, color and opacity sliders
- **Copy CSS button** — copies the generated value directly to clipboard, ready to paste into `tile_color`

### Priority Logic

The card resolves tile color in the following order:

1. **Per-device `tile_color`** — if set under a specific device in `devices:`, it takes full priority for that tile
2. **Card-level `tile_color`** — if set at the top level of the card config, it applies to all tiles that don't have their own `tile_color`
3. **`show_color_card: true`** — temperature-based background color, used only when no `tile_color` is present
4. **Default** — subtle neutral background (`rgba(255,255,255,0.1)`)

When `tile_color` is set (at either level), `show_color_card` is **completely ignored** for that tile — including the colored side borders that `show_color_card` normally adds.

### Usage

**Card-level** — same color for all tiles:
```yaml
type: custom:piotras-climate-info
layout: 3
tile_color: "linear-gradient(135deg, rgba(26,26,46,1) 0%, rgba(255,152,0,0.30) 100%)"
devices:
  - name: "Living Room"
    ...
```

**Per-device** — individual color per tile:
```yaml
type: custom:piotras-climate-info
layout: 3
devices:
  - name: "Living Room"
    tile_color: "#1a1a2e"
    ...
  - name: "Bathroom"
    tile_color: "linear-gradient(135deg, rgba(15,52,96,1) 0%, rgba(26,26,46,1) 100%)"
    ...
```

**Mixed** — card-level default with one override:
```yaml
type: custom:piotras-climate-info
layout: 3
tile_color: "#1a1a2e"
devices:
  - name: "Living Room"
    tile_color: "linear-gradient(135deg, rgba(45,27,105,1) 0%, rgba(26,26,46,1) 100%)"   # overrides card-level
    ...
  - name: "Bathroom"
    ...   # uses card-level #1a1a2e
```

---

## ⚡ Dynamic Gauge Maximum (`temp_comfort_max` in Layout 4)

> Applies to: **Layout 4 only**

In Layout 4, `temp_comfort_max` controls the **top of the vertical gauge bar** — it defines what value equals 100% on the gauge.

### Static value (number)

Set a fixed maximum directly:

```yaml
devices:
  - name: "Watts"
    entity_kwh: sensor.power_meter
    temp_comfort_max: 500   # gauge goes from 0 to 500 W
```

### Dynamic value (entity ID)

Pass an entity ID as a string — the card will read the current state of that entity at runtime and use it as the gauge maximum. This is useful when the maximum changes over time (e.g. a configurable power limit).

```yaml
devices:
  - name: "Watts"
    entity_kwh: sensor.power_meter
    temp_comfort_max: "sensor.power_limit"   # reads live value from HA
```

The entity value is parsed as a number. If the entity is unavailable or the value cannot be parsed, the gauge falls back to the default maximum of `23`.

---
*Created by Piotras. Strictly engineered for reliability.*
