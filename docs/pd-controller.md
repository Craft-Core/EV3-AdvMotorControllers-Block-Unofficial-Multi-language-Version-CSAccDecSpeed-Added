# OFDL PD Controller — Usage Guide

A line-following PD (Proportional-Derivative) controller that reads two color sensors and drives two motors to keep the robot centered on the line.

---

## Concept

```
error      = P1 − P2
derivative = error − prev_error

correction = Kp × error + Kd × derivative

left_motor  = Power + correction
right_motor = Power − correction
```

- **P control only** (`P_*` modes): uses only `Kp × error`
- **PD control** (`PD_*` modes): uses both `Kp` and `Kd`
- **PDpwr** (`PDpwr_*` modes): same as PD, but reads Power from global config

---

## Setup

### Step 1 — Configuration block (run once before the loop)

| Parameter | Description | Typical value |
|-----------|-------------|---------------|
| **Ports** | Motor ports (B+C) | `1.B+C` |
| **Kp** | Proportional gain | `0.3` |
| **Kd** | Derivative gain | `0.7` |
| **Power** | Base motor speed (−100 to 100) | `50` |

### Step 2 — Control block (run every loop iteration)

| Parameter | Description |
|-----------|-------------|
| **P1** | Left color sensor raw value |
| **P2** | Right color sensor raw value |

---

## Modes

| Mode | Category | Description |
|------|----------|-------------|
| `Configuration` | — | Set Kp, Kd, Power, Ports (call once) |
| `P_Large` | P\_byVars | P control, large motor ports |
| `P_Medium` | P\_byVars | P control, medium motor ports |
| `P_twoRev` | P\_byVars | P control, reversed motor direction |
| `PD_Large` | PD\_byVars | PD control, large motor ports |
| `PD_Medium` | PD\_byVars | PD control, medium motor ports |
| `PD_twoRev` | PD\_byVars | PD control, reversed motor direction |
| `PDpwr_Large` | PDpwr\_byVars | PD + configurable power, large motors |
| `PDpwr_Medium` | PDpwr\_byVars | PD + configurable power, medium motors |
| `PDpwr_twoRev` | PDpwr\_byVars | PD + configurable power, reversed |

---

## Typical loop structure

```
[Configuration: Ports=B+C, Kp=0.3, Kd=0.7, Power=50]

Loop:
  [Read Color Sensor 1] → P1
  [Read Color Sensor 2] → P2
  [PD_Large: P1, P2]
```

---

## Tips

- Start with `Kp=0.3, Kd=0.7`. Increase `Kp` for faster correction; increase `Kd` to reduce oscillation.
- Use `PDpwr_*` modes when you want to vary speed dynamically (e.g., combined with the Acceleration Controller).
- Use `P_twoRev` / `PD_twoRev` if your robot's left and right motors are mounted in opposite orientations.
