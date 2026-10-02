# Hybrid CSP + PVT Plant for Santiago: Recap

**Assignment 1, Q5 (with the inputs for Q6 and Q7).** Renewable Energy Conversion, Energy Transition Perspectives minor.

---

## 1. Bottom line

The cheapest plant that covers Santiago's daytime heat and electricity demand on both design days is:

| | Units | Collector area | Investment |
|---|---|---|---|
| **Heliostats (CSP)** | **215** | 47,300 m² | €3.78 M |
| **PVT panels** | **9,559** | 38,236 m² | €5.74 M |
| **Total** | | **85,536 m²** (19% of the 450,000 m² site) | **€9.52 M** |

- **The winter day (23 June) sets the size of the plant.**
  - Its heat demand sets the number of PVT panels.
  - Its electricity demand sets the number of heliostats.
- **The 60% CSP rule is met without extra effort:** CSP supplies 62.8% of the electricity.
- **The plant does not cover demand around the clock.** Nights, mornings and the evening electricity peak are short of energy. Storage and extra capacity are the main improvements (see Q8).

---

## 2. Method

1. **Efficiency of each technology.**
   - The CSP chain is: mirror field (optical efficiency 0.649) × receiver (0.80) × Rankine cycle (0.42). So 21.8% of the sunlight on the mirrors becomes electricity.
   - The PVT panels convert 16% of sunlight into electricity.
   - The PVT heat output follows the flat-plate collector formula in its heat-removal-factor form (Lecture 2): $\dot{Q}_u = F_R A_c [(\tau\alpha) I_T - U (T_{in} - T_a)]$. Heat loss is evaluated at the 35 °C inlet temperature and corrected by $F_R$ = 0.65.
2. **Hourly output.** These efficiencies are applied to the measured hourly irradiance and temperature for two days, 23 June (winter) and 16 December (summer). The result is the output of one m² of mirror and one m² of panel in every hour.
3. **Optimisation.** We choose the number of heliostats and PVT panels that minimise investment cost subject to four rules, applied on each day:
   - **C1:** heat supplied ≥ heat demanded, over the sunlit hours;
   - **C2:** electricity supplied ≥ electricity demanded, over the sunlit hours;
   - **C3:** CSP supplies ≥ 60% of the electricity;
   - **C4:** total collector area ≤ 450,000 m².

   With only two decisions, every integer combination was checked, so the result is the true optimum. The full formulation is in `2_Math_Model`.
4. **Hour-by-hour check.** We then compare the optimum against demand hour by hour on both days (Q6), and re-run it with mirrors degraded from 95% to 85% reflectivity (Q7).

---

## 3. Results

### Energy delivered over the sunlit hours

| | June (winter, 14 sun hours) | December (summer, 16 sun hours) |
|---|---|---|
| Electricity supplied / demanded | 361 / 361 GJ | 524 / 478 GJ |
| of which CSP / PVT | 227 / 134 GJ | 329 / 195 GJ |
| CSP share of electricity | 62.8% | 62.8% |
| Heat supplied / demanded | 184 / 184 GJ | 510 / 137 GJ |

### Which rules decide the design

| Rule | Status | Consequence |
|---|---|---|
| C1 Heat (June) | **binding** | Sets the PVT count. Winter heat losses are high, so each panel delivers little heat. |
| C2 Electricity (June) | **binding** | Sets the heliostat count. Mirrors cover the electricity the PVT panels do not. |
| C3 CSP share ≥ 60% | slack | 62.8% |
| C4 Area | slack | 19% of the site used |

### Hour by hour (whole day)

| | June | December |
|---|---|---|
| Electricity surplus at midday | +148 GJ | +214 GJ |
| Electricity shortfall (night, morning, evening peak) | −226 GJ | −232 GJ |
| Heat surplus at midday | +76 GJ | +391 GJ |
| Heat shortfall (night, morning, evening) | −130 GJ | −34 GJ |

- **Electricity:** on both days the shortfall is larger than the midday surplus. Storage alone cannot close the gap; the plant also needs more capacity, sized for the 24-hour total.
- **Heat:** in December, thermal storage of the midday surplus would cover the whole day. In June the shortfall is larger than the surplus, so winter needs extra heat capacity as well.
- **The 19:00 electricity peak** falls after sunset on both days. It can only be met from storage.

### PVT collector performance (per 4 m² panel)

| | June | December |
|---|---|---|
| Peak usable heat | 1,024 W at 14:00 (256 W/m², efficiency 34.1%) | 1,978 W at 12:00 (494 W/m², efficiency 48.3%) |
| Usable heat over the day | 19.2 MJ (5.34 kWh) | 53.4 MJ (14.82 kWh) |
| Average over the sunlit hours | 381 W | 926 W |
| Daily thermal efficiency | 21.9% | 41.8% |
| Maximum outlet water temperature | 36.2 °C | 37.4 °C |

- **Winter performance is much weaker:** 31% less sunlight, but 64% less heat, because the cold air (4–15 °C) raises the heat losses.
- **The PVT water warms by only 1–2 K.** The high flow rate (0.2 kg/s per panel) carries heat away quickly, so it is low-temperature heat.

### Mirror degradation (Q7: reflectivity 95% → 85%)

| | June | December |
|---|---|---|
| Electricity over the sunlit hours | 361 → **337 GJ (below the 361 demand)** | 524 → 490 GJ (still above the 478 demand) |
| CSP share | 62.8% → 60.1% (still compliant) | 62.8% → 60.1% |
| Heat | unchanged | unchanged |

Degraded mirrors make the plant **fall short of winter electricity demand by about 7%**. Covering it at 85% reflectivity needs about **241 heliostats** (+26, roughly +€0.46 M), or a mirror cleaning schedule.

---

## 4. Assumptions and limitations

| Assumption | Why |
|---|---|
| Demand is covered **in total over the sunlit hours of each day**, not in every single hour | Hourly coverage is physically impossible: the PVT gives no heat at dawn and dusk, and the 19:00 peak would need more than the whole site. |
| PVT heat uses the lecture's **heat-removal-factor formula; radiation is not modelled separately** | The plate temperature needed for the full balance (with emissivity) is not given. The $F_R$ form with the known inlet temperature is the calculable version for low-temperature collectors. |
| The data file's demand is used, not the brief's 4,300 TJ/year | The data file totals about 250 TJ/year. The questions refer to "the data provided". |
| The 450,000 m² limit applies to **collector area** (mirrors + panels) | Real heliostat fields need 3–5× more land than mirror area. |
| **Rankine condenser heat is not counted** towards heat demand | Confirmed with the TA: heat demand is supplied by the PVT panels only. |
| Efficiencies are constant: average cosine efficiency, fixed 42% cycle efficiency | As given in the brief. |
| The water's specific heat is 4,186 J/(kg·K) | Standard value. It is only used for the outlet temperature. |

---

## 5. Open points

1. **TA confirmation:** is the energy-basis coverage the intended reading?
2. **Q8 recommendations** (from the results above):
   - thermal storage and batteries to move the midday surplus to the evening and night;
   - extra capacity, because daily electricity (both days) and winter heat exceed what the daytime plant delivers;
   - a heliostat margin, or a cleaning schedule, against mirror degradation.

---

## 6. Folder contents

| Folder | Contents |
|---|---|
| `2_Math_Model` | Complete mathematical formulation (PDF and LaTeX source) |
| `3_Code` | `plant_sizing.py`. Run it to reproduce every number, figure and the results workbook. |
| `4_Visualizations` | Q5 design-space cost map · Q6 hourly supply vs demand · Q7 mirror degradation |
| `5_Data` | `Input_Data_Assignment_1.xlsx` (given data) · `Results_Plant_Sizing.xlsx` (all results, hour by hour, as live formulas) |
