# personal-health-router

Hermes Agent skill for automated personal health tracking across nutrition, sleep, and exercise, with Feishu/Lark Bitable persistence and automated reporting.

用于个人健康数据自动采集与管理的 Hermes Agent 技能，覆盖饮食、睡眠与运动，并支持飞书 Bitable 持久化与自动化报告生成。

## Overview

This skill provides a unified health management layer for the Hermes Agent, handling:
本能力为 Hermes 智能代理 提供统一健康管理能力层，涵盖以下模块：

- **Nutrition / 营养分析**
  - Input: Meal images  
    输入：餐食图片  
  - Processing: Image-based nutrition analysis  
    处理：基于图像的营养分析  
  - Output: Calorie and macronutrient estimation  
    输出：卡路里与宏量营养素估算  
- **Sleep / 睡眠分析**
  - Input: Sleep screenshots  
    输入：睡眠截图  
  - Processing: Sleep data extraction  
    处理：睡眠数据解析  
  - Output: Sleep stages and recovery signals  
    输出：睡眠阶段与恢复指标  
- **Exercise / 运动分析**
  - Input: App screenshots (Garmin, Strava, etc.)  
    输入：运动应用截图（Garmin、Strava 等）  
  - Processing: Workout data parsing  
    处理：运动数据解析  
  - Output: Structured workout metrics  
    输出：结构化训练指标 
- **Cross-domain Reporting / 跨域报告**
  - Input: Aggregated health data  
    输入：聚合后的健康数据  
  - Processing: Rule-based analysis & aggregation  
    处理：规则分析与数据聚合  
  - Output: Weekly/monthly reports and dashboards  
    输出：周报、月报与健康评估仪表盘  

Transform fragmented health inputs (images/screenshots) into structured data and actionable reports, with all data persisted in Feishu/Lark Bitable and managed via automated bootstrapping and refresh scripts.

将分散的健康图片/截图转化为结构化数据与可持续跟踪的健康报告，并通过飞书 Bitable 持久化存储，配合自动化初始化与刷新脚本进行管理。

## 📊 Example Output / 示例输出

Below is an example of the generated health dashboard based on aggregated data from nutrition, sleep, and exercise inputs.

下图为基于饮食、睡眠与运动数据聚合后自动生成的健康仪表盘示例。

It demonstrates how structured data is visualized into actionable insights, including trends, summaries, and key health metrics.

展示了结构化数据如何转化为可视化健康洞察，包括趋势分析、汇总信息与关键指标。

### 🥗 Nutrition Insights / 营养分析

<img width="2514" height="1336" alt="每日营养最新值 vs 参考值" src="https://github.com/user-attachments/assets/615cd124-9a0d-49cb-9a33-51dcc5561e45" />

- Nutrition trends and calorie distribution  
  营养趋势与热量分布

  ### 😴 Sleep Insights / 睡眠分析
  
<img width="2486" height="1458" alt="睡眠评估" src="https://github.com/user-attachments/assets/1a6d4d78-628b-4416-a15e-6969f152f7d2" />

- Sleep duration and recovery signals  
  睡眠时长与恢复指标

  ### 🏃 Exercise Insights / 运动分析
<img width="2516" height="1368" alt="运动评估" src="https://github.com/user-attachments/assets/f0d6abeb-3ac2-4cab-9f47-1c8a40bf0d50" />

- Exercise frequency and intensity  
  运动频率与强度分析
  
This system forms an end-to-end pipeline from multimodal health inputs to structured data and visualized insights.

该系统构建了从多模态健康输入到结构化数据再到可视化洞察的完整数据链路。


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
