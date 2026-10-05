# Dataset: `ToleranceTest_MasterDoc.xlsx`

Field data on how African lions (*Panthera leo*) responded to experimental drone approaches, together with group counts made from the ground and from the drone. The data were collected at Ol Pejeta Conservancy (OPC), Laikipia County, Kenya, between November and December 2024.

This file is the raw input for all analyses in this repository (exploratory analysis, drone-disturbance models and count-assessment models). For the full study design, see the Methods section of the associated manuscript.

---

## Study overview

| | |
|---|---|
| **Location** | Ol Pejeta Conservancy, Laikipia County, central Kenya (0°00ʹ N, 36°54ʹ E) |
| **Period** | 7 November – 2 December 2024 (14 field days in this file) |
| **Daily window** | 08:20 – 18:25 local time |
| **Subjects** | Lion groups from 5 prides: Ajali, Bima, Sela, Utali, Wanjiku |
| **Trials** | 69 straight-line drone approach flights (one row per flight) |
| **Drone** | DJI Mavic 3 Enterprise T (RGB + thermal cameras) |
| **Altitude treatments** | 20, 40, 60, 80, 100 and 120 m above ground level (AGL), randomised in order |

In each trial the drone took off from the open-roof research vehicle and climbed vertically to the target altitude. It then flew in a straight line toward the lion group at constant altitude and hovered over the group for at least 5 minutes. Lion behaviour was scored for the 5 minutes before the flight and during the flight. Group size and age/sex composition were recorded with four methods (see [Count methods](#count-methods)). Each encounter with a group included up to three trials, 15–62 minutes apart.

### Trials per pride and altitude

| Pride | 20 m | 40 m | 60 m | 80 m | 100 m | 120 m | Total |
|---|---|---|---|---|---|---|---|
| Ajali | 3 | 4 | 7 | 1 | 6 | 2 | 23 |
| Bima | 1 | 1 | 1 | 0 | 0 | 0 | 3 |
| Sela | 3 | 4 | 3 | 2 | 3 | 2 | 17 |
| Utali | 2 | 1 | 2 | 5 | 0 | 3 | 13 |
| Wanjiku | 1 | 3 | 1 | 3 | 2 | 3 | 13 |
| **Total** | 10 | 13 | 14 | 11 | 11 | 10 | **69** |

---

## File structure

The workbook has two sheets:

| Sheet | Content |
|---|---|
| `Tolerance test` | Main dataset: 69 rows (one per drone trial) × 56 columns |
| `Flight logs` | Column headers only (`Test_ID`, `Date`, `Distance`, `Duration`); contains no data |

### Coding conventions

- Binary variables use `Y` (yes / present / observed) and `N` (no / absent / not observed).
- The column prefixes `BF_` and `AF_` mean **Before Flight** and **After Flight start** (that is, during the drone flight).
- Count columns hold the number of individuals: `F` = adult females, `M` = adult males, `c` = cubs, `Individual` = all individuals.
- Empty cells are missing values.

---

## Variable descriptions — sheet `Tolerance test`

### Trial identification and context

| Column | Type | Units / levels | Description |
|---|---|---|---|
| `Test_ID` | string | e.g. `AJ01` | Unique trial ID. The two-letter prefix is the pride (AJ = Ajali, BI = Bima, SE = Sela, UT = Utali, WA = Wanjiku) and the number is the trial number within that pride. |
| `Date` | date | YYYY-MM-DD | Date of the trial. |
| `Species` | string | `Lion` | Target species (constant). |
| `Altitude` | integer | m AGL; 20, 40, 60, 80, 100, 120 | Altitude treatment of the approach flight. |
| `Time` | time | HH:MM, local time (EAT, UTC+3) | Start time of the trial. |
| `prides` | string | Ajali, Bima, Sela, Utali, Wanjiku | Pride identity (*pride ID*). |
| `Pride_with_cubs` | Y/N | | Whether the pride was known to have dependent cubs at the time of the trial (from recent OPC monitoring records) |
| `vegetation` | string | Acacia drepanolobium, Euclea divinorum, Grassland, Mixed bushland | Dominant vegetation type at the trial site, classified before the flight. |
| `Temperature` | integer | °C | Ambient temperature recorded before the flight. |
| `Wind` | Y/N | | Wind present during the trial. |
| `Kill` | Y/N | | Fresh kill present at the site. |
| `Disturbance` | Y/N | | Any environmental disturbance (e.g. approaching vehicles, aircraft) before or during the trial. |
| `BF_Distance` | integer or string | m | Distance from the field vehicle (the drone take-off point) to the lions before the flight, measured with a laser rangefinder. Where lions were spread out, the value is a range from the nearest to the furthest lion (e.g. `15-30`). |
| `BF_Distance_averaged` | integer | m | `BF_Distance` as a single number: the midpoint of the range where a range was recorded, otherwise the same value. Used as the *take-off distance* variable. |

### Behaviour (one-zero sampling)

Behaviour was scored with one-zero sampling (Altmann 1974). For each period, a category is `Y` if **any** lion in the group showed it, regardless of how many individuals did. The categories follow the felid ethogram of Stanton et al. (2015). The same 13 categories are recorded for the pre-flight period (`BF_`, 5 minutes of observation before take-off) and the flight period (`AF_`, from take-off to the end of the trial):

| Suffix | Behavioural category |
|---|---|
| `_Agonistic` | Agonistic behaviour |
| `_Aggressive/Flee` | Aggressive or flight behaviour |
| `_Fear` | Fear / alert behaviour |
| `_Stereotypic` | Stereotypic behaviour |
| `_Vocalization` | Vocalisation |
| `_Active/Exploratory` | Active / exploratory behaviour (e.g. looking at or investigating the drone) |
| `_Marking` | Scent marking |
| `_Maintenance` | Maintenance (e.g. grooming) |
| `_Feeding` | Feeding |
| `_Affiliative_Reproductive` | Affiliative or reproductive (mating) behaviour |
| `_Loc` | Locomotion |
| `_Calm` | Calm |
| `_Inactive` | Inactive (resting, lying) |

For analysis, these categories are collapsed into five behavioural classes (manuscript Table 2; Appendix S1, Section S2): **Flee/Fear**, **Exploratory**, **Feeding/Affiliative/Mating**, **Locomotion** and **Calm/Inactive**.

### Count methods

Group size and age/sex composition were recorded with four methods, in this order:

| Count method | Column prefix | Description |
|---|---|---|
| Close ground count | `N_*_close` | Count by sight from the vehicle at < 10 m from the group, before any drone activity. This is the standard OPC monitoring protocol. |
| Far ground count | `N_*_dronelaunch` | Count by sight (binoculars where needed) from the drone launch position, 20–120 m from the group. |
| Live drone count | `Drone_N_*` | Real-time count from the drone's RGB and thermal video feeds on the controller, made while the drone hovered over the group. |
| Video drone count | `DroneVIDEO_N_*` | Count made later from the recorded RGB and thermal drone footage, reviewed frame by frame. This is the reference (baseline) method in the count models. |

Each method has four columns:

| Column pattern | Description |
|---|---|
| `…_Individual…` | Total number of lions counted (all age/sex classes) |
| `…_F…` | Number of adult females |
| `…_M…` | Number of adult males |
| `…_c…` | Number of cubs |

Full column names:

- Close ground: `N_Individual_close`, `N_F_close`, `N_M_close`, `N_c_close`
- Far ground: `N_Individual_dronelaunch`, `N_F_dronelaunch`, `N_M_dronelaunch`, `N_c_dronelaunch`
- Live drone: `Drone_N_Individual`, `Drone_N_F`, `Drone_N_M`, `Drone_N_c`
- Video drone: `DroneVIDEO_N_Individual`, `DroneVIDEO_N_F`, `DroneVIDEO_N_M`, `DroneVIDEO_N_c`

A count of 0 means no lions of that class were detected with that method.

---

## Variables derived in the analysis code

Several model variables (manuscript Table 3) are not stored in the spreadsheet. They are computed in the notebooks:

| Derived variable | Derived from |
|---|---|
| *Before/After* | Reshaping the `BF_` and `AF_` behaviour columns into long format |
| *Behavioural class* (5 levels) | Collapsing the 13 behaviour categories (see above) |
| *Cluster ID* (encounter) | Trials on the same pride (`prides`) on the same `Date` |
| *Cubs presence* | Cub count columns (`N_c_*`, `Drone_N_c`, `DroneVIDEO_N_c`) |
| *Adult male presence* | Adult male count columns (`…_M…`) |
| *Time of day (1)*, categorical | `Time` |
| *Time of day (2)*, circular (sine/cosine) | `Time` |
| *Week of test* | `Date` |
| *Take-off distance* | `BF_Distance_averaged` |

---

## Usage

```python
import pandas as pd

df = pd.read_excel("ToleranceTest_MasterDoc.xlsx", sheet_name="Tolerance test")
```

See `Initial_Data_Exploration.ipynb` for the exploratory analysis. The modelling notebooks contain the Bayesian GLMMs (Bambi 0.15, ArviZ 0.22, Python 3.11.4).

---

## Permits and ethics

All drone operations were flown by a licensed pilot (A1/A2/A3 European licence or equivalent) with permission from the Kenya Civil Aviation Authority (KCAA). Research was conducted under permits from the Wildlife Research and Training Institute (WRTI, Research Permit No. WRTI-0431-06-24) and the National Commission for Science, Technology and Innovation (NACOSTI, License No. NACOSTI/P/24/41404). No lions were captured or collared for this study. Collared individuals were located using collars fitted for OPC's routine monitoring (Kamaru et al. 2024).

---

## Citation

If you use this dataset, please cite the associated manuscript:

> Iannino, E. et al. (in prep/under review). *Drone aerial monitoring improves demographic accuracy of lion groups with low behavioral impact*. 

## Contact

Elena Iannino — ianninoelena@gmail.com

## References

- Altmann, J. (1974). Observational study of behavior: sampling methods. *Behaviour*, 49, 227–267.
- Kamaru, D. N. et al. (2024). Disruption of an Ant-Plant Mutualism Shapes Interactions between Lions and Their Primary Prey. *Science* 383 (6681): 433–38.
- Stanton, L. A., Sullivan, M. S., & Fazio, J. M. (2015). A standardized ethogram for the Felidae: a tool for behavioral researchers. *Applied Animal Behaviour Science*, 173, 3–16.
