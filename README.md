# Plant 2: an open manufacturing dataset

**13 weeks of data from one made-up packaging plant: production, downtime, quality, maintenance, energy, safety, supply chain and people. Something went wrong at Plant 2. Several things, actually. Can you find them?**

Public manufacturing datasets usually cover one thing: a sensor stream, a fault label, a single machine. Real plants don't work that way. A label supplier change shows up as labeler jams, then scrap, then customer complaints, then overtime. The evidence is spread across five systems that don't talk to each other.

Plant 2 puts all of it in one place. It's built for:

- **Testing AI tools** (agents, LLM analysts, MCP servers) on messy, connected plant data.
- **Training** engineers, supervisors and analysts: OEE, Pareto, SPC, energy baselines, PM analysis, supplier scorecards.
- **Building demos** without exposing a real plant's data.

Every tool in the [Plant Pulse](https://github.com/ivanegetov-lab/plant-pulse) family uses this plant. Plant Pulse's sample report is week 45 of this dataset: the downtime log, OEE trend, safety and labor numbers match.

## The plant

Plant 2 fills and packs liquid household products on three lines, three shifts, Monday to Friday. See [`plant.md`](plant.md) for the full description: lines, equipment, products, shifts, costs and targets.

| | Line 1 | Line 2 | Line 3 |
|---|---|---|---|
| Products | All-purpose cleaner 1 L (2 scents) | Fabric softener 2 L and 500 ml | Dish soap 750 ml (regular, eco) |
| Ideal rate | 100 bottles/min | 70 (2 L) / 140 (500 ml) | 110 |
| Equipment | Filler → capper → labeler → case packer → palletizer, linked by conveyors | same | same (labeler new in 2025) |

Period: **Monday 10 Aug to Sunday 8 Nov 2026** (ISO weeks 33–45).

## What's inside

| Folder | File | Rows | What it is |
|---|---|---|---|
| `production/` | `production_log.csv` | 581 | One row per line per shift: planned and run minutes, counts, rejects |
| | `downtime_events.csv` | 785 | Every stop: start, line, asset, cause, minutes, operator comment |
| | `changeovers.csv` | 119 | Product changeovers with from/to SKU and minutes |
| | `shift_notes.csv` | 84 | Supervisor and maintenance notes, free text |
| `quality/` | `fill_weights.csv` | 23,240 | Hourly SPC samples, 5 bottles each, with spec limits |
| | `scrap_log.csv` | 270 | Scrapped units and cost by day, line and SKU |
| | `customer_complaints.csv` | 5 | Complaints with lot codes |
| `maintenance/` | `assets.csv` | 46 | Asset register (criticality left blank on purpose) |
| | `pm_schedule.csv` | 44 | Preventive maintenance tasks and frequencies |
| | `work_orders.csv` | 359 | CMMS export: PM, corrective and requests, with closeout comments |
| | `spare_parts.csv`, `parts_usage.csv` | 30, 55 | Stores list and parts issued to work orders |
| `energy/` | `meters_15min.csv` | 8,736 | 15-minute kW for each line, compressed air, HVAC and lighting |
| `safety/` | `near_misses.csv`, `incidents.csv` | 46, 6 | Near-miss reports (free text) and injuries |
| `supply_chain/` | `receipts.csv` | 237 | Purchase order receipts: promised vs received, lots, incoming inspection |
| `people/` | `labor_weekly.csv` | 13 | Scheduled, overtime and absence hours by week |
| `plant/` | `skus.csv` | 6 | Products, rates, costs and fill specs |

Column-by-column definitions: [`data_dictionary.md`](data_dictionary.md). Total size is about 2 MB, all CSV.

## Like a real plant, the data is messy

- Free-text comments with inconsistent wording.
- Failure codes that don't always match what happened.
- A planned holiday shutdown, a meter outage, a sensor glitch, a keying error, duplicate work orders.
- Some things look like problems and aren't. Some problems hide behind numbers that look fine.

## The challenge

There are **at least 8 problems** buried in these 13 weeks. Some cost money every hour, some are slow drifts, one is a safety risk, and some only show up when you join two or three files.

For each one you find, write down:

1. **What** the problem is.
2. **When** it started (and ended, if it did).
3. **Why**: the root cause, as far as the data supports it.
4. **Evidence**: which files and numbers show it.
5. **What it cost**, where you can put a number on it (minutes, dollars, kWh, risk).

Use any approach: a spreadsheet, Python, a BI tool, an AI agent, or a mix. Send your findings to [Ivan Getov on LinkedIn](https://www.linkedin.com/in/ivan-getov-mba/) with a short note on how you found them. The answer key stays private so the challenge stays fair.

## Rules for using it

- Everything here is **fictional**. The plant, products, suppliers, people and numbers were generated. Any match with a real company is a coincidence.
- License: [CC BY 4.0](LICENSE). Use it for anything, including commercial work and training. Credit "Plant 2 dataset by Ivan Getov" with a link to this repo.

## About

Made by [Ivan Getov](https://www.linkedin.com/in/ivan-getov-mba/), chemical engineer and manufacturing excellence leader, author of *Fix the System: A Maintenance Manager's Field Manual*. Free tools at [tools.getov.xyz](https://tools.getov.xyz), weekly notes at [getov.substack.com](https://getov.substack.com).
