# OFDL Acceleration Controller — Usage Guide

Generates a smooth speed profile that ramps **up** from `MinPwr` to `MaxPwr` over `AccelDist` degrees, runs at `MaxPwr` through the middle, then ramps **down** back to `MinPwr` over `DecelDist` degrees — all based on live encoder readings.

---

## Concept

```
Encoder position →

0 ────── AccelDist ──────── (FullDist − DecelDist) ──────── FullDist
│ ramp up │       full speed        │      ramp down      │
MinPwr → MaxPwr              MaxPwr              MaxPwr → MinPwr
```

The block **outputs a speed value** — wire it into your motor power input each loop iteration. It does not drive motors directly.

---

## Setup

### Step 1 — Configuration block (run once before the loop)

| Parameter | Description | Typical value |
|-----------|-------------|---------------|
| **EncPort** | Encoder motor ports | `1.B+C` |
| **MaxPwr** | Peak speed (−100 to 100) | `90` |
| **MinPwr** | Minimum speed at start/end (−100 to 100) | `15` |
| **AccelDist** | Acceleration distance (degrees) | `300` |
| **DecelDist** | Deceleration distance (degrees) | `300` |
| **FullDist** | Total travel distance (degrees) | `1000` |

### Step 2 — Output block (run every loop iteration)

#### Outputs

| Output | Description |
|--------|-------------|
| **Output** | Current speed to apply to motors |
| **E1Output** | Current encoder 1 reading (degrees) |
| **E2Output** | Current encoder 2 reading (degrees) |
| **Finish** | `True` when `FullDist` has been reached |

---

## Modes

| Mode | Description |
|------|-------------|
| `Configuration` | Set all parameters (call once before loop) |
| `ACDC_Output1Degs` | Output speed using encoder 1 only |
| `ACDC_Output2Degs` | Output speed using both encoders (averaged) |

---

## Typical loop structure

```
[Reset encoders (Advanced Encoder block)]
[Configuration: EncPort=B+C, MaxPwr=90, MinPwr=15, AccelDist=300, DecelDist=300, FullDist=1000]

Loop until Finish = True:
  [ACDC_Output2Degs] → Output, E1Output, E2Output, Finish
  [Drive motors with Output]
  [PD Controller if line following]
```

---

## Tips

- Always **reset encoders** before starting (use the Advanced Encoder `EncReset` block).
- `AccelDist + DecelDist` must be less than `FullDist`, otherwise the profile overlaps.
- Combine with the **PD Controller** (`PDpwr_*` modes) for smooth line-following at variable speed: feed `Output` as the power input to the PD block.
- Use `ACDC_Output1Degs` for single-motor tasks; use `ACDC_Output2Degs` for two-motor drives to account for encoder drift.
