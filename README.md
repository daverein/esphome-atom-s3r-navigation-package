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
  device_name: "den-atom-s3r"
  device_friendly_name: "Den Atom S3R"

packages:
  atom_s3r: github://daverein/esphome-atom-s3r-navigation-package/packages/atom_s3r/main.yaml@main
