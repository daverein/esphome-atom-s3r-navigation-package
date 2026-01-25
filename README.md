

# ESPHome Atom S3R Navigation Package

A reusable ESPHome package for the **M5Stack Atom S3R** that provides:

- BLE Proxy
- IR transmitter (GPIO4)
- Button navigation (tap = cycle screens)
- Optional multi-screen UI (up to 4 displays)
- Per-display button events (press / double-click / hold)
- Auto-idle return to Display 1 (optional toggle)

<a href="https://esphome.io/guides/getting_started_hassio.html">
  <img alt="Open ESPHome" src="https://img.shields.io/badge/Open%20in-ESPHome-000000?logo=esphome&logoColor=white">
</a>

---

## Example (recommended)

Create a new ESPHome device YAML like this:

```yaml
substitutions:
  device_name: "den-atom-s3r"
  device_friendly_name: "Den Atom S3R"

api:
  encryption:
    key: "PUT_YOUR_32_BYTE_BASE64_KEY_HERE="

packages:
  atom_s3r: github://daverein/esphome-atom-s3r-navigation-package/packages/atom_s3r/main.yaml@main

