# Holdover Time Calculator (GNSS-Denied Timing)

A free, single-file web tool that estimates the **accumulated time error of a free-running oscillator during GNSS holdover** — for example after jamming, spoofing detection, antenna failure or an indoor outage. Enter the initial frequency offset, the aging rate and the holdover duration to get the time error, the frequency offset at time t, the time-error curve, and how long until a 1 μs / 1 ms / 10 ms error threshold is crossed.

## Online use

Open the tool directly in your browser (no install, no dependencies, all math runs client-side):

**https://xiaokeni2.github.io/holdover-time-calculator/**

## What it does

- Inputs: initial frequency offset Δf₀ (ppb), oscillator aging rate (ppb/day) and run time (hours or days).
- One-click presets for typical aging rates (order-of-magnitude, verify against datasheets):
  - OCXO ≈ 1×10⁻¹⁰/day
  - Rubidium ≈ 5×10⁻¹¹/month (≈ 1.7×10⁻¹²/day)
  - Caesium beam ≈ 1×10⁻¹² over its service life (≈ 10 years)
  - TCXO ≈ 1×10⁻⁸/day
- Outputs: frequency offset at t, accumulated time error TE(t) in ns/μs/ms/s, time to 1 μs / 1 ms / 10 ms thresholds, and an SVG time-error curve.
- Background sections on holdover, GNSS jamming/spoofing and how to extend holdover capability.
- Pure HTML/CSS/JS, dark engineering UI, mobile friendly.

## Formulas

```
Δf(t)  = Δf₀ + a·t_day                        (fractional frequency offset)
TE(t)  = Δf₀·t_s + a·t_s² / (2·86400)          (seconds; t_s = time in seconds)
```

The linear term integrates the initial frequency error; the quadratic term accumulates aging. Assumptions: constant temperature and linear aging — temperature-induced frequency shifts (an uncontrolled shelter can dominate) and aging non-linearity/retrace are not modeled.

## Usage

1. Enter the frequency error at the moment GNSS is lost (e.g. 1.0 ppb for a typical disciplined OCXO).
2. Click an aging preset or type your oscillator's aging rate (e.g. 0.1 ppb/day).
3. Enter the expected holdover duration (e.g. 24 h or 7 days).

Example: Δf₀ = 1 ppb, aging = 0.1 ppb/day, t = 1 day → TE ≈ 86.4 μs + 4.3 μs ≈ 90.7 μs.

## Related

- [BRIDZA RF — OCXO, rubidium & timing components](https://rf.bridza.com/)
- [Standalone vs GNSS-disciplined holdover analysis](https://rf.bridza.com/resources/comparisons/br012.html)
- [STM-RB-NC rubidium oscillator module](https://rf.bridza.com/products/stm-rb-nc.html)
- [BD1024-C GNSS-disciplined timing board](https://rf.bridza.com/products/bd1024-c.html)

---

More free RF/timing tools: [VSWR Calculator](https://xiaokeni2.github.io/vswr-return-loss-calculator/) · [Phase Noise–Jitter Converter](https://xiaokeni2.github.io/phase-noise-jitter-converter/) · [Clock Tree Jitter Budget Calculator](https://xiaokeni2.github.io/clock-tree-jitter-budget-calculator/) · [LEO Doppler Calculator](https://xiaokeni2.github.io/leo-doppler-calculator/)

© BRIDZA · Open code, free to use.
