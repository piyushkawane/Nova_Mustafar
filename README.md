# Nova_Mustafar

**STAC WARS PS1: OpenRocket Extraterrestrial Flight Design Challenge**
*Operation Ember Ascent: launch from Vader's world of fire*

Team: **Nova** | Software: **OpenRocket 24.12**

A two-stage sounding rocket designed in OpenRocket for a scientific flight on the fictional planet Mustafar (700 K, 75 kPa, 10 m/s wind). The rocket carries a 1.00 kg payload to an apogee of about 4 km and recovers both stages under parachute.

---

## Repository contents

| File | Description |
|---|---|
| `Nova_Rocket.ork` | Final OpenRocket file: full geometry, materials, payload, motors, recovery system and all flight simulations |
| `Nova_FlightData.csv` | Flight data exported from the `Mustafar_Final` simulation (altitude, velocities, accelerations, CG, CP, stability, wind, temperature, pressure, density, Mach number) |
| `Nova_Report.pdf` | Short report: design approach, Mustafar launch conditions, recovery system, Earth vs Mustafar comparison, and conclusions |

The `.ork` file is self-contained and fully editable, with no externally referenced files.

---

## Mission requirements and results

| Requirement | Target | Result |
|---|---|---|
| Apogee | 4000 ± 100 m (3900-4100 m) | **4020 m** |
| Payload mass | 1.00 ± 0.05 kg | **1.00 kg** (1000 g mass component, no overrides) |
| Rocket length | ≤ 220 cm | **144 cm** |
| Total motor impulse | ≤ 2800 N·s | **about 959 N·s** (combined) |
| Body material | Cardboard (≤ 10 kg total) | **Cardboard, 2926 g with motors** |
| Parachute recovery | Mandatory | **Both stages recovered by parachute** |
| Descent velocity | 4-8 m/s | **6.86 m/s (sustainer), 5.62 m/s (booster)** |
| Deployment | At apogee | **Sustainer chute at apogee**; booster chute at the booster's own apogee |

---

## Final design

- **Configuration:** two stages (sustainer + booster), 5 cm maximum diameter
- **Sustainer motor:** AeroTech I285R, ejection delay plugged
- **Booster motor:** AeroTech I366R-4 (4 s delay, which separates the stages shortly after burnout)
- **Payload:** 1.00 kg mass component carried in the sustainer and recovered with it
- **Ballast:** 333 g mass component added to tune apogee
- **Recovery:** one parachute per stage, both with a drag coefficient of 0.8
- **Stability:** 3.0 cal for the full stack in the design view, 4.31 cal in flight at t = 2 s, and 5.14 cal for the sustainer alone. The brief sets no stability requirement, so these are reported as simulated values.
- **Max velocity:** 301 m/s (Mach 0.54)

---

## Mustafar launch conditions (OpenRocket simulation settings)

| Parameter | Value |
|---|---|
| Temperature | 426.85 °C (700 K) |
| Pressure | 750 mbar (75 kPa) |
| Air density | about 0.373 kg/m³ (derived by OpenRocket from pressure and temperature) |
| Wind | 10 m/s average, direction 270° |
| Turbulence | 2%, standard deviation 0.5 m/s |
| Launch site altitude | 0 m |
| Launch rod | 250 cm, vertical launch |

International Standard Atmosphere is switched **off** for the Mustafar run.

> **Limitation:** OpenRocket 24.12 does not offer a gravity setting that we could find. All simulations use its built-in gravity (about 9.78-9.79 m/s²), not Mustafar's 6.5 m/s². The effect of lower gravity is discussed in the report as an untested prediction.

---

## Simulations in the `.ork` file

All five simulations use the same final rocket. Only the environment changes, one parameter at a time.

| Simulation | Atmosphere | Wind | Apogee | Max velocity | Sustainer descent | Sustainer drift |
|---|---|---|---|---|---|---|
| `Mustafar_Final` | 700 K, 75 kPa | 10 m/s | 4020 m | 301 m/s | 6.86 m/s | 4943 m |
| `Earth_Baseline` | ISA (15 °C, 101.3 kPa) | 10 m/s | 2613 m | 265 m/s | 3.81 m/s | 5678 m |
| `Temp_Only` | 700 K, 101.3 kPa | 10 m/s | 3625 m | 294 m/s | 5.90 m/s | 5283 m |
| `Pressure_Only` | 15 °C, 75 kPa | 10 m/s | 2975 m | 277 m/s | 4.43 m/s | 5336 m |
| `Wind_Only` (no wind) | 700 K, 75 kPa | 0 m/s | 4136 m | 302 m/s | 6.87 m/s | 12 m |

Descent rates are the mean vertical speed over the last 60 s of descent. `Mustafar_Final` is the submitted design. `Wind_Only` and the three Earth-based runs are comparison runs used for the report.

### Key findings

- Thinner, hotter air raises apogee by about 1400 m compared with Earth (2613 m to 4020 m). Temperature accounts for most of it (+1012 m); pressure adds +362 m.
- Parachute descent is faster in thin air: 3.81 m/s on Earth against 6.86 m/s on Mustafar, consistent with descent speed scaling as 1/√density.
- The 10 m/s wind lowers apogee by about 116 m (4136 m without wind) and causes thousands of metres of downrange drift.
- The OpenRocket warning "recovery device deployment at high speed" on the sustainer parachute (30.8 m/s) comes from sideways motion in the wind at apogee. With no wind the same event is at 0.64 m/s.

---

## How to open and reproduce

1. Install [OpenRocket](https://openrocket.info/) 24.12 or later.
2. Open `Nova_Rocket.ork`.
3. Go to the **Flight simulations** tab, select the simulations, and click **Run simulations**.
4. To inspect the launch conditions, select a simulation and click **Edit simulation** (Launch conditions tab).
5. To re-export flight data, use **Plot / Export**, then the Export data tab.

Results may vary by a few metres between runs because of the wind turbulence model.

---

## Report

`Nova_Report.pdf` explains the design approach and thought process, the Mustafar launch conditions, the recovery system, and the Earth-versus-Mustafar comparison. It gives a prediction and result for each environmental change (gravity, pressure, temperature, air density and wind) and finishes with a conclusion on whether each prediction held.
