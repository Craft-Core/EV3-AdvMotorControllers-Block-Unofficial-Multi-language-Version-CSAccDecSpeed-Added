# EV3-AdvMotorControllers-Block-Unofficial-Multi-language-Precision

> An extended, multi-language fork of [EV3-AdvMotorControllers-Block](https://github.com/a10036gt/EV3-AdvMotorControllers-Block) — adding precision control blocks to make your EV3 robot move faster and more accurately.

![](https://i2.wp.com/www.ofdl.nctu.me/wp-content/uploads/2020/07/EV3_AdvMotorCtrl.jpg?w=592&ssl=1)

## What is this?

WRO robots need to be **fast, accurate, and consistent**. The built-in EV3-G blocks are far from sufficient for competitive use. This project extends the original `EV3-AdvMotorControllers-Block` with additional precision control blocks, multi-language UI support, and color sensor utilities — all implemented at a low level for maximum speed and accuracy.

![](https://www.tecnonews.info/files/3-10397-fotoArticulo/Captura%20de%20pantalla%202018-11-24%20a%20las%201.13.30.png)

---

## Blocks Included

### Original blocks (by [OFDL / a10036gt](https://github.com/a10036gt/EV3-AdvMotorControllers-Block))

| Block | Description |
| ----- | ----------- |
| **PD Controller** | Line-following PD controller using two sensors |
| **Synchronous Movement Controller** | Keeps two motors in sync during straight travel |
| **Acceleration-Deceleration Controller** | Smooth speed ramp-up and ramp-down by encoder |

### Added in this fork

| Block | Description |
| ----- | ----------- |
| **Color Sensor Speed Controller** | Calculates motor speed from two color sensor values (Linear / Quadratic / Cubic / Sqrt / Step / Smooth modes) with optional smoothing |
| **CS Calibration** | Normalizes raw color sensor values to 0–100 using user-defined white/black calibration points |
| **Advanced Motor Control** | Raw and standard advanced motor power output per port |
| **Advanced Encoder** | Reset, read angle, and read change per motor port |

---

## Usage Guides

Detailed documentation for each block:

| Block | Guide |
| ----- | ----- |
| **PD Controller** | [docs/pd-controller.md](https://github.com/Craft-Core/EV3-AdvMotorControllers-Block-Unofficial-Multi-language-Precision/blob/master/docs/pd-controller.md) |
| **Acceleration-Deceleration Controller** | [docs/acceleration-controller.md](https://github.com/Craft-Core/EV3-AdvMotorControllers-Block-Unofficial-Multi-language-Precision/blob/master/docs/acceleration-controller.md) |
| **Synchronous Movement Controller** | [docs/sync-controller.md](https://github.com/Craft-Core/EV3-AdvMotorControllers-Block-Unofficial-Multi-language-Precision/blob/master/docs/sync-controller.md) |
| **Color Sensor Speed Controller** | [docs/color-sensor-speed-controller.md](https://github.com/Craft-Core/EV3-AdvMotorControllers-Block-Unofficial-Multi-language-Precision/blob/master/docs/color-sensor-speed-controller.md) |

---

## Multi-Language Support

All blocks are fully localized for 15 languages:

| Language | Folder |
| -------- | ------ |
| English (US) | en-US |
| English (GB) | en-GB |
| Japanese (日本語) | ja |
| German (Deutsch) | de |
| French (Français) | fr |
| Spanish (Español) | es |
| Italian (Italiano) | it |
| Dutch (Nederlands) | nl |
| Portuguese (Português) | pt |
| Russian (Русский) | ru |
| Korean (한국어) | ko |
| Simplified Chinese (简体中文) | zh-Hans |
| Danish (Dansk) | da |
| Norwegian (Norsk) | nb-NO |
| Swedish (Svenska) | sv |

---

## Credits

- Original block: **OFDL / a10036gt** — <https://github.com/a10036gt/EV3-AdvMotorControllers-Block>
- Original user guide (繁體中文): <https://ofdl.tw/ev3-hack/adv-motor-controllers-block/>
- Original user guide (English): <https://ofdl.tw/en/ev3-hacking/advanced-motor-controllers-block/>
