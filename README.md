# ErdiLRF

Arduino driver for [ERDI](https://erdilrf.com) 905 nm laser rangefinder modules over UART.
Works with `HardwareSerial` or `SoftwareSerial` on AVR, SAMD, ESP32, and other Arduino-core
targets.

## Install

- **Arduino IDE / Arduino CLI Library Manager**: Sketch -> Include Library -> Manage Libraries ->
  search `ErdiLRF` -> Install. The
  [registry submission](https://github.com/arduino/library-registry/pull/9133)
  has been accepted. If your local index is out of date, refresh it or use Git below.
- **From Git**: `arduino-cli lib install --git-url https://github.com/yu911517778-a11y/ErdiLRF`
  or clone/copy this repository into your sketchbook's `libraries/` folder.
- **PlatformIO**: add to `platformio.ini`:
  ```ini
  lib_deps =
      erdi-tech/ErdiLRF@0.1.0
  ```
  Version 0.1.0 is public in the
  [PlatformIO Registry](https://registry.platformio.org/libraries/erdi-tech/ErdiLRF).
  Git installation remains available with
  `https://github.com/yu911517778-a11y/ErdiLRF.git`.

## Supported models

**Family A** -- 8-byte `55 AA` command/response protocol, 115200 bps, raw counts x10:
`LR1000E2`, `LR1000E4`, `LR1200E2`, `LR1200E4`, `LR1500E2`, `LR1500E4`, `LR2000E2`, `LR2000E4`,
`LRF1200A1`, `LRF3000A1`, `SPD1200N0`, `SPD1200N2`, `SPD1200N4`, `SPD1200D03`.

**Family B** -- free-running `5C` data-frame protocol, 460800 bps:
`LRF50H`, `LRF100H`, `LRF200H`, `LRF300H`, `LRF600H`, `LRF1500H`, `LRF22VB`, `LRF50VB`.

Per-model measurement units are respected in the driver (the `VB` series reports millimetres,
the `H` series centimetres). Full model datasheets: <https://erdilrf.com/models/>.

`SPD1200D03` is deliberately excluded from automatic baud selection -- see the note in
[`examples/BasicMeasure`](examples/BasicMeasure/BasicMeasure.ino).

## Usage

```cpp
#include <ErdiLRF.h>

static const ErdiModel ERDI_TARGET_MODEL = ERDI_LRF3000A1;
```

See the bundled examples:

- [`BasicMeasure`](examples/BasicMeasure/BasicMeasure.ino) -- single-shot ranging.
- [`ContinuousStream`](examples/ContinuousStream/ContinuousStream.ino) -- free-running stream mode.

A step-by-step wiring and first-reading walkthrough is here:
[Read a laser distance module over Arduino UART](https://erdilrf.com/knowledge/read-laser-distance-module-arduino-uart/).

## Also available

- Python driver: install the published GitHub release wheel:
  ```bash
  pip install https://github.com/yu911517778-a11y/erdi-lrf-drivers/releases/download/v0.1.0/erdi_lrf-0.1.0-py3-none-any.whl
  ```
  See the [Python installation guide](https://github.com/yu911517778-a11y/erdi-lrf-drivers#install-in-one-command).
- ROS 2 node:
  [`ros2/erdi_lrf_ros2`](https://github.com/yu911517778-a11y/erdi-lrf-drivers/tree/main/ros2/erdi_lrf_ros2)
  in the same mono-repo. Its documented validation does not include a live ROS 2 runtime test.

This repository is a maintained split of `arduino/ErdiLRF` from that mono-repo, published
standalone so it can be registered with the Arduino Library Manager and the PlatformIO
Registry (both require a dedicated, tag-releasing repository).

## License

MIT -- see [LICENSE](LICENSE).

---

ERDI TECH LTD -- 905 nm eye-safe laser rangefinder modules (IEC 60825-1 Class 1)
Email: tommy@erdimail.com  WhatsApp: +86 133 0819 5790 (https://wa.me/8613308195790)  Tel: +86-28-81076698
Web: https://erdilrf.com  Room 2812, 28/F, Building 3, No. 88 Jiaozi Avenue, Chengdu Hi-Tech Zone, Sichuan, China
