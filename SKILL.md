---
name: strikeradar
description: Monitor US-Iran strike probability with real-time signals. Use when user asks about "Iran strike probability", "strike radar", "Iran situation", "US attack Iran", "flights over Iran", "Iran internet", "oil prices Iran", "Pentagon activity", "Polymarket Iran", "הסתברות תקיפה באיראן", "מצב איראן", "תקיפה אמריקאית", or "סטרייק ראדאר".
license: MIT
compatibility: Requires Node.js 18+ with tsx, and internet access
metadata:
  author: Alex Polonsky
  github: https://github.com/alexpolonsky
  version: "1.0.0"
  keywords: geopolitics, iran, risk-monitor, strike-radar, osint
  openclaw:
    emoji: "🎯"
    os:
      - darwin
      - linux
    requires:
      bins:
        - node
---

# StrikeRadar - US-Iran strike probability monitor

Real-time risk scores across 8 signal categories, aggregated into a composite strike probability.

Risk scores are algorithmic estimates from publicly available data, not intelligence assessments. Do not use for personal, financial, or safety decisions. Wraps [StrikeRadar](https://usstrikeradar.com/) by Yonatan Back.

## Quick Start

No dependencies needed. Run directly:
```bash
npx tsx {baseDir}/scripts/strikeradar.ts status
```

## Commands

| Command | Description |
|---------|-------------|
| `status` | All 8 signals with risk scores and total risk |
| `signal <name>` | Deep dive into one signal with raw data |
| `pulse` | Live viewer count and activity by country |

### Status
```bash
npx tsx {baseDir}/scripts/strikeradar.ts status
```
Returns: total_risk (0-100%), per-signal risk + detail, last_updated.

### Signal deep-dive
```bash
npx tsx {baseDir}/scripts/strikeradar.ts signal <name>
```
Valid signals: `news`, `connectivity`, `energy`, `flight`, `tanker`, `weather`, `polymarket`, `pentagon`

**What each signal tracks:**
- **news** - article alerts from BBC/Al Jazeera, alert_count, total_count
- **connectivity** - Iran internet status via Cloudflare Radar
- **energy** - Brent crude price, volatility, market status
- **flight** - aircraft count near Iran, key airline presence
- **tanker** - military refueling tanker detection, callsigns
- **weather** - conditions over Iran (visibility matters for strikes)
- **polymarket** - betting market odds for US strike
- **pentagon** - building activity level and patterns

### Pulse
```bash
npx tsx {baseDir}/scripts/strikeradar.ts pulse
```
Returns: watching_now, activity_level, surge multiplier, country breakdown.

## Agent Usage

All commands return JSON with `next_actions` when output is piped:
```bash
npx tsx {baseDir}/scripts/strikeradar.ts status | cat
```
