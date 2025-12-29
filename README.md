# open-ec-control-center

EC control toolkit for RGB keyboards on **Tongfang-based laptops**
using the **Integrated Technology Express (ITE) 8291** controller.

This project provides a Linux userspace driver and control tool that interacts
directly with the system **Embedded Controller (EC)** to manage RGB keyboard
backlighting, without relying on vendor-specific software.

---

## Hardware scope

This tool targets laptops based on **Tongfang barebones** that use the
**ITE Device (8291) Rev 0.03** RGB keyboard controller.

These systems are sold worldwide under many reseller brands.
Compatibility depends on the EC firmware and keyboard controller revision,
not on the reseller name.

---

### Identify your keyboard controller

```bash
sudo hwinfo --short | awk '
  /^keyboard:/ { show=1 }
  /^[^[:space:]]/ && !/^keyboard:/ { show=0 }
  show
'
```

You should see the ITE device under the keyboard section:

```bash
keyboard:
  /dev/input/event10   KYE GF3000F Ethernet Adapter
                       Integrated Technology Express ITE Device(8291)
  /dev/input/event0    AT Translated Set 2 keyboard
```

### Known compatible devices

**ITE Device (8291)** is used in many Tongfang-based gaming laptops, including
(non-exhaustive):

- Tongfang GK5* series barebones (e.g.GK5CN5Z, GK5CN6Z, GK5CQ7Z, GK5CP0Z)
- Avell G1550 FOX, G1513 FOX-7, A65, A52 (BR reseller)
- XMG/Schenker Neo 15 (DE reseller), Versions M18 & M19
- PCSpecialist Recoil II & III (UK reseller)
- Scan/3XS LG15 Vengeance Pro (UK reseller)
- Overpowered 15 and 15+ (US reseller, sold via Walmart)
- Monster Tulpar T5 (TR reseller)
- MECHREVO Deep Sea Ghost Z2 (CN reseller)
- Raionbook GS5 (IT reseller)
- Illegear Onyx (MY reseller)
- Hyperbook Pulsar Z15 (PL reseller)
- SMART7 Kallisto GX15D (PL reseller)
- Aftershock APEX 15 (SG reseller)
- Origin-PC EON15-S (USA, Asia, and AU/NZ reseller)
- Eluktronics Mech 15 G2 (US reseller)
- HIDevolution EVOC 16GK5 (US reseller)
- Obsidian GK5CP (PT reseller)
- Vulcan JinGang GTX Standard
- Wootware
- Other Tongfang-based resellers

## Project status

#### Working:

- Set RGB keyboard colors
- Adjust brightness
- Disable keyboard backlight
- Apply predefined lighting effects

### Planned
- CLI improvements
- GUI interface

## Installation

### Using `pip`

Install via pip using sudo or with root user:

```bash
sudo pip3 install git+https://github.com/0xlsa/open-ec-control-center.git
```

### Manual installation

```bash
git clone https://github.com/0xlsa/open-ec-control-center.git
cd open-ec-control-center
python3 setup.py build
sudo python3 setup.py install
```

## Usage

```
usage: aucc [-h]
            (-l | -c COLOR | -H COLOR COLOR | -V COLOR COLOR | -s STYLE | -d)
            [-v VENDOR] [-p PRODUCT] [-D DEVICE]
            [-b {1,2,3,4}]
            [--speed {1,2,3,4,5,6,7,8,9,10}]

Colors available:
[red|green|blue|teal|pink|purple|white|yellow|orange|olive|maroon|brown|gray|
 skyblue|navy|crimson|darkgreen|lightgreen|gold|violet]

options:
  -h, --help            Show this help message and exit
  -l, --list-devices    List all available devices
  -c, --color COLOR     Set a single color for all keys
  -H, --h-alt COLOR COLOR
                        Horizontal alternating colors
  -V, --v-alt COLOR COLOR
                        Vertical alternating colors
  -s, --style STYLE     Lighting style
  -d, --disable         Turn keyboard backlight off
  -v, --vendor VENDOR   Vendor ID (e.g. 1165 or 0x048d)
  -p, --product PRODUCT Product ID
  -D, --device DEVICE   Select device index (use -l)
  -b, --brightness {1..4}
                        Brightness (1 = min, 4 = max)
  --speed {1..10}       Effect speed (1 = fastest, 10 = slowest)
```

### Examples

#### List available devices
```bash
aucc -l
```

#### Set a single color (green, max brightness)
```bash
aucc -c green -b 4
```

#### Horizontal alternating colors
```bash
aucc -H pink teal -b 4
```

#### Vertical alternating colors
```bash
aucc -V red blue -b 3
```

#### Apply a predefined style
```bash
aucc -s rainbow
```

#### Apply a style with a color suffix
```bash
aucc -s rippler          # Ripple Red
aucc -s reactiveo        # Reactive Orange
```

#### Control animation speed
```bash
aucc -s wave --speed 3
```

#### Disable keyboard backlight
```bash
aucc -d
```

#### Select a specific device
```bash
aucc -D 1 -c blue -b 2
```

## Contributions

Contributions are welcome.

Please follow [pep-8](https://www.python.org/dev/peps/pep-0008/) coding style guides.

## Support :coffee:

Developed in my free time.

If you find it useful, supporting the work helps keep it going:
[Buy me a coffee](https://buymeacoffee.com/0xlsa)
