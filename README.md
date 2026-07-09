# Deutschlandticket Commute Potential — Norderstedt 🚇

A data science project that estimates how attractive public transport would be for employees commuting to **AB company, Robert-Koch-Straße 1, 22851 Norderstedt** — and how likely they would be to adopt the **Deutschlandticket**.

Because real employee addresses are sensitive, the analysis uses a fully **synthetic employee dataset** representing people living in Hamburg and surrounding areas.

---

## Project Structure

```
Deutschlandticket-Commute-Analysis/
├── deutschlandticket_analysis.ipynb   ← main notebook (start here)
├── requirements.txt                   ← Python dependencies
├── data/                              ← generated when you run the notebook
│   ├── synthetic_employees.csv
│   └── employees_scored.csv
└── outputs/                           ← generated when you run the notebook
    ├── commute_map.png
    ├── commute_time_distribution.png
    └── adoption_by_area.png
```

> `data/` and `outputs/` are empty on clone — the notebook fills them automatically when run.

---

## What the Notebook Does

| Step | Description |
|---|---|
| 1 | **Synthetic data generation** — 500 employees across Hamburg and the northern commuter belt, no real data used |
| 2 | **Public transport assessment** — offline HVV rail network model (U-Bahn, S-Bahn, AKN, Regional) with ~120 stations |
| 3 | **Door-to-door commute time** — walk / connecting bus + rail + transfers + last mile to the office |
| 4 | **Commute-time grouping** — ≤30 min / 31–45 min / 46–60 min / >60 min |
| 5 | **Deutschlandticket adoption scoring** — weighted utility model based on time, cost, convenience, and personal context |
| 6 | **Summary findings** + interactive Plotly map |

---

## Key Findings

- **~21%** of employees can reach the office within 30 minutes by public transport
- **~59%** within 60 minutes
- Expected Deutschlandticket adoption: **~43%** of the workforce (with 30% employer subsidy)
- **Best PT areas:** U1 corridor — Norderstedt, Garstedt, Langenhorn, Fuhlsbüttel
- **Weakest PT areas:** Wedel/Blankenese (west), Harburg (south), Billstedt/Bergedorf (east)
- **Biggest insight:** A company shuttle from Ochsenzoll or Norderstedt Mitte would improve adoption more than any ticket discount — the last mile is the biggest barrier

---

## How to Run

**1. Clone the repo**
```bash
git clone https://github.com/Sachinisand/Deutschlandticket-Commute-Analysis.git
cd Deutschlandticket-Commute-Analysis
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Open the notebook**
```bash
jupyter lab deutschlandticket_analysis.ipynb
```

**4. Run all cells**

`Kernel → Restart & Run All`

> The notebook also has an install cell at the top that installs missing packages automatically.

---

## Dependencies

| Package | Purpose |
|---|---|
| `numpy` | Numerical computation |
| `pandas` | Data manipulation |
| `networkx` | Rail network graph + Dijkstra routing |
| `matplotlib` | Charts and visualisations |
| `folium` | Map building |
| `plotly` | Interactive map (renders on GitHub without running) |
| `kaleido` | Saves map as image to outputs/ |
| `nbformat` | Notebook rendering support |

Install all at once:
```bash
pip install -r requirements.txt
```

---

## Why an Offline Network Model?

Journey-planner APIs (HVV GTI, Google Routes) require API keys and make the project non-reproducible. Instead, this project routes over a curated graph of ~120 real HVV stations using Dijkstra's algorithm with:
- Mode-specific commercial speeds (U-Bahn, S-Bahn, AKN, Regional)
- Average waiting times per line type
- Transfer penalties between lines
- Walk / connecting bus for first and last mile

---

## Limitations

- **Travel times are estimated**, not exact — real HVV timetables would give more accurate results
- **Adoption scores are based on assumptions** — a short employee survey would make them more reliable
- **Local buses are simplified** — using real HVV bus routes would improve accuracy for employees near the office

---

## Author

Sachini — Data Analytics Portfolio Project
