# Crash radar — parameters doc (template)

Copy this into a Google Doc and fill it in. The [crash radar prompt](../prompts/02-portfolio-crash-radar.md) reads it on every run, so you change your rules here in plain language instead of editing the prompt. All numbers below are **examples**; set your own.

---

## 1. Positions

The broker is the source of truth for units and average price. This table is the source of truth for what you *intend* to hold.

| Ticker | Type | Band (min–max %) | Target % | Live stop (trigger) | Hard cap % |
|---|---|---|---|---|---|
| VOO | Core | 22–30 | 26 | — | — |
| VEA | Core | 9–13 | 11 | — | — |
| VWO | Core | 7–11 | 9 | — | — |
| VXF | Core | 5–9 | 7 | — | — |
| VGT | Thematic | 5–9 | 7 | — | — |
| XLV | Sector | 4–8 | 6 | — | — |
| GLDM | Ballast | 9–13 | 11 | — | — |
| XYZ | Single stock | 4–8 | 6 | 100.00 | 8 |

Concentration bucket: `VGT + XYZ`, limit 25%.

## 2. The two keys

A key turns **red** when 2 of its 3 signals are on.

**Price key**
- a) S&P 500 below its 200-day average for 3 consecutive closes
- b) Benchmark ETF (VOO) ≤ −10% from its 52-week high
- c) Less than 40% of S&P 500 stocks above their 200-day average

**Stress key**
- a) High-yield spread above 5.0%, or up 1.5 points in 3 months
- b) VIX above 30 and above VIX3M
- c) Sahm rule at or above 0.50

## 3. Overall level

Define your own mapping. Example:

| Level | Condition |
|---|---|
| GREEN | Both keys off, no more than 1 signal on in total |
| YELLOW | 2+ signals on, but no key red |
| ORANGE | One key red |
| RED | Both keys red |

## 4. Crisis playbook

What you will do at each level, written now while you are calm.

- **GREEN:** keep contributing to positions below their band. Nothing else.
- **YELLOW:** pause contributions to thematic positions; keep contributing to the core.
- **ORANGE:** review every position marked REVIEW THESIS. No core sales.
- **RED:** follow the trend rule only. No panic sales.
- **Band rule:** if VOO goes above 24%, sell just enough to return to 20%.
- **Trend rule:** if the S&P 500 closes a month below its 10-month average, move 1/3 of VOO to SGOV. Buy back when it closes a month above.

## 5. Open to-dos

- Example: confirm the XYZ stop quantity matches the position after the last purchase.
- Example (Resolved): update average price after October contribution.
