# Research Plan: GenAI & Corporate Financial Policy

## Executive Summary

**Research Question:** How did the emergence of generative AI (ChatGPT release, November 2022) affect corporate investment, employment, and capital allocation decisions?

**Identification Strategy:** Difference-in-Differences using heterogeneous firm-level exposure to AI-driven automation.

---

## 1. Motivation & Contribution

### Why This Matters for Tier-1 Journals

| Factor | Strength |
|--------|----------|
| **Timeliness** | GenAI is the defining technology shock of the 2020s |
| **Clean identification** | ChatGPT release was sudden and unexpected |
| **Data availability** | Standard Compustat variables + occupational exposure data |
| **Policy relevance** | Informs labor policy, corporate governance, investor decisions |
| **Broad appeal** | Spans technology, corporate finance, labor economics |

### Potential Outlets
- **Journal of Finance** (broad interest)
- **Journal of Financial Economics** (corporate policy focus)
- **Review of Financial Studies** (methodology strength)
- **Management Science** (technology + strategy angle)

---

## 2. Theoretical Framework

### Channels Through Which GenAI Affects Firms

```
ChatGPT Release (Nov 2022)
         │
         ▼
┌────────────────────────────────────────┐
│     Firm's AI Exposure (Treatment)      │
│  (based on workforce composition)       │
└────────────────────────────────────────┘
         │
         ▼
┌────────────────────────────────────────────────────────────┐
│                    Firm Responses                          │
├──────────────────┬──────────────────┬─────────────────────┤
│   Investment     │   Employment     │   Capital Structure  │
│   - CapEx ↑/↓    │   - Headcount    │   - Cash holdings   │
│   - R&D ↑        │   - Composition  │   - Leverage        │
│   - Acquisitions │                  │   - Payouts         │
└──────────────────┴──────────────────┴─────────────────────┘
```

### Testable Hypotheses

**H1 (Investment):** High-AI-exposure firms increase investment in technology (CapEx, R&D) post-ChatGPT.

**H2 (Employment):** High-AI-exposure firms reduce headcount relative to low-exposure firms.

**H3 (Productivity):** High-AI-exposure firms show improved revenue-per-employee.

**H4 (Valuation):** Market capitalizations of high-exposure firms increase (anticipating productivity gains) OR decrease (anticipating disruption).

---

## 3. Data Requirements

### Your Dataset Variables

| Variable | Use in Study | Available? |
|----------|--------------|------------|
| Company identifiers | Firm fixed effects | Yes |
| Industry classification | AI exposure measure | Yes |
| Market Cap (10 years) | Valuation response | Yes |
| Revenue (40 quarters) | Productivity numerator | Yes |
| Employees (40 quarters) | Employment response + productivity | Yes |
| CapEx (40 quarters) | Investment response | Yes |
| R&D Expense (40 quarters) | Technology investment | Yes |
| Cash (40 quarters) | Liquidity response | Yes |
| Debt (40 quarters) | Capital structure | Yes |
| EBITDA (40 quarters) | Profitability control | Yes |

### External Data Needed (Free/Publicly Available)

1. **Occupation-level AI exposure scores**
   - Felten, Raj, & Seamans (2023) AI exposure by occupation
   - Available: https://github.com/MITEcon/AI_Exposure

2. **Industry-occupation crosswalk**
   - BLS Occupational Employment Statistics
   - Maps industries to occupational composition

---

## 4. Methodology

### 4.1 AI Exposure Measure

Following Felten et al. (2023):

```
AI_Exposure_i = Σ_j (Employment_ij / Employment_i) × AI_Score_j
```

Where:
- `i` = firm/industry
- `j` = occupation
- `AI_Score_j` = occupation-level AI exposure score

### 4.2 Main Specification (Difference-in-Differences)

```
Y_it = α_i + α_t + β(High_Exposure_i × Post_t) + γX_it + ε_it
```

Where:
- `Y_it` = outcome (CapEx/Assets, Employees, R&D/Revenue, etc.)
- `α_i` = firm fixed effects
- `α_t` = time fixed effects
- `High_Exposure_i` = indicator for above-median AI exposure
- `Post_t` = indicator for Q4 2022 onwards
- `X_it` = time-varying controls

### 4.3 Event Study Specification

```
Y_it = α_i + α_t + Σ_k β_k(High_Exposure_i × 1{t=k}) + γX_it + ε_it
```

This traces out the dynamic treatment effect quarter-by-quarter.

### 4.4 Key Identification Assumptions

1. **Parallel trends**: High and low exposure firms followed similar trends pre-ChatGPT
2. **No anticipation**: Firms didn't adjust before November 2022
3. **SUTVA**: Treatment doesn't spill over to control firms

---

## 5. Analysis Pipeline

### Notebook Structure

```
01_data_exploration.ipynb      <- Current: Understand your data
02_construct_treatment.ipynb   <- Build AI exposure measure
03_panel_construction.ipynb    <- Reshape to firm-quarter panel
04_descriptive_stats.ipynb     <- Summary statistics, balance tests
05_main_results.ipynb          <- DiD and event study estimates
06_robustness.ipynb            <- Alternative specifications
07_mechanisms.ipynb            <- Heterogeneity analysis
08_figures_tables.ipynb        <- Publication-ready outputs
```

### Key Outputs for Paper

1. **Table 1**: Summary statistics by AI exposure group
2. **Table 2**: Main DiD results (multiple outcomes)
3. **Figure 1**: Event study plots showing parallel trends + treatment effect
4. **Table 3**: Heterogeneity by firm size, industry, financial constraints
5. **Table 4**: Robustness checks

---

## 6. Timeline (Milestones, Not Dates)

### Phase 1: Data Preparation
- [ ] Run exploration notebook, verify data quality
- [ ] Obtain AI exposure scores from Felten et al.
- [ ] Construct treatment variable
- [ ] Build clean firm-quarter panel

### Phase 2: Preliminary Analysis
- [ ] Summary statistics
- [ ] Validate parallel trends assumption
- [ ] Preliminary DiD estimates

### Phase 3: Main Analysis
- [ ] Event study specifications
- [ ] Multiple outcome variables
- [ ] Robustness checks

### Phase 4: Writing
- [ ] Draft introduction and literature review
- [ ] Write methodology section
- [ ] Results and discussion
- [ ] Circulate for feedback

---

## 7. Potential Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| AI exposure measure validity | Use multiple measures; cite established papers |
| Short post-period (2 years) | Focus on immediate responses; note limitation |
| Confounding events (rate hikes, SVB) | Include time fixed effects; robustness with subperiods |
| Measurement error in employees | Use multiple data sources if available |
| Selection into treatment | Firm fixed effects; pre-treatment characteristics balance |

---

## 8. Alternative/Complementary Ideas

If GenAI story doesn't work out:

1. **COVID + Capital Structure** - Very clean shock, tons of data points
2. **Interest Rate Shock** - Fed's 2022-23 hiking cycle
3. **Labor-Capital Substitution Trends** - 10-year automation analysis

---

## Next Steps

1. **Run `01_data_exploration.ipynb`** in Colab
2. **Share outputs** so we can verify time coverage
3. **Confirm** which industries are represented
4. **Proceed** with treatment construction
