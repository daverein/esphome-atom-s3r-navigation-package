# ESPHome Atom S3R Navigation Package

![ESPHome](https://img.shields.io/badge/ESPHome-Package-blue)
![Home%20Assistant](https://img.shields.io/badge/Home%20Assistant-Compatible-green)
![Platform](https://img.shields.io/badge/ESP32--S3-Atom%20S3R-orange)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

A reusable ESPHome package for the **M5Stack Atom S3R** that provides:

- BLE Proxy
- IR transmitter (GPIO4)
- Button-driven multi-screen navigation (up to 4 screens)
- Per-display button events (press / double-click / hold)
- Optional “idle return to Display 1”
- Fully customizable per-screen icon + text lines via Home Assistant UI
- Network status via colored background

---

## Features

| Feature | Included |
|--------|----------|
| BLE Proxy | ✅ |
| IR Transmitter (GPIO4) | ✅ |
| Screen cycling via tap | ✅ |
| 4 screens (1 required + 3 optional) | ✅ |
| Per-display button events | ✅ |
| Optional idle return to Display 1 | ✅ |
| HA-configurable icon + title + 3 lines per screen | ✅ |
| Rotation selector (0/90/180/270) | ✅ |
| Backlight control (LP5562) | ✅ |

---

## Quick Start (Recommended)

Create a new ESPHome device YAML like:

```yaml
substitutions:
  device_name: "your-device-name"
  device_friendly_name: "Your Friendly NAme"

api:
  encryption:
    key: "YOUR_API_KEY"

packages:
  atom_s3r: github://daverein/esphome-atom-s3r-navigation-package/packages/atom_s3r/main.yaml@main

```
---

## Home Assistant Entities You’ll See

Once the device is adopted in Home Assistant, you’ll get entities like:

### Display navigation + behavior
- `Enable Display 2`
- `Enable Display 3`
- `Enable Display 4`
- `Idle Return To Display 1`
- `Display Rotation`

Displays 2–4 are only included in cycling if enabled.
Tap-to-cycle is separated from normal press events, so it won’t accidentally trigger your automations.


![Atom S3R preview](img/shades-example.png)

### Per-display UI fields
- `D1 Icon`, `D1 Icon Title`, `D1 Line 1`, `D1 Line 2`, `D1 Line 3`
- `D2 Icon`, `D2 Icon Title`, `D2 Line 1`, `D2 Line 2`, `D2 Line 3`
- `D3 Icon`, `D3 Icon Title`, `D3 Line 1`, `D3 Line 2`, `D3 Line 3`
- `D4 Icon`, `D4 Icon Title`, `D4 Line 1`, `D4 Line 2`, `D4 Line 3`

### Per-display button events (perfect for automations)
- `Display 1 Button Pressed`
- `Display 1 Button Double Clicked`
- `Display 1 Button Held`
- `Display 2 Button Pressed`
- `Display 2 Button Double Clicked`
- `Display 2 Button Held`
- `Display 3 Button Pressed`
- `Display 3 Button Double Clicked`
- `Display 3 Button Held`
- `Display 4 Button Pressed`
- `Display 4 Button Double Clicked`
- `Display 4 Button Held`

---

## Automation Examples

### 1) Send temperature to Display 2 Line 2

This updates **D2 Line 2** whenever the sensor changes.

```yaml
alias: Atom S3R - Display temperature on Display 2 middle line
description: "Push temperature value into the Atom S3R Display 2 Line 2 field."
mode: restart

trigger:
  - platform: state
    entity_id: sensor.living_room_temperature

action:
  - service: text.set_value
    target:
      entity_id: text.den_atom_s3r_d2_line_2
    data:
      value: >
        {{ states('sensor.living_room_temperature') }} °F

```

![Atom S3R preview](img/temp-example.png)

### 2) Turn on a light when Display 1 is double-clicked

This example turns on a light whenever the Atom is on **Display 1** and you **double-click** the physical button.

```yaml
alias: Atom S3R - D1 Double Click turns on Lamp
description: "Double click on Display 1 triggers a light on."
mode: single

trigger:
  - platform: state
    entity_id: binary_sensor.den_atom_s3r_display_1_button_double_clicked
    to: "on"

action:
  - service: light.turn_on
    target:
      entity_id: light.living_room_lamp
```


