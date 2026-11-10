# Plant 2: plant description

Plant 2 is a fictional liquid household-products packaging plant. Product is batched in two mixing tanks, then filled and packed on three lines. Finished pallets ship from a warehouse with four dock doors.

## Lines

Each line runs the same equipment train, linked by conveyors:

**Filler → capper → labeler → case packer → palletizer**

| Line | Products (SKU) | Ideal rate | Units per case | Notes |
|---|---|---|---|---|
| Line 1 | AC-1000 all-purpose cleaner 1 L, AC-1000-LEM lemon 1 L | 100 bottles/min | 12 | Equipment from 2014. 12-valve rotary filler |
| Line 2 | FS-2000 fabric softener 2 L, FS-0500 500 ml | 70 / 140 bottles/min | 6 / 12 | Equipment from 2017. Size changeovers need change parts from the stores crib |
| Line 3 | DS-0750 dish soap 750 ml, DS-0750-ECO eco refill 750 ml | 110 bottles/min | 12 | Equipment from 2021, pressure-sensitive labeler replaced in 2025 |

Line 4 was decommissioned years ago. Its assets are still in the register and some of its spare parts are still in stores.

## Shifts and calendar

- Three 8-hour shifts, Monday to Friday: **A** 06:00–14:00, **B** 14:00–22:00, **C** 22:00–06:00 (C belongs to the day it starts).
- Planned production time is **450 minutes per shift** (30 minutes of breaks).
- Weekends are off. Occasional Saturday overtime shifts appear in the production log.
- Monday 7 September 2026 (Labor Day) is a planned shutdown.
- About 7 people per line per shift. Maintenance crew of 8 technicians on days, with on-call coverage at night.

## Utilities

- Two rotary screw air compressors: CMP-1 runs, CMP-2 is the backup. One refrigerated dryer.
- Two air handlers (production hall, warehouse) and six roof exhaust fans.
- Electricity costs **$0.11 per kWh**.

## Targets the plant manager uses

| Area | Measure | Target |
|---|---|---|
| Safety | Recordable injuries | 0 |
| Quality | Fill weight | Inside the spec limits in `skus.csv` (target set slightly above label claim) |
| Delivery | OEE (good units at ideal rate ÷ planned time) | 70% |
| Maintenance | PM compliance | 90% |
| Maintenance | Unplanned downtime | 12 h per week, plant |
| Cost | Overtime | 8% of scheduled hours |
| People | Absenteeism | 3.5% |

## Suppliers

| Material | Supplier |
|---|---|
| Bottles | Clearform Bottles |
| Caps | Capitol Closures |
| Labels | Northside Labels (and others) |
| Shipper cases | Ridge Corrugated |
| Chemicals | Midstate Chemicals |

## How the systems relate

- `asset_id` links downtime events, work orders, PMs and the asset register.
- `line` + `date` + `shift` links production, downtime, fill weights, scrap, energy (by timestamp) and shift notes.
- Lot codes on complaints follow `P2-<line>-<yymmdd>-<shift>`, so a complaint can be traced to the shift that made it.
- `wo_id` links parts usage to work orders.
