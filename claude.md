# claude.md — Glassnode x ARK: Decentralization Research Notebook

## Project Overview

You are helping build a Jupyter Notebook data pipeline for a joint research report between **Glassnode** and **ARK Investment**, assessing the decentralization of top crypto assets: **Bitcoin (BTC)**, **Ethereum (ETH)**, and **Solana (SOL)**.

This is a **Phase 01 scaffolding task**. The goal is to produce a clean, well-structured notebook boilerplate — with markdown outlines, placeholder data-fetching stubs, and a reusable visualization class — so that real API integrations can be dropped in during Phase 02.

---

## Notebook File

**Filename:** `decentralization_pipeline.ipynb`

---

## Notebook Structure

The notebook is organized into **three main parts**, each mirroring the report outline. Use the hierarchy below to generate notebook cells.

Each section follows this cell pattern:
1. A `## Markdown` cell with the section heading and a brief 1-2 sentence description
2. A `## Code` cell with a placeholder `fetch_` function stub
3. A `## Code` cell that calls the visualization class with placeholder/mock data

---

### Cell 0 — Imports and Configuration (top of notebook)

```python
# Standard imports
import pandas as pd
import numpy as np
import requests
import os
from datetime import datetime, timedelta
import plotly.graph_objects as go
from plotly.subplots import make_subplots
import plotly.express as px

# API Keys (load from environment variables — never hardcode)
GLASSNODE_API_KEY = os.getenv("GLASSNODE_API_KEY", "YOUR_API_KEY_HERE")
```

---

### Cell 1 — Visualization Class (standalone, defined once at top)

Define a single `DecentralizationVisualizer` class. It must be instantiated once and reused throughout the notebook. All chart methods live inside this class.

**Design rules:**
- Plotly only, light mode
- Default chart type: line chart with time on X axis and one or more Y axes
- Support dual Y-axis for charts comparing two metrics at different scales
- Support bar chart and pie chart as alternate modes
- Each method accepts a `pd.DataFrame`, a title string, axis label strings, and an optional `chart_type` parameter (`"line"` | `"bar"` | `"pie"`)
- All charts must include a consistent color palette across BTC (orange), ETH (blue/purple), SOL (green)
- Include a `show()` and optionally a `save(filename)` method
- Use `plotly.graph_objects` not `plotly.express` for multi-axis charts

**Stub signature:**

```python
class DecentralizationVisualizer:
    """
    Reusable Plotly visualization engine for the Glassnode x ARK decentralization report.
    Supports line, bar, and pie charts with consistent styling and multi-asset color coding.
    """

    COLORS = {
        "BTC": "#F7931A",
        "ETH": "#627EEA",
        "SOL": "#14F195",
        "neutral": "#888888"
    }

    def __init__(self, theme: str = "light"):
        # TODO: set plotly template and layout defaults
        pass

    def line_chart(self, df: pd.DataFrame, title: str, x_col: str,
                   y_cols: list, y_labels: list = None,
                   dual_axis: bool = False) -> go.Figure:
        # TODO: build multi-series line chart, support dual Y axis
        pass

    def bar_chart(self, df: pd.DataFrame, title: str, x_col: str,
                  y_col: str, color_col: str = None) -> go.Figure:
        # TODO: build grouped or stacked bar chart
        pass

    def pie_chart(self, labels: list, values: list, title: str) -> go.Figure:
        # TODO: build pie / donut chart for distribution data
        pass

    def show(self, fig: go.Figure):
        fig.show()

    def save(self, fig: go.Figure, filename: str):
        # TODO: save to HTML or PNG
        pass

viz = DecentralizationVisualizer()
```

---

## Part 1 — Foundations and Implications of Decentralization

> **Note:** Part 1 is primarily qualitative/narrative. Data cells here support contextual comparisons rather than deep metric pulls. Placeholders should reflect this.

---

### Section 1.1 — The Importance of Decentralization

**Markdown cell:**
```
## 1.1 The Importance of Decentralization

Decentralization underpins two foundational properties of public blockchains:
**property rights sovereignty** (tamper-proof, seizure-resistant ownership) and
**ledger assurance** (independent verifiability without trust assumptions).
This section provides contextual framing before quantitative analysis.
```

**Data stub:** No data fetch required. Markdown only.

---

### Section 1.2 — What Makes a Network Decentralized?

**Markdown cell:**
```
## 1.2 What Makes a Network Decentralized?

Four analytical dimensions: Auditability, Security, Governance, and Ownership & Distribution.
These dimensions map directly onto the quantitative metrics developed in Part 2.
```

**Data stub:** No data fetch required. Markdown only.

---

### Section 1.3 — Trade-offs in Decentralization

**Markdown cell:**
```
## 1.3 Trade-offs in Decentralization

### 1.3.1 Scalability
Higher throughput and gas limits increase node hardware requirements,
concentrating participation. This section examines the scalability-decentralization tension
using Ethereum's gas limit debate as a case study.

### 1.3.2 Coordination
More decentralized networks face higher friction in governance upgrades
due to the need for broad stakeholder consensus.
```

**Data stub:**

```python
def fetch_chain_performance_metrics(chains: list = ["BTC", "ETH", "SOL"]) -> pd.DataFrame:
    """
    Fetch L1 performance comparison metrics: TPS, gas/fee levels, node count.
    Sources: Blockworks Research API, Artemis Analytics API (Phase 02)
    
    Returns:
        pd.DataFrame with columns: [chain, tps, avg_fee_usd, node_count, timestamp]
    """
    # TODO Phase 02: implement Blockworks / Artemis API call
    # Reference: https://app.blockworksresearch.com/analytics/l1
    # Reference: https://app.artemisanalytics.com/chains
    mock_data = {
        "chain": ["BTC", "ETH", "SOL"],
        "tps": [7, 15, 2000],
        "avg_fee_usd": [1.5, 2.0, 0.001],
        "node_count": [15000, 9000, 1900],
        "timestamp": [datetime.utcnow()] * 3
    }
    return pd.DataFrame(mock_data)

df_chain_perf = fetch_chain_performance_metrics()
fig = viz.bar_chart(df_chain_perf, title="L1 Performance Comparison: TPS by Chain",
                    x_col="chain", y_col="tps", color_col="chain")
viz.show(fig)
```

---

### Section 1.4 — When is Decentralization Necessary?

**Markdown cell:**
```
## 1.4 When is Decentralization Necessary?

Demand for decentralization is contextual. Risk-averse, institutional capital gravitates
toward battle-tested networks (BTC, ETH). Speculative and retail capital often favors
throughput over censorship resistance (SOL). This section compares on-chain activity
signals across the three assets.
```

**Data stubs:**

```python
def fetch_transaction_count(chain: str, start_date: str, end_date: str) -> pd.DataFrame:
    """
    Fetch daily transaction count time series.
    Source: Glassnode API (BTC/ETH), Solscan or Helius API (SOL) — Phase 02
    
    Returns:
        pd.DataFrame with columns: [timestamp, tx_count, chain]
    """
    # TODO Phase 02: implement Glassnode /v1/transactions/count endpoint
    dates = pd.date_range(start=start_date, end=end_date, freq="D")
    mock = pd.DataFrame({
        "timestamp": dates,
        "tx_count": np.random.randint(300_000, 600_000, len(dates)),
        "chain": chain
    })
    return mock

def fetch_active_addresses(chain: str, start_date: str, end_date: str) -> pd.DataFrame:
    """
    Fetch daily active address count time series.
    Source: Glassnode API — Phase 02
    
    Returns:
        pd.DataFrame with columns: [timestamp, active_addresses, chain]
    """
    # TODO Phase 02: Glassnode /v1/addresses/active_count
    dates = pd.date_range(start=start_date, end=end_date, freq="D")
    mock = pd.DataFrame({
        "timestamp": dates,
        "active_addresses": np.random.randint(500_000, 1_200_000, len(dates)),
        "chain": chain
    })
    return mock

def fetch_rev(chain: str, start_date: str, end_date: str) -> pd.DataFrame:
    """
    Fetch daily Real Economic Value (REV) = fees + MEV (where applicable).
    Source: Blockworks Research API — Phase 02
    
    Returns:
        pd.DataFrame with columns: [timestamp, rev_usd, chain]
    """
    # TODO Phase 02: implement REV endpoint
    dates = pd.date_range(start=start_date, end=end_date, freq="D")
    mock = pd.DataFrame({
        "timestamp": dates,
        "rev_usd": np.random.uniform(1e6, 20e6, len(dates)),
        "chain": chain
    })
    return mock

START = "2023-01-01"
END = datetime.utcnow().strftime("%Y-%m-%d")

df_tx = pd.concat([fetch_transaction_count(c, START, END) for c in ["BTC", "ETH", "SOL"]])
df_addr = pd.concat([fetch_active_addresses(c, START, END) for c in ["BTC", "ETH", "SOL"]])
df_rev = pd.concat([fetch_rev(c, START, END) for c in ["BTC", "ETH", "SOL"]])

fig_tx = viz.line_chart(df_tx.pivot(index="timestamp", columns="chain", values="tx_count").reset_index(),
                        title="Daily Transaction Count: BTC vs ETH vs SOL",
                        x_col="timestamp", y_cols=["BTC", "ETH", "SOL"])
viz.show(fig_tx)
```

---

## Part 2 — Quantitative Measures of Decentralization

> **Note:** Part 2 is the empirical core. Every section has a data fetch stub and a visualization call.

---

### Section 2.1 — Node Participation and Accessibility

**Markdown cell:**
```
## 2.1 Node Participation and Accessibility

Node participation measures how accessible it is for independent parties to
run full validation infrastructure. Key dimensions include hardware cost,
disk requirements, bandwidth, and uptime. Lower cost = greater decentralization potential.
```

#### 2.1.1 — Cost to Run a Full Node

```python
def fetch_node_cost_estimates() -> pd.DataFrame:
    """
    Static or periodically updated cost estimates to run a full node per chain.
    Includes: disk space (GB), RAM (GB), bandwidth (TB/month), estimated monthly USD cost.
    Source: Manual research / community benchmarks — Phase 02
    
    Returns:
        pd.DataFrame with columns: [chain, disk_gb, ram_gb, bandwidth_tb, monthly_cost_usd]
    """
    # TODO Phase 02: source from node operator surveys or community benchmarks
    mock = {
        "chain": ["BTC", "ETH", "SOL"],
        "disk_gb": [600, 1200, 2000],
        "ram_gb": [8, 16, 256],
        "bandwidth_tb": [0.5, 1.5, 10],
        "monthly_cost_usd": [20, 80, 400]
    }
    return pd.DataFrame(mock)

df_node_cost = fetch_node_cost_estimates()
fig = viz.bar_chart(df_node_cost, title="Estimated Monthly Cost to Run a Full Node (USD)",
                    x_col="chain", y_col="monthly_cost_usd", color_col="chain")
viz.show(fig)
```

#### 2.1.2 — Validator and Issuer Centralization

```python
def fetch_validator_centralization() -> pd.DataFrame:
    """
    Snapshot of validator/miner distribution by entity share.
    BTC: top mining pools by hashrate share.
    ETH: top staking entities by stake share.
    SOL: top validators by stake share.
    Sources: BTC.com / Glassnode (BTC), rated.network (ETH), Solana Beach (SOL) — Phase 02
    
    Returns:
        pd.DataFrame with columns: [chain, entity, share_pct]
    """
    # TODO Phase 02: integrate pool distribution APIs
    mock = pd.DataFrame({
        "chain": ["BTC"] * 5 + ["ETH"] * 5 + ["SOL"] * 5,
        "entity": [f"BTC Pool {i}" for i in range(1, 6)] +
                  [f"ETH Staker {i}" for i in range(1, 6)] +
                  [f"SOL Validator {i}" for i in range(1, 6)],
        "share_pct": [28, 22, 18, 12, 20,
                      30, 20, 15, 20, 15,
                      35, 25, 15, 15, 10]
    })
    return mock

df_val = fetch_validator_centralization()
# Render as pie chart per chain
for chain in ["BTC", "ETH", "SOL"]:
    subset = df_val[df_val["chain"] == chain]
    fig = viz.pie_chart(labels=subset["entity"].tolist(),
                        values=subset["share_pct"].tolist(),
                        title=f"{chain} Validator/Miner Share Distribution")
    viz.show(fig)
```

#### 2.1.3 — Miner/Validator Reward Distribution (Entity-Level)

```python
def fetch_reward_distribution(chain: str, start_date: str, end_date: str) -> pd.DataFrame:
    """
    Daily reward distribution across top mining/staking entities.
    Source: Glassnode mining metrics (BTC), Dune Analytics / rated.network (ETH/SOL) — Phase 02
    
    Returns:
        pd.DataFrame with columns: [timestamp, entity, reward_usd, chain]
    """
    # TODO Phase 02: integrate entity-level reward tracking
    dates = pd.date_range(start=start_date, end=end_date, freq="D")
    mock = pd.DataFrame({
        "timestamp": dates,
        "top_entity_share_pct": np.random.uniform(20, 35, len(dates)),
        "chain": chain
    })
    return mock

df_rewards = pd.concat([fetch_reward_distribution(c, START, END) for c in ["BTC", "ETH", "SOL"]])
fig = viz.line_chart(df_rewards.pivot(index="timestamp", columns="chain",
                    values="top_entity_share_pct").reset_index(),
                     title="Top Entity Reward Share Over Time (%)",
                     x_col="timestamp", y_cols=["BTC", "ETH", "SOL"])
viz.show(fig)
```

#### 2.1.4 — Mining / Staking Pool Delegation Distribution

```python
def fetch_pool_delegation_distribution(chain: str) -> pd.DataFrame:
    """
    Distribution of delegated stake or hashrate across pools.
    Source: Glassnode miner metrics (BTC), Solana Beach delegation data (SOL) — Phase 02
    
    Returns:
        pd.DataFrame with columns: [pool_name, delegated_share_pct, chain]
    """
    # TODO Phase 02: implement pool-level delegation breakdown
    mock = pd.DataFrame({
        "pool_name": [f"Pool {i}" for i in range(1, 11)],
        "delegated_share_pct": np.random.dirichlet(np.ones(10)) * 100,
        "chain": chain
    })
    return mock

for chain in ["BTC", "ETH", "SOL"]:
    df_pool = fetch_pool_delegation_distribution(chain)
    fig = viz.bar_chart(df_pool, title=f"{chain} Pool Delegation Distribution",
                        x_col="pool_name", y_col="delegated_share_pct", color_col="pool_name")
    viz.show(fig)
```

#### 2.1.5 — Miner/Validator Operating Cost vs. Annual Rewards

```python
def fetch_operating_cost_vs_rewards(chain: str, start_date: str, end_date: str) -> pd.DataFrame:
    """
    Ratio of annual rewards earned vs. estimated operating costs for validators/miners.
    A higher ratio indicates more profitable — and likely more competitive — participation.
    Source: Glassnode miner revenue metrics (BTC), manual ETH/SOL cost modeling — Phase 02
    
    Returns:
        pd.DataFrame with columns: [timestamp, reward_to_cost_ratio, chain]
    """
    # TODO Phase 02: build cost model from hardware + energy + staking yield data
    dates = pd.date_range(start=start_date, end=end_date, freq="D")
    mock = pd.DataFrame({
        "timestamp": dates,
        "reward_to_cost_ratio": np.random.uniform(1.0, 3.5, len(dates)),
        "chain": chain
    })
    return mock

df_ratio = pd.concat([fetch_operating_cost_vs_rewards(c, START, END) for c in ["ETH", "SOL"]])
fig = viz.line_chart(df_ratio.pivot(index="timestamp", columns="chain",
                    values="reward_to_cost_ratio").reset_index(),
                     title="Validator Reward-to-Cost Ratio: ETH vs SOL",
                     x_col="timestamp", y_cols=["ETH", "SOL"])
viz.show(fig)
```

#### 2.1.6 — Client Diversity

```python
def fetch_client_diversity(chain: str) -> pd.DataFrame:
    """
    Distribution of node software clients across the network.
    Single-client dominance creates systemic risk (e.g., Solana 0-day bug).
    Source: clientdiversity.org (ETH), Helius orb stats (SOL) — Phase 02
    Reference: https://clientdiversity.org/#distribution
    Reference: https://orb.helius.dev/stats?cluster=mainnet-beta
    
    Returns:
        pd.DataFrame with columns: [client_name, share_pct, chain]
    """
    # TODO Phase 02: scrape or API-fetch client distribution data
    if chain == "ETH":
        clients = ["Geth", "Nethermind", "Besu", "Erigon", "Other"]
        shares = [35, 30, 15, 12, 8]
    else:  # SOL
        clients = ["Agave (Solana Labs)", "Firedancer", "Other"]
        shares = [85, 12, 3]
    return pd.DataFrame({"client_name": clients, "share_pct": shares, "chain": chain})

for chain in ["ETH", "SOL"]:
    df_clients = fetch_client_diversity(chain)
    fig = viz.pie_chart(labels=df_clients["client_name"].tolist(),
                        values=df_clients["share_pct"].tolist(),
                        title=f"{chain} Client Diversity Distribution")
    viz.show(fig)
```

#### 2.1.7 — Entity-Level Stake Aggregation (Nakamoto Coefficient)

```python
def fetch_nakamoto_coefficient() -> pd.DataFrame:
    """
    Nakamoto Coefficient: minimum number of entities required to control 67% of stake/hashrate.
    A higher number indicates greater decentralization.
    Source: rated.network (ETH), Solana Beach (SOL), BTC.com (BTC) — Phase 02
    Reference: https://explorer.rated.network
    Reference: https://solanabeach.io/validators
    
    Returns:
        pd.DataFrame with columns: [chain, nakamoto_coefficient, threshold_pct]
    """
    # TODO Phase 02: compute from live validator distribution data
    mock = {
        "chain": ["BTC", "ETH", "SOL"],
        "nakamoto_coefficient": [3, 4, 19],
        "threshold_pct": [51, 67, 67]
    }
    return pd.DataFrame(mock)

df_nakamoto = fetch_nakamoto_coefficient()
fig = viz.bar_chart(df_nakamoto, title="Nakamoto Coefficient by Chain (Entities to Control 67% Stake)",
                    x_col="chain", y_col="nakamoto_coefficient", color_col="chain")
viz.show(fig)
```

---

### Section 2.2 — Governance Participation and Control

**Markdown cell:**
```
## 2.2 Governance Participation and Control

Governance decentralization measures whether protocol changes require
broad consensus or can be enacted unilaterally. Developer diversity is a
leading proxy for governance health — single-entity contributor dominance
indicates fragility.
```

#### 2.2.1 — Developer Contributions

```python
def fetch_developer_contributions() -> pd.DataFrame:
    """
    Developer activity breakdown: number of active monthly developers,
    contributor concentration (top entity share), and total commits.
    Source: Electric Capital Developer Report, DeveloperReport.com — Phase 02
    Reference: https://developerreport.com
    
    Returns:
        pd.DataFrame with columns: [chain, monthly_active_devs, top_entity_share_pct, total_commits_ytd]
    """
    # TODO Phase 02: integrate Electric Capital or DeveloperReport data
    mock = {
        "chain": ["BTC", "ETH", "SOL"],
        "monthly_active_devs": [850, 5800, 2100],
        "top_entity_share_pct": [15, 8, 45],
        "total_commits_ytd": [2000, 35000, 12000]
    }
    return pd.DataFrame(mock)

df_devs = fetch_developer_contributions()
fig = viz.bar_chart(df_devs, title="Monthly Active Developers by Chain",
                    x_col="chain", y_col="monthly_active_devs", color_col="chain")
viz.show(fig)
```

---

### Section 2.3 — Ownership Distribution

**Markdown cell:**
```
## 2.3 Ownership Distribution

Token ownership concentration is a structural risk factor. This section examines
supply distribution across address cohorts, founder/VC allocation vs. community issuance,
and the share of supply held by the largest addresses.
```

#### 2.3.1 — Token Supply by Address Cohort

```python
def fetch_supply_by_cohort(chain: str) -> pd.DataFrame:
    """
    Supply distribution across address balance cohorts (e.g., < 1 token, 1-10, 10-100, etc.).
    Source: Glassnode Supply Distribution metrics — Phase 02
    
    Returns:
        pd.DataFrame with columns: [cohort_label, supply_pct, chain]
    """
    # TODO Phase 02: Glassnode /v1/distribution/balance_* endpoints
    cohorts = ["< 0.001", "0.001-0.01", "0.01-0.1", "0.1-1", "1-10", "10-100", "100-1000", "> 1000"]
    mock = pd.DataFrame({
        "cohort_label": cohorts,
        "supply_pct": np.random.dirichlet(np.ones(8)) * 100,
        "chain": chain
    })
    return mock

for chain in ["BTC", "ETH", "SOL"]:
    df_cohort = fetch_supply_by_cohort(chain)
    fig = viz.bar_chart(df_cohort, title=f"{chain} Supply Distribution by Address Cohort",
                        x_col="cohort_label", y_col="supply_pct", color_col="cohort_label")
    viz.show(fig)
```

#### 2.3.2 — Founder/VC Allocation vs. Community Issuance

```python
def fetch_token_allocation_breakdown() -> pd.DataFrame:
    """
    Genesis and ongoing supply allocation: what % went to founders, VCs, community, or PoW mining.
    Source: Token unlock schedules, whitepapers, on-chain genesis analysis — Phase 02
    
    Returns:
        pd.DataFrame with columns: [chain, category, allocation_pct]
    """
    # TODO Phase 02: source from tokenomics research and unlock schedule data
    mock = pd.DataFrame({
        "chain":    ["BTC", "BTC", "ETH", "ETH", "ETH", "SOL", "SOL", "SOL", "SOL"],
        "category": ["PoW Mining", "Unissued",
                     "Community/PoW", "Founders/EF", "Unissued",
                     "Community Sale", "Insiders/VC", "Foundation", "Unissued"],
        "allocation_pct": [50, 50,
                           70, 12, 18,
                           38, 40, 12, 10]
    })
    return mock

df_alloc = fetch_token_allocation_breakdown()
for chain in ["BTC", "ETH", "SOL"]:
    subset = df_alloc[df_alloc["chain"] == chain]
    fig = viz.pie_chart(labels=subset["category"].tolist(),
                        values=subset["allocation_pct"].tolist(),
                        title=f"{chain} Token Allocation: Founders/VC vs. Community")
    viz.show(fig)
```

#### 2.3.3 — % of Supply Held by Top X Addresses

```python
def fetch_top_address_supply_concentration(chain: str, start_date: str, end_date: str) -> pd.DataFrame:
    """
    Time series of supply % held by top 1%, top 10%, and top 100 addresses.
    Source: Glassnode /v1/distribution/supply_* endpoints — Phase 02
    
    Returns:
        pd.DataFrame with columns: [timestamp, top_1pct_supply, top_10pct_supply, top_100_addresses, chain]
    """
    # TODO Phase 02: Glassnode supply distribution endpoints
    dates = pd.date_range(start=start_date, end=end_date, freq="D")
    mock = pd.DataFrame({
        "timestamp": dates,
        "top_1pct_supply": np.random.uniform(25, 35, len(dates)),
        "top_10pct_supply": np.random.uniform(55, 70, len(dates)),
        "top_100_addresses": np.random.uniform(10, 20, len(dates)),
        "chain": chain
    })
    return mock

df_conc = pd.concat([fetch_top_address_supply_concentration(c, START, END) for c in ["BTC", "ETH", "SOL"]])
# Example: top 1% supply concentration over time, all chains
fig = viz.line_chart(
    df_conc.pivot(index="timestamp", columns="chain", values="top_1pct_supply").reset_index(),
    title="% of Supply Held by Top 1% of Addresses: BTC vs ETH vs SOL",
    x_col="timestamp", y_cols=["BTC", "ETH", "SOL"]
)
viz.show(fig)
```

---

## Part 3 — BTC, ETH, and SOL Compared (and Conclusion)

---

### Section 3.1 — Cross-Chain Comparative Summary

**Markdown cell:**
```
## 3.1 Cross-Chain Comparative Summary

This section consolidates all decentralization vectors — node accessibility,
validator concentration, client diversity, governance, and ownership distribution —
into a side-by-side comparison of BTC, ETH, and SOL.
```

```python
def build_decentralization_scorecard() -> pd.DataFrame:
    """
    Aggregate scorecard: normalized decentralization scores per dimension per chain.
    Dimensions: Node Cost, Nakamoto Coefficient, Client Diversity, Developer Concentration, Ownership Gini.
    Source: Derived from all fetch functions above — Phase 02 will compute from real data.
    
    Returns:
        pd.DataFrame with columns: [dimension, BTC, ETH, SOL]
        Scores normalized 0-10 (10 = most decentralized)
    """
    # TODO Phase 02: compute scores from real data
    mock = {
        "dimension": ["Node Accessibility", "Validator Concentration",
                      "Client Diversity", "Developer Diversity",
                      "Ownership Distribution", "Governance Openness"],
        "BTC": [9.0, 6.5, 9.5, 7.0, 5.5, 8.0],
        "ETH": [6.5, 7.0, 8.0, 9.0, 6.0, 7.5],
        "SOL": [3.5, 4.5, 2.0, 5.5, 4.0, 4.5]
    }
    return pd.DataFrame(mock)

df_scorecard = build_decentralization_scorecard()
# Render as grouped bar chart
fig = viz.bar_chart(
    df_scorecard.melt(id_vars="dimension", var_name="chain", value_name="score"),
    title="Decentralization Scorecard: BTC vs ETH vs SOL",
    x_col="dimension", y_col="score", color_col="chain"
)
viz.show(fig)
```

---

### Section 3.2 — Cost of Economic Attack

**Markdown cell:**
```
## 3.2 Cost of Economic Attack

The economic security of a network can be proxied by the cost required
to execute a majority attack: 51% of hashpower for BTC, or acquiring
33% and 67% of staked supply for ETH and SOL.
```

```python
def fetch_attack_cost_estimates(start_date: str, end_date: str) -> pd.DataFrame:
    """
    Estimated USD cost to execute a majority economic attack on each chain.
    BTC: cost to acquire 51% of current hashrate (hardware + energy).
    ETH: cost to acquire 33% and 67% of staked ETH at spot price.
    SOL: cost to acquire 33% and 67% of staked SOL at spot price.
    Source: Glassnode hashrate/miner metrics (BTC), on-chain staking data (ETH/SOL) — Phase 02
    
    Returns:
        pd.DataFrame with columns: [timestamp, chain, attack_threshold_pct, attack_cost_usd]
    """
    # TODO Phase 02: build cost model from hashrate, price, and staking data
    dates = pd.date_range(start=start_date, end=end_date, freq="D")
    rows = []
    for date in dates:
        rows.append({"timestamp": date, "chain": "BTC", "attack_threshold_pct": 51,
                     "attack_cost_usd": np.random.uniform(8e9, 12e9)})
        rows.append({"timestamp": date, "chain": "ETH", "attack_threshold_pct": 33,
                     "attack_cost_usd": np.random.uniform(25e9, 35e9)})
        rows.append({"timestamp": date, "chain": "ETH", "attack_threshold_pct": 67,
                     "attack_cost_usd": np.random.uniform(50e9, 70e9)})
        rows.append({"timestamp": date, "chain": "SOL", "attack_threshold_pct": 33,
                     "attack_cost_usd": np.random.uniform(2e9, 5e9)})
        rows.append({"timestamp": date, "chain": "SOL", "attack_threshold_pct": 67,
                     "attack_cost_usd": np.random.uniform(4e9, 10e9)})
    return pd.DataFrame(rows)

df_attack = fetch_attack_cost_estimates(START, END)
# Example: BTC 51% attack cost over time
btc_attack = df_attack[df_attack["chain"] == "BTC"]
fig = viz.line_chart(btc_attack, title="Estimated Cost of 51% Attack: BTC",
                     x_col="timestamp", y_cols=["attack_cost_usd"])
viz.show(fig)
```

---

### Section 3.3 — Conclusion

**Markdown cell:**
```
## 3.3 Conclusion

[Narrative conclusion authored by David — to be written after quantitative analysis is complete.]

Key themes expected:
- BTC maintains the strongest structural decentralization case across node accessibility and immutability
- ETH trades some decentralization for programmability but preserves meaningful distribution
- SOL optimizes for performance at measurable cost to decentralization on most vectors
- The appropriate level of decentralization is contextual and capital-demand-driven
```

**No data fetch required for this section.**

---

## Phase 01 Completion Checklist

- [ ] `DecentralizationVisualizer` class defined at top of notebook with all stub methods
- [ ] All 3 parts structured as markdown cells with correct heading hierarchy
- [ ] All data fetch functions stubbed with docstrings, return types, and mock data
- [ ] All visualization calls present after each fetch, using mock data
- [ ] API keys loaded from environment variables only
- [ ] No hardcoded credentials anywhere in the notebook
- [ ] `START` and `END` date variables defined globally and referenced throughout

---

## Phase 02 Preview (for awareness only — do not implement yet)

When Phase 02 begins, each `# TODO Phase 02` stub will be replaced with:
- **Glassnode API** calls for BTC/ETH on-chain metrics (hashrate, supply distribution, miner revenue)
- **Rated.network API** for ETH validator stake distribution
- **Helius/Solana Beach** for SOL validator data
- **Electric Capital / DeveloperReport** for developer diversity data
- **Custom cost modeling** for node operating cost and economic attack scenarios

All API integrations will follow the same function signature established in the stubs.
