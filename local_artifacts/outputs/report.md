# Cargo Exposure & Risk Intelligence Report

> Run tag: **20260320_182304**  
> Output folder: `outputs`

---

## 1. Executive Summary (1 page)

- **Total exposure analysed:** ₹1.19B
- **Entities covered:** Routes=41 | Carriers=13 | Vehicles=115
- **Concentration insight (80/20 style):**
  - Vehicle concentration: **Top 10 vehicles hold 27.28%** of total exposure (Top 1: 7.48%, Top 3: 14.82%).
  - Route concentration: **Top 10 routes hold 68.67%** of total exposure.
- **Immediate underwriting red flags:**
- **Route risk hotspots**: highest risk-score routes include Vadodara → Cuttack, Vadodara → South West Delhi, Vadodara → Visakhapatnam.

---

## 2. Data Coverage & Quality

### Quality gates (exported)
- CSV: `L0_quality_gates_summary__20260320_182304.csv`
- Summary table:

| gate                        | status   | notes                                                             |
|:----------------------------|:---------|:------------------------------------------------------------------|
| exposure_value_non_negative | PASS     | negative rows: 0                                                  |
| exposure_value_non_null     | PASS     | non-null: 134/134                                                 |
| route_fields_present        | PASS     | present=['destination_city', 'origin_city']                       |
| distance_km_non_null        | PASS     | non-null: 124/134                                                 |
| distance_km_near_zero_check | PASS     | near-zero (<5km) rows: 0 (intracity or same-city legs)            |
| duplicate_key_check         | PASS     | strict 12-digit eWayBill duplicated count: 0 | missing/blank: 134 |
| geo_columns_present         | PASS     | present=['origin_lat', 'origin_lon', 'dest_lat', 'dest_lon']      |

### Known blind spots
- Driver-level identifiers are not used as primary keys in this report (high churn, reassignment, and masking effects).

### Why this data is still decision-grade
This dataset is decision-grade because it quantifies **where the money moves** (exposure concentration) and **where operational stress accumulates** (route/carrier/vehicle clusters). Even without claims, these are the right levers for underwriting controls: **sub-limits, deductibles, route conditions, carrier tiering, and inspection triggers**.

---

## 3. Route Risk Spine

### Top 10 risky routes (by risk score)
| route                       |   trip_count |   total_exposure |   avg_distance_km |   p90_distance_km |   exposure_per_trip |   risk_score_0_100 |
|:----------------------------|-------------:|-----------------:|------------------:|------------------:|--------------------:|-------------------:|
| Vadodara → Cuttack          |            2 |      3.1152e+07  |          1328.62  |          1328.62  |         1.5576e+07  |           100      |
| Vadodara → South West Delhi |            4 |      6.31215e+07 |           795.758 |           795.758 |         1.57804e+07 |            93.1383 |
| Vadodara → Visakhapatnam    |            5 |      6.78568e+07 |          1172.27  |          1172.27  |         1.35714e+07 |            83.2727 |
| Vadodara → Medak            |            1 |      1.27269e+07 |           713.627 |           713.627 |         1.27269e+07 |            70.5289 |
| Vadodara → Nalgonda         |           13 |      1.56975e+08 |           862.69  |           862.69  |         1.2075e+07  |            68.457  |
| Vadodara → Raigarh(MH)      |            3 |      4.01926e+07 |           363.095 |           363.095 |         1.33975e+07 |            65.7262 |
| Vadodara → Belgaum          |            2 |      2.37534e+07 |           729.248 |           729.248 |         1.18767e+07 |            64.9964 |
| Vadodara → East Godavari    |            4 |      4.1106e+07  |          1069.05  |          1069.05  |         1.02765e+07 |            58.121  |
| Vadodara → Dharwad          |            2 |      2.12872e+07 |           796.733 |           796.733 |         1.06436e+07 |            57.5344 |
| Vadodara → Bangalore        |           10 |      8.78474e+07 |          1135.99  |          1135.99  |         8.78474e+06 |            47.874  |

**What underwriters should do**
- Apply **route-tier rules**: higher deductible / stricter packing & escort rules on top-risk routes.
- Use **route pre-approval** for extreme-distance or extreme-exposure legs.
- Push **route survey / verification** for repeated high-exposure corridors.

---

## 4. Vehicle Concentration Risk

**Why single-vehicle dominance is dangerous**
When one vehicle (or a small set) carries disproportionate exposure, you create a **single-point-of-failure**. The operational system becomes brittle: breakdowns, detentions, driver churn, or route deviation spikes the insurer’s tail risk.

**Evidence from data**
- Vehicle concentration headline: Top 10 vehicles hold 27.28% of exposure (Top 1: 7.48%).

**Operational actions**
- Cap exposure per vehicle (per-day / per-trip).
- Require **secondary vehicle readiness** for routes where Top-1 share is extreme.
- Telemetry + photo-verification triggers for high-exposure vehicles.

---

## 5. Carrier Risk Profile

### Top 10 carriers by exposure
| carrier_norm                           |   trips |   total_exposure |   avg_exposure |   unique_routes |
|:---------------------------------------|--------:|-----------------:|---------------:|----------------:|
| SHYAMSUNDER BHIMSAIN GOYAL             |      68 |      6.00887e+08 |    8.83657e+06 |              18 |
| YATAYAT CORPORATION OF INDIA           |      20 |      1.45967e+08 |    7.29833e+06 |              14 |
| INLAND WORLD LOGISTICS PRIVATE LIMITED |      11 |      9.90046e+07 |    9.00042e+06 |               7 |
| RAVINDER SINGH                         |       8 |      7.07825e+07 |    8.84782e+06 |               5 |
| PREMIER ROAD CARRIERS LIMITED          |       3 |      3.22228e+07 |    1.0741e+07  |               1 |
| SURAT GOODS TRANSPORT PVT LTD          |       2 |      2.62845e+07 |    1.31422e+07 |               1 |
| NAVEEN S DADHICH                       |       6 |      2.18987e+07 |    3.64979e+06 |               4 |
| EITA INDIA LIMITED                     |       2 |      2.12872e+07 |    1.06436e+07 |               1 |
| ADHUNIK TRANSPORT ORGANISATION LIMITED |       2 |      1.22012e+07 |    6.1006e+06  |               1 |
| Surat Goods transport                  |       1 |      8.7615e+06  |    8.7615e+06  |               1 |

**Carrier × Route hotspots**
Use the carrier-route concentration summary to identify where underwriting terms should be carrier-specific.

| carrier_norm                           | route                       |   pair_trips |   pair_total_exposure |   pair_unique_vehicles |
|:---------------------------------------|:----------------------------|-------------:|----------------------:|-----------------------:|
| SHYAMSUNDER BHIMSAIN GOYAL             | Vadodara → Nalgonda         |           13 |           1.56975e+08 |                     11 |
| SHYAMSUNDER BHIMSAIN GOYAL             | Vadodara → Surat            |           16 |           1.1522e+08  |                     14 |
| SHYAMSUNDER BHIMSAIN GOYAL             | Vadodara → Visakhapatnam    |            5 |           6.78568e+07 |                      4 |
| SHYAMSUNDER BHIMSAIN GOYAL             | Vadodara → Bangalore        |            6 |           5.21963e+07 |                      6 |
| SHYAMSUNDER BHIMSAIN GOYAL             | Vadodara → East Godavari    |            4 |           4.1106e+07  |                      3 |
| INLAND WORLD LOGISTICS PRIVATE LIMITED | Vadodara → Jaipur           |            2 |           3.58793e+07 |                      2 |
| YATAYAT CORPORATION OF INDIA           | Vadodara → South West Delhi |            2 |           3.34233e+07 |                      2 |
| PREMIER ROAD CARRIERS LIMITED          | Vadodara → Bangalore        |            3 |           3.22228e+07 |                      3 |
| SHYAMSUNDER BHIMSAIN GOYAL             | Vadodara → Cuttack          |            2 |           3.1152e+07  |                      2 |
| RAVINDER SINGH                         | Vadodara → Raigarh(MH)      |            2 |           3.0529e+07  |                      2 |

**What to demand from each carrier tier**
- **Tier RED (highest exposure / hotspots):** route compliance evidence, vehicle fitness proof, stricter SLAs, higher deductibles.
- **Tier YELLOW:** periodic route audit, standard telemetry/photo checks.
- **Tier GREEN:** keep as preferred list, reward with smoother terms.

---

## 6. Consignee Risk Profile

### Top 10 consignees by exposure
| consignee_norm                           |   trips |   total_exposure |   unique_carriers |
|:-----------------------------------------|--------:|-----------------:|------------------:|
| DIVI S LABORATORIES LIMITED              |      10 |      1.2655e+08  |                 1 |
| KARTIK REFRIGERATION PRIVATE LIMITED     |      17 |      1.22376e+08 |                 2 |
| VOLTAS LIMITED                           |      14 |      9.54345e+07 |                 4 |
| BANGALORE METRO RAIL CORPORATION LIMITED |       9 |      8.44192e+07 |                 2 |
| DIVIS LABORATORIES LIMITED               |       6 |      6.5034e+07  |                 1 |
| KMV PROJECTS LIMITED                     |       4 |      5.62034e+07 |                 3 |
| SRF LIMITED                              |       3 |      3.5046e+07  |                 2 |
| DELHI INTERNATIONAL AIRPORT LIMITED      |       2 |      3.34233e+07 |                 1 |
| BLUE JET HEALTHCARE LIMITED              |       2 |      3.0529e+07  |                 1 |
| CEMINDIA PROJECTS LIMITED                |       2 |      2.96982e+07 |                 1 |

**Consignee × Carrier clusters**
Use the hotspot plot/CSV to prioritize joint interventions (who ships with whom at scale).

- CSV: `L2_consignee_carrier_hotspots__20260320_182304.csv`
- Figures (if present): `L2_consignee_x_carrier_hotspot__20260320_182304.png`

**Why consignees should co-fund risk reduction**
Consignees are the stable node in the system. Carriers and drivers churn; consignees don’t. Funding telemetry, secure yards, unloading discipline, and route compliance is cheaper than absorbing disruption.

---

## 7. What This Enables

- **Pricing leverage:** rate adjustments based on exposure concentration (not gut feel).
- **Deductible rationalisation:** higher deductibles where operational stress concentrates.
- **Route exclusions:** defendable route carve-outs when exposure/risk spine is extreme.
- **Embedded insurance logic:** integrate operational proofs (route/vehicle controls) with underwriting terms.

---

## 8. What This Does NOT Claim

- This is **not** a claims predictor.
- This is **not** a loss probability model (yet).
- That honesty makes this defensible: it’s a **risk concentration + operational stress intelligence layer** that underwriters can audit and act on.

---

## Appendix — Key artifacts generated

- Route scorecard CSV: `L1_route_scorecard__20260320_182304.csv`
- Route spine CSV: `L1_route_spine__20260320_182304.csv`
- Vehicle concentration CSV: `L1_vehicle_concentration__20260320_182304.csv`
- Carrier exposure CSV: `L2_carrier_exposure__20260320_182304.csv`
- Consignee exposure CSV: `L2_consignee_exposure__20260320_182304.csv`
