# Marketplace Operations & Fulfillment SLA Diagnostics Engine

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-Operational%20Analytics-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-Statistical%20Visualization-teal)
![License](https://img.shields.io/badge/License-MIT-green)

An end-to-end operational analytics framework designed to diagnose micro-hub warehouse fulfillment, courier dispatch friction, weather sensitivity, driver idle-time loss, and customer support escalation across 1,000 marketplace dispatches.

---

## Executive Summary

In hyper-local, on-demand marketplaces and quick-commerce platforms, gross order volume often obscures severe supply-chain friction. While high-level delivery completion rates typically sit near 100%, true operational profitability is dictated by controllable execution inputs: warehouse pick-and-pack seconds, courier curb staging, weather resilience, and dispute mitigation.

This project analyzes 1,000 multi-node dispatches across 4 regional fulfillment hubs to decouple warehouse bottlenecks from street transit delays. Rather than treating delivery failure as an isolated event, this framework isolates the compounding effects of operational defects on customer CSAT scores, live support ticket escalations, and reverse-logistics margin bleed.

---

## Key Business Objectives & Achievements

* **Fulfillment Stage Decomposition:** Splits total order cycle time into warehouse pick & pack duration versus last-mile street transit to isolate upstream shelving delays from road congestion.
* **The "Perfect Order Rate" (POR) North Star:** Disproves the vanity metric of ~100% "Delivery Completion Rate" by quantifying the true platform Perfect Order Rate (~62% on-time, zero support tickets, zero returns).
* **Environmental Elasticity Modeling:** Measures how adverse weather events (storms, severe heat) degrade fixed customer SLA commitments across Instant, Same-Day, and Standard tiers.
* **Fleet Labor & Dispatch Optimization:** Identifies labor wage waste from idle dedicated couriers waiting in staging bays due to premature dispatch triggers.
* **Downstream Unit Economics Protection:** Connects SLA delivery delays directly to the customer CSAT drop-off cliff (collapsing from 4.4 to 2.0 stars) and quantifies the cost of customer support ticket escalations ($4–$7 per incident).

---

## Analytical Architecture & 10 Core Frameworks

| # | Analytical Framework | Statistical / Visual Technique | Operational Problem Solved |
|---|----------------------|--------------------------------|----------------------------|
| **1** | **Hub Fulfillment Pick & Pack Bottlenecks** | Grouped Bar Chart | Uncovers that warehouse pick delays consume up to 33% of the total customer SLA window in suburban hubs before dispatch. |
| **2** | **Adverse Weather Sensitivity** | Diverging Point Plot | Demonstrates that storm events drive Instant delivery breach rates from 18% to nearly 58%, validating dynamic ETA buffering. |
| **3** | **Fleet Model Idle Time Waste** | Scatter Plot + Linear Fit | Profiles Dedicated In-House vs. Gig Contractor fleets, exposing driver idle costs during off-peak volume windows. |
| **4** | **Customer Support Ticket Escalations** | Stacked Horizontal Bar | Measures compound operational defects, revealing an 88% ticket escalation rate when late deliveries coincide with returns. |
| **5** | **Category Return Friction** | Lollipop / Stem Plot | Pinpoints reverse-logistics capacity drains, showing Apparel drives a 26.5% return rate (over 3x other categories). |
| **6** | **CSAT Rating Degradation Curve** | Violin Distribution | Uncovers the customer sentiment cliff: missed SLAs trigger an immediate drop to a 2.0 median rating with >45% 1-star reviews. |
| **7** | **Cargo Weight vs. Transit Velocity** | Multi-Variable Scatter Plot | Identifies the physical cargo limit (>6.0–7.5 kg) where two-wheeler transit velocity collapses, requiring 3-wheel EV or van dispatch. |
| **8** | **Hub-to-Hub Fulfillment Error Matrix** | Matrix Heatmap | Diagnoses suburban micro-hub overextension, showing Suburban-West incurs a 34% breach rate vs. 16% in Metro-North. |
| **9** | **Rider Idle vs. Warehouse Lag** | 2D Bivariate KDE Contour | Proves dispatch algorithms call drivers 10–14 minutes too early while warehouse picking is still underway. |
| **10** | **Executive Fulfillment Outcome Health** | Donut Chart with KPI Ring | Replaces top-line completion metrics with the true Perfect Order Rate (~62%), surfacing 38% hidden operational waste. |

---

## Dataset Schema

The synthetic dataset (`marketplace_operations.csv`) contains 1,000 multi-hub fulfillment logs with zero missing or null values:

* `order_id`: Unique dispatch consignment identifier (`ORD-50000` to `ORD-50999`)
* `city_hub`: Regional dispatch node (`Metro-North`, `Metro-South`, `Suburban-East`, `Suburban-West`)
* `product_category`: Merchandise line (`Consumer Electronics`, `Apparel`, `Fresh & Grocery`, `Home & Kitchen`, `Beauty & Care`)
* `delivery_type`: Customer service level commitment (`Instant (15-30m)`, `Same-Day`, `Standard 2-Day`)
* `fleet_type`: Delivery courier labor model (`Gig Contractor`, `Dedicated 3PL`, `In-House Fleet`)
* `weather`: Ambient atmospheric condition during transit (`Clear`, `Rain/Storm`, `Extreme Heat`)
* `package_weight_kg`: Consignment cargo weight (0.2 to 12.0 kg)
* `driver_idle_prior_min`: Courier wait time at hub staging bay before order assignment
* `pick_pack_time_min`: Internal warehouse picking, sorting, and bagging duration
* `transit_time_min`: In-transit road duration from hub departure to customer doorstep
* `total_delivery_time_min`: End-to-end order cycle duration (`pick_pack_time_min` + `transit_time_min`)
* `delivery_sla_min`: Guaranteed customer commitment SLA in minutes (30, 240, or 2880 min)
* `is_sla_breached`: Binary fulfillment breach status (`0` = On-Time, `1` = SLA Breached)
* `customer_rating`: Post-delivery CSAT evaluation (1 to 5 stars)
* `ticket_escalated`: Binary customer support contact status (`0` = Resolved Clean, `1` = Ticket Filed)
* `return_requested`: Binary reverse-logistics flag (`0` = Kept, `1` = Return Initiated)

---

## Key Executive Takeaways & Recommendations

1. **Deploy Predictive Courier Dispatch:** Drivers currently wait idle for 10–14 minutes in hub staging lots because dispatch triggers upon order creation. Shifting to predictive dispatch—calling drivers only when warehouse picking hits ≥70% completion—eliminates yard congestion and driver idle compensation.
2. **Implement Dynamic Weather Buffering:** Static 30-minute delivery promises fail during storm events (breaches spike to 58%). Integrate live weather radar feeds into checkout promises, automatically adding a +10 to +15 minute buffer to protect customer expectations and CSAT.
3. **Automate Heavy Consignment Routing:** Consignments exceeding 6.0 kg cause transit delays and safety risks on two-wheelers. Enforce hard automated vehicle profiles in the dispatch routing engine, reassigning bulky cargo exclusively to three-wheeler EVs or delivery vans.
4. **Rebalance Suburban Dark-Store Geofences:** Peripheral suburban hubs face double the breach rate of central metro nodes due to courier dispersion over wide areas. Contract the guaranteed Instant delivery radius for suburban hubs from 7 km to 4.5 km or deploy micro-fulfillment dark stores.
5. **Establish Proactive Support Ticket Deflection:** Late deliveries paired with return requests escalate to expensive live support agents in 88% of cases. Deploy automated deflection: if telematics detects an SLA breach >10 minutes, proactively push an in-app apology credit before the customer files a complaint.

---

## Repository Structure

```text
├── data/
│   └── marketplace_operations.csv              # Generated 1,000-dispatch clean dataset
├── scripts/
│   ├── generate_marketplace_data.py            # Telemetry dataset generator
│   └── run_marketplace_analytics.py            # Complete analytics suite and visualizations
├── notebooks/
│   └── marketplace_fulfillment_analysis.ipynb  # Interactive walkthrough of all 10 analyses
├── docs/
│   └── operations_brief.md                     # Comprehensive operational findings and inferences
└── README.md                                   # Project documentation