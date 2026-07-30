# Data Dictionary — `PyOutput_Sn_Cn.xlsx`

> **Note:** This README describes the structure of the raw model-run output
> workbook (one workbook per coalition scenario). Sn refers to the serial number assigned, and Cn, the number of coalition blocks for that scenario.
> It complements the top-level `README.md`, which covers the repository
> overview and folder structure only.
>
## Background: sets and indices used throughout

All sheets are indexed by some combination of the following (see the
Sets/Variables table in the paper):

| Symbol | Meaning | In this dataset |
|---|---|---|
| $p$ | Producer | 13 producers (see ordering in `Run`, cell A4) |
| $n$ | Node | 14 nodes: 13 correspond to a producer's own demand region; the 14th represents export, modeled as external demand rather than a producer-owned region |
| $h$ | Season | [4 seasons] |
| $t$ | Year | [2020–2050] |
| coalition | Which producers are grouped together in this run | One column/block per producer pair or coalition membership, consistent with the indicator variables used in the regression (see `Sec 2.2 Coalition formulation `) |

## Producer, node, season, and year labels

`Producers:` ['P_ALK', 'P_CAE', 'P_CAW', 'P_MEX2', 'P_MEX5', 'P_US2', 'P_US3', 'P_US4', 'P_US5', 'P_US6', 'P_US7', 'P_US8', 'P_US9']

`Nodes:` ['N_ALK', 'N_CAE', 'N_CAW', 'N_MEX2', 'N_MEX5', 'N_US2', 'N_US3', 'N_US4', 'N_US5', 'N_US6', 'N_US7', 'N_US8', 'N_US9', 'N_External']

`Seasons:`['summer', 'fall', 'winter', 'spring']

`Year:`[2020, 2025, 2030, 2035, 2040, 2045, 2050]

Flow and stock quantities (production, storage,
liquefaction, transport, sales) are in **bcm**; surplus, revenue, and
investment cost figures are in **mUSD**.
---

## Sheet 1: `run`

**What it is:** The main results overview sheet — one row per model run (i.e., per
coalition scenario), summarizing that scenario's headline outcomes.

**Columns:**

| Column | Description |
|---|---|
| Producer count | Fixed at 13 for all runs |
| Node count | Fixed at 14 for all runs (13 producer regions + 1 export/external-demand node) |
| Season, Year | Confirms the temporal resolution used to generate this run's underlying flows |
| Coalitions | Indicates which producers are grouped together in this scenario (e.g. a set of coalition-membership string identifying the pairing/grouping) |
| Total Producer Surplus | Aggregate producer surplus across all 13 producers for this scenario (mUSD) |
| Total Revenue | Aggregate sales revenue across all producers for this scenario (mUSD) |
| Total Consumer Surplus | Aggregate consumer surplus for this scenario (mUSD) |
| Total Social Surplus | Total Producer Surplus + Total Consumer Surplus (mUSD) |
| Individual producer surplus | Each producer's own producer surplus for this scenario, in the same producer order as listed in cell A4 |
| Individual consumer surplus | Each producer's own consumer surplus for this scenario, in the same producer order as listed in cell A4 |


**Note:** This is the sheet from which `regression_results.xlsx` is built —
the `Producer_Surplus_Diff` / `Consumer_Surplus_Diff` columns used in the
regression are each scenario's Total Producer/Consumer Surplus here, minus
the fully-independent base-case values. Additionally, the coaltions indicated 
helps us to form the indicator variables that determine if two producers are 
in a coalition or not.

---

## Sheet 2: `strI`

**What it is:** Total storage capacity investment decided per producer,
for this scenario. Corresponds to $I_{p,n}$ in the model.

**Grain:** One value per producer (per node).

**Columns:** Producer, Node (if applicable), Storage Investment (bcm).

---

## Sheet 3: `strQ`

**What it is:** Actual storage level held by a given producer, at a given
node, in a given season and year. Corresponds to $S_{p,n,h,t}$.

**Grain:** One row per (producer, node, season, year) combination.

**Columns:** Producer, Node, Season, Year, Storage Quantity (bcm).

---

## Sheet 4: `prodI`

**What it is:** Production capacity investment decided by a producer in a
given year. Corresponds to $I^{\text{prod}}_{p,n,t}$.

**Grain:** One row per (producer, node, year) combination.

**Columns:** Producer, Node, Year, Production Investment (bcm capacity).

---

## Sheet 5: `prodQ`

**What it is:** Actual gas production quantity by a producer, at a given
node, in a given season and year. Corresponds to $Q^{\text{prod}}_{p,n,h,t}$.

**Grain:** One row per (producer, node, season, year) combination.

**Columns:** Producer, Node, Season, Year, Production Quantity (bcm).

---

## Sheet 6: `Qliquify`

**What it is:** Quantity of gas liquefied (converted to LNG) by a
producer, at a node, in a season/year. Corresponds to
$Q^{\text{liq}}_{p,n,h,t}$.

**Grain:** One row per (producer, node, season, year) combination.

**Columns:** Producer, Node, Season, Year, Liquefied Quantity (bcm).

---

## Sheet 7: `Qgasify`

**What it is:** Quantity of LNG regasified back into pipeline gas by a
producer, at a node, in a season/year. Corresponds to
$Q^{\text{gas}}_{p,n,h,t}$.

**Grain:** One row per (producer, node, season, year) combination.

**Columns:** Producer, Node, Season, Year, Regasified Quantity (bcm).

---

## Sheet 8: `Qtgas`

**What it is:** Quantity of pipeline gas transported by a producer from
one node to another, in a given season/year. Corresponds to
$Q^{\text{trans-gas}}_{p,n,n',h,t}$.

**Grain:** One row per (producer, node-from, node-to, season, year)
combination.

**Columns:** Producer, Node_From, Node_To, Season, Year, Gas Transported (bcm).

---

## Sheet 9: `Qtlng`

**What it is:** Quantity of LNG transported by a producer from one node
to another, in a given season/year. Corresponds to
$Q^{\text{trans-lng}}_{p,n,n',h,t}$.

**Grain:** One row per (producer, node-from, node-to, season, year)
combination.

**Columns:** Producer, Node_From, Node_To, Season, Year, LNG Transported (bcm).

---

## Sheet 10: `sellQG`

**What it is:** Quantity of gas sold by a producer at a given node, in a
given season/year. Corresponds to $Q^{\text{sell-G}}_{p,n,h,t}$.

**Grain:** One row per (producer, node, season, year) combination.

**Columns:** Producer, Node, Season, Year, Gas Sold (bcm).

---

## Sheet 11: `sellQL`

**What it is:** Quantity of LNG sold by a producer at a given node, in a
given season/year. Corresponds to $Q^{\text{sell-L}}_{p,n,h,t}$.

**Grain:** One row per (producer, node, season, year) combination.

**Columns:** Producer, Node, Season, Year, LNG Sold (bcm).

---
