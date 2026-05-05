# Nutrition Branch (Unified)

Use this branch for meal recognition, calorie estimation, and Feishu logging.

## Scope
- Analyze meal photos or food descriptions.
- Map a structured meal result into a Feishu nutrition-meal schema.
- Rebuild nutrition daily history when required.

## Recognition Rules
- Extract only visible food items.
- Estimate calories, protein, sodium, carbs, fat, and fiber conservatively.
- State uncertainty when portions or hidden ingredients (e.g., oil, salt) are unclear.

## Persistence Rules (Feishu)
- Use `lark-cli base +record-upsert --json` (NOT `--field`).
- **`--field` flag is NOT supported** by `+record-upsert`; pass a JSON object via `--json`.
- The nutrition table uses **Chinese field names** (not English-only): `日期时间`, `食物描述`, `估算卡路里(kcal)`, `蛋白质(g)`, `钠(mg)`, `碳水(g)`, `脂肪(g)`, `膳食纤维(g)`, `估算重量(g)`, `份量说明`, `置信度(0-1)`, `备注`, `营养简报`.
- Micronutrient fields: `维生素C(mg)`, `维生素A(μg RAE)`, `钙(mg)`, `铁(mg)`, `镁(mg)`, `叶酸B9(μg)`, `钾(mg)`.
- Always `--field-list` first to discover exact field names before writing.

## Known Base & Tables (May 2026)
- Base token: `Ww6RbYVfVa0EAIsAk3ucaWt7nUv` (健康记录 v2)
- Nutrition table: `tblbFxtbGBJ6SWaO` (营养摄入记录)

## Image Analysis
- Use `mcp_minimax_vision_understand_image` for food images.
- `vision_analyze` tool CANNOT access local file paths — use minimax vision MCP instead.

## Standard Upsert Template (correct syntax)
```bash
# List fields first to get exact names:
HOME=/home/neverwarm lark-cli base +field-list \
  --base-token Ww6RbYVfVa0EAIsAk3ucaWt7nUv \
  --table-id tblbFxtbGBJ6SWaO | grep '"name"'

# Upsert using --json (--field is NOT supported):
HOME=/home/neverwarm lark-cli base +record-upsert \
  --as user \
  --base-token Ww6RbYVfVa0EAIsAk3ucaWt7nUv \
  --table-id tblbFxtbGBJ6SWaO \
  --json '{"日期时间":"2026-05-04 09:00","食物描述":"酸奶+燕麦+蓝莓","估算卡路里(kcal)":460,"蛋白质(g)":17,"钠(mg)":180,"碳水(g)":54,"脂肪(g)":18,"膳食纤维(g)":7,"置信度(0-1)":0.75}'
```

## Boundary
Do not mix first-pass recognition with full monthly/weekly rebuilds unless explicitly requested.
