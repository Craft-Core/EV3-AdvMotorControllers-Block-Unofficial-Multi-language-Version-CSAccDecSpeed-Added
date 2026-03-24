# OFDL MoveSync Controller — Usage Guide

Keeps two motors running at the same speed during straight-line travel by continuously correcting for encoder drift using a P controller.

---

## Concept

```
drift      = E1 − E2
correction = Kp × drift

left_motor  = Power1 − correction
right_motor = Power2 + correction
```

Without synchronization, even identical motors at the same commanded speed will drift apart over time due to mechanical differences. This block eliminates that drift.

---

## Setup

### Step 1 — Configuration block (run once before the loop)

| Parameter | Description | Typical value |
|-----------|-------------|---------------|
| **Ports** | Motor ports | `1.B+C` |
| **Kp** | Sync correction gain | `0.12` |
| **Power1** | Left motor base speed (−100 to 100) | `50` |
| **Power2** | Right motor base speed (−100 to 100) | `50` |
| **LeftInversed** | Invert left motor direction | `False` |
| **RightInversed** | Invert right motor direction | `False` |

### Step 2 — Sync block (run every loop iteration)

| Parameter | Description |
|-----------|-------------|
| **E1** | Left encoder reading |
| **E2** | Right encoder reading |

---

## Modes

| Mode | Description |
|------|-------------|
| `Configuration` | Set Kp, Power1, Power2, Ports, inversion flags (call once) |
| `SYNC_Std` | Sync using configured Power1/Power2 |
| `SYNC_byPwr` | Sync with Power1/Power2 passed each iteration (overrides config) |

---

## Typical loop structure

```
[Reset encoders]
[Configuration: Ports=B+C, Kp=0.12, Power1=60, Power2=60]

Loop:
  [Read Encoder B] → E1
  [Read Encoder C] → E2
  [SYNC_Std: E1, E2]
```

Or with dynamic power:

```
Loop:
  [Read Encoder B] → E1
  [Read Encoder C] → E2
  [SYNC_byPwr: Power1=speed, Power2=speed, E1, E2]
```

---

## Tips

- Set `Power1 = Power2` for straight travel. Intentionally unequal values will produce a consistent arc.
- Use `LeftInversed` / `RightInversed` if your motors are physically mirrored (one faces forward, one faces backward).
- Increase `Kp` for tighter sync; if the robot oscillates, reduce it.
- Combine with the **Acceleration Controller** to keep motors in sync during ramp-up and ramp-down: feed `Output` into `SYNC_byPwr`.
