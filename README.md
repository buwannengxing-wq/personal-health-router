# personal-health-router

Hermes Agent skill for personal health tracking — meals, sleep, and exercise with automated Feishu/Lark Bitable persistence and reporting.

## Overview

This skill provides a unified health management layer for the Hermes Agent, handling:

- **Nutrition**: Photo-based calorie and macro estimation from meal images
- **Sleep**: Screenshot-based extraction of sleep stages and recovery signals
- **Exercise**: Extraction of workout metrics from app screenshots (Garmin, Strava, etc.)
- **Cross-domain reporting**: Weekly/monthly health assessments and dashboards

All data persists to Feishu/Lark Bitable tables with automated bootstrapping and refresh scripts.

## Installation

```bash
# Install via ClawHub (recommended)
clawdhub install personal-health-router

# Or clone this repo manually
git clone https://github.com/YOUR_HANDLE/personal-health-router.git
```

## Quick Start

1. **Configure**: Copy `references/config-template.md` to `config.json` and fill in your Feishu app credentials
2. **Bootstrap tables**: `node scripts/bootstrap_health_tables.js config.json`
3. **Track**: Send meal photos, sleep screenshots, or workout summaries to the Hermes Agent
4. **Report**: Run scripts in `scripts/` to generate weekly and monthly health reports

## Project Structure

```
personal-health-router/
├── SKILL.md                    # Main skill definition
├── README.md
├── references/
│   ├── config-template.md      # Config file template
│   ├── nutrition.md            # Nutrition branch rules
│   ├── exercise.md             # Exercise branch rules
│   ├── sleep.md                # Sleep branch rules
│   ├── cross-domain.md         # Reporting rules
│   └── data-model.md           # Data model documentation
└── scripts/
    ├── bootstrap_health_tables.js   # Create Bitable tables
    ├── rebuild_monthly_calendar.py  # Monthly aggregation
    ├── rebuild_weekly_assessment.py # Weekly reports
    └── build_monthly_dashboard.js   # Dashboard refresh
```

## Configuration

See `references/config-template.md` for all available configuration options.

Required environment variables:
- `FEISHU_APP_ID` — Feishu app ID
- `FEISHU_APP_SECRET` — Feishu app secret
- `FEISHU_BASE_TOKEN` — Target Bitable base token

## License

MIT
