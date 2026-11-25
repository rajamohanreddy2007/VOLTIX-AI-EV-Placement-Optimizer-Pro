# Electric Vehicle Charging Station Placement Optimizer
**Problem Statement No. 78 | Version 1.0 | Student Project Implementation**

An interactive facility-location planning application and web platform that identifies charging coverage gaps and optimizes candidate site locations for electric vehicle infrastructure across municipal zones using traffic density, population, capacity, and budgetary constraints.

---

## 🌟 Key Highlights & Implementation Plans

The application supports multiple flexible delivery paces: a **6-Day Balanced Plan** (recommended for student project submissions), an accelerated **5-Day Sprint**, and the original **10-Day Granular Breakdown**.

### 📅 Recommended 6-Day Balanced Plan

| Day | Milestone Focus | Functions Implemented | Done When Criteria |
|:---:|---|---|---|
| **Day 1** | **Data Ingestion & Municipal Zones** | `collect_data()` + `create_zones()` | CSV parsed; negative values rejected; unique zones created and totals aggregated. |
| **Day 2** | **Demand Estimation & Normalization** | `calculate_demand()` | Traffic & population normalized; composite demand weights $W_i = 0.6 \cdot T_i + 0.4 \cdot P_i$ computed. |
| **Day 3** | **Baseline Coverage & Gap Prioritization** | `check_coverage()` + `find_coverage_gaps()` | Baseline coverage evaluated (38.70%); uncovered points sorted descending by demand weight. |
| **Day 4** | **Candidate Scoring & Redundancy Penalty** | `calculate_score()` | Candidates scored by new demand covered minus overlap penalty ($\gamma = 0.25$). |
| **Day 5** | **Greedy Optimization & Post-Coverage Analysis** | `optimize_locations()` + `calculate_coverage()` | Best stations selected iteratively under budget; final coverage (100%) and delta (+61.3%) calculated. |
| **Day 6** | **Final Reporting & PRD Validation Suite** | `display_results()` + `runValidationTests()` | Comprehensive report generated; all 7 PRD Section 11 test cases pass. |

---

### ⚡ Accelerated 5-Day Sprint Plan

| Day | Sprint Milestone | Functions Grouped | Daily Objective |
|:---:|---|---|---|
| **Day 1** | **Ingestion & Spatial Representation** | `collect_data()` + `create_zones()` | Data validation, CSV reader, and municipal zone mapping. |
| **Day 2** | **Demand Modeling & Baseline Coverage** | `calculate_demand()` + `check_coverage()` | Normalization, composite demand weights, and baseline radius check. |
| **Day 3** | **Gap Prioritization & Candidate Scoring** | `find_coverage_gaps()` + `calculate_score()` | Uncovered clusters prioritization and overlap redundancy penalty scoring. |
| **Day 4** | **Greedy Optimization & Metrics** | `optimize_locations()` + `calculate_coverage()` | Greedy budget allocation and post-optimization coverage improvement. |
| **Day 5** | **Reporting & Full PRD Test Suite** | `display_results()` + `runValidationTests()` | Analytical results report and verification of all 7 PRD edge-case test cases. |

---

### 🔍 10-Day Granular Breakdown (1 Function / Day)

| Day | Function | Purpose & PRD Requirement |
|:---:|---|---|
| Day 1 | `collect_data()` | Ingests traffic, population, stations, candidates, radius, capacity, limit from CSV. |
| Day 2 | `create_zones()` | Groups demand points into municipal `Zone` objects and aggregates totals. |
| Day 3 | `calculate_demand()` | Normalizes traffic and population to $[0, 1]$; computes demand weights. |
| Day 4 | `check_coverage()` | Distance check against existing stations. Marks points covered if $\text{dist} \le \text{radius}$. |
| Day 5 | `find_coverage_gaps()` | Filters uncovered points and sorts them descending by demand weight. |
| Day 6 | `calculate_score()` | Evaluates candidate net benefit: $\text{Score} = \text{NewDemand} - \gamma \cdot \text{RedundantDemand}$. |
| Day 7 | `optimize_locations()` | Greedy optimization loop selecting top-scoring candidates under budget. |
| Day 8 | `calculate_coverage()` | Computes total demand, final covered demand, final coverage %, and improvement $\Delta\%$. |
| Day 9 | `display_results()` | Generates structured analytical reports with recommendations and remaining gaps. |
| Day 10 | `run_tests()` & Integration | Connects all functions end-to-end and runs the 7 PRD Section 11 test cases. |

---

## 🚀 Running the Web Application

The interactive web dashboard is powered by FastAPI and modern HTML5/Canvas/CSS3.

### 1. Launch Web Server
```powershell
cd C:\Users\rajam\.gemini\antigravity\scratch\ev-charging-optimizer\backend
python -m uvicorn app:app --host 127.0.0.1 --port 8000 --reload
```

### 2. Open in Browser
Visit:
```
http://127.0.0.1:8000/
```

### Features of the Web Application:
- **Day-by-Day Interactive Workshop**: Step through Day 1 to Day 10 with live inputs, execution buttons, state inspection, mathematical formula breakdowns, and Java/Python code views.
- **City-Wide Placement Optimizer Map**: Interactive 2D Canvas rendering coordinate grids, municipal zones, existing station circles (solid blue), candidate circles (dashed purple/amber), demand points colored by coverage status (red gaps vs green covered), and dynamic hover tooltips.
- **Optimization Sliders**: Tweak coverage radius (km), station limit, budget, traffic weight $\alpha$, population weight $\beta$, and redundancy penalty $\gamma$ on the fly with instant recomputation.
- **PRD Section 11 Test Suite Runner**: 1-click execution of all 7 edge-case test scenarios with live assertion logs and terminal view.
- **Code & Artifacts Hub**: View, copy, and export `Station.java`, `DemandPoint.java`, `Zone.java`, `CandidateLocation.java`, `Optimizer.java`, `EVChargingOptimizerApp.java`, and `sample-city.csv`.

---

## ☕ Running the Java Console Application

The Java implementation adheres strictly to Section 7 (Object-Oriented Design) and Section 14 (Folder Structure) of the PRD.

### Compile and Run:
```powershell
cd C:\Users\rajam\.gemini\antigravity\scratch\ev-charging-optimizer
javac -d . src\DemandPoint.java src\Station.java src\Zone.java src\CandidateLocation.java src\Optimizer.java src\EVChargingOptimizerApp.java
java -ea src.EVChargingOptimizerApp
```

### Verification Output:
```text
================================================================
 Electric Vehicle Charging Station Placement Optimizer (PS #78) 
================================================================

[Day 1] Reading and validating data from: data\sample-city.csv
        Loaded: 2 stations, 14 demand points, 6 candidates.
[Day 2] Creating geographic zones...
        Created 7 unique zones.
[Day 3] Normalizing traffic/population and calculating demand weights...
        Total city demand weight: 8.823
[Day 4] Checking coverage from existing stations (Radius = 5.0 km)...
        Initial covered demand: 3.414 (38.70%)
[Day 5] Identifying prioritized coverage gaps...
        Found 8 uncovered demand points.
[Day 6 & 7] Running greedy candidate selection optimizer...
        Selected 3 optimal stations.
[Day 8] Calculating post-optimization coverage metrics...
        Final coverage: 100.00% (+61.30% improvement)

[Day 9] Final Results Report:
--- COVERAGE METRICS ---
Total Demand Weight           : 8.823
Initial Covered Demand Weight : 3.414 (38.70%)
Final Covered Demand Weight   : 8.823 (100.00%)
Coverage Improvement          : +61.30%
Uncovered Demand Remaining    : 0.000

--- RECOMMENDED STATIONS (Selected Candidates) ---
[1] Tech Park Gateway (C2) at (15.8, 4.5) | Score: 2.229 | Cost: 32.0 Lakhs
[2] Central Junction Hub (C1) at (12.5, 8.8) | Score: 2.076 | Cost: 28.5 Lakhs
[3] University Campus Gate (C3) at (4.8, 12.0) | Score: 0.932 | Cost: 22.0 Lakhs

[Day 10] Running PRD Section 11 Test Cases...
[PASS] TC 1: All demand points covered -> No redundant sites recommended
[PASS] TC 2: No existing stations -> Initial coverage begins at 0.0%
[PASS] TC 3: Candidate covering no demand receives 0 score
[PASS] TC 4: Station limit 0 -> No new sites selected
[PASS] TC 5: Total demand zero -> Handled safely without division by zero
[PASS] TC 6: Invalid negative traffic/population correctly rejected
[PASS] TC 7: Overlapping candidates -> Second candidate experiences diminishing returns
```

---

## 📁 Project Folder Structure

```
ev-charging-optimizer/
├── src/
│   ├── DemandPoint.java             # Demand point entity with traffic/population/coverage
│   ├── Station.java                 # Existing station entity with distance & radius check
│   ├── Zone.java                    # Municipal zone grouping & demand aggregator
│   ├── CandidateLocation.java       # Prospective charging station with score evaluation
│   ├── Optimizer.java               # Core optimization engine implementing Day 1 - Day 9
│   └── EVChargingOptimizerApp.java  # Main driver & Day 10 test suite runner
├── backend/
│   ├── app.py                       # FastAPI REST API serving all endpoints & static UI
│   └── optimizer_engine.py          # Python OOP engine mirroring Java 1:1
├── static/
│   ├── index.html                   # Modern single-page web application
│   ├── style.css                    # Professional dark theme UI styling
│   └── app.js                       # Interactive simulation, Canvas renderers, and stepper
├── data/
│   └── sample-city.csv              # PRD sample city dataset (Pedda Mavalli & Gandhi Nagar)
├── tests/
│   └── test-cases.md                # Complete test cases documentation & PRD compliance matrix
└── README.md                        # Project documentation
```
