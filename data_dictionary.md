# Data dictionary

All files are UTF-8 CSV with a header row. Times are local plant time, `YYYY-MM-DD HH:MM`. Blank means missing or not applicable.

## production/production_log.csv
One row per line per production shift.

| Column | Meaning |
|---|---|
| date, shift | Shift date (C shift belongs to the day it starts) and shift letter A/B/C |
| line | Line 1, Line 2, Line 3 |
| sku | Product running that shift |
| planned_min | Planned production time (450) |
| downtime_min | Sum of downtime events in the shift |
| run_min | planned_min − downtime_min |
| ideal_rate_per_min | Nameplate bottles per minute for the SKU |
| total_count, reject_count, good_count | Bottles made, rejected, good |

OEE for any group of rows = Σ(good_count ÷ ideal_rate_per_min) ÷ Σ planned_min.

## production/downtime_events.csv
| Column | Meaning |
|---|---|
| start | Event start |
| date, shift, line | Production shift the event belongs to |
| asset_id | Asset that stopped, if the operator knew it |
| cause | Cause category picked by the operator |
| minutes | Duration |
| operator_comment | Free text |

## production/changeovers.csv
date, shift, line, from_sku, to_sku, minutes. Each changeover also appears in `downtime_events.csv` with cause `Changeovers`.

## production/shift_notes.csv
date, shift, area, author (Supervisor / Maintenance), note (free text).

## quality/fill_weights.csv
| Column | Meaning |
|---|---|
| timestamp | Sample time (about hourly while the line runs) |
| line, sku | Where and what |
| sample_id, bottle | Subgroup id and bottle 1–5 in the subgroup |
| fill_g | Net fill weight in grams |
| target_g, lsl_g, usl_g | Fill target and spec limits for the SKU |

## quality/scrap_log.csv
date, line, sku, units_scrapped, unit_cost_usd, scrap_cost_usd.

## quality/customer_complaints.csv
received_date, sku, lot_code (`P2-<line>-<yymmdd>-<shift>`), category, description.

## maintenance/assets.csv
asset_id, name, line, area, type, manufacturer, install_year, installed_spare (Yes if a backup unit is installed), status (Active / Decommissioned), criticality (blank: score it yourself).

## maintenance/pm_schedule.csv
pm_id, asset_id, task, frequency_days, estimated_hours.

## maintenance/work_orders.csv
| Column | Meaning |
|---|---|
| wo_id | Work order number |
| type | PM (preventive), CM (corrective), REQ (facility request) |
| asset_id | Asset worked on (blank for some requests) |
| priority | 1 = emergency … 4 = low |
| created_at, due_date, started_at, completed_at | Dates and times |
| status | Closed, Open, Closed - not done |
| description | What was asked or found |
| labor_hours, technicians | Hours booked and crew size |
| failure_code | SEAL, ADJ, ELEC, MECH, BEAR, JAM, OTHER, or blank |
| closeout_comment | Technician's closing note |
| pm_id | PM task that generated the work order (PM only) |
| technician | Who closed it |

## maintenance/spare_parts.csv
part_no, description, used_on, on_hand, min_qty, max_qty, unit_cost_usd, lead_time_days.

## maintenance/parts_usage.csv
date, wo_id, part_no, qty.

## energy/meters_15min.csv
timestamp (start of the 15-minute interval), line1_kw, line2_kw, line3_kw, compressed_air_kw, hvac_kw, lighting_kw, total_kw (blank if any meter is missing or invalid). Average kW over the interval; kWh = kW × 0.25.

## safety/near_misses.csv
date, shift, area, source (Verbal / App / Walkway card), description.

## safety/incidents.csv
date, shift, area, type (Recordable / First aid), description.

## supply_chain/receipts.csv
| Column | Meaning |
|---|---|
| po_id, supplier, material | Purchase order and what was bought |
| order_date | Date the PO was placed |
| promised_at, received_at | Promised and actual delivery time |
| qty_ordered, qty_received, unit | Quantities |
| lot | Supplier lot |
| incoming_inspection | Result of the receiving check |
| comment | Receiving notes (labels: liner caliper measurement) |

## people/labor_weekly.csv
iso_week, week_start, scheduled_hours, overtime_hours, absence_hours (production and maintenance combined).

## plant/skus.csv
sku, description, line, fill_ml, units_per_case, ideal_rate_per_min, unit_cost_usd (filled, labeled bottle), fill_target_g, fill_lsl_g, fill_usl_g.
