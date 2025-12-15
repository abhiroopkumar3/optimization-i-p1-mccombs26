# Portfolio Optimization Using Conditional Value-at-Risk (CVaR)

## Project Overview
This project applies **linear programming** techniques to construct and evaluate **risk-aware investment portfolios** using **Conditional Value-at-Risk (CVaR)** as the primary risk measure.

Using daily stock return data from the **NASDAQ-100 universe**, we design portfolios under normal market conditions (2019) and evaluate their robustness during an extreme stress period (2020, COVID-19). The project explores static optimization, sensitivity to confidence levels, conservative monthly risk control, and dynamic rebalancing strategies.

---

## Objectives
- Minimize downside tail risk using CVaR optimization  
- Compare static vs. dynamic portfolio strategies  
- Evaluate performance under extreme market volatility  
- Analyze trade-offs between risk reduction, stability, and turnover  

---

## Data Description
- **Universe:** NASDAQ-100 stocks  
- **Training period:** 2019 (normal market conditions)  
- **Out-of-sample test period:** 2020 (COVID-19 volatility)  
- **Returns:** Daily percentage returns  

This split allows the model to be trained in stable conditions and tested during a real market stress event.

---

## Methodology

### 1. CVaR Portfolio Optimization
We formulate a **linear programming model** to minimize CVaR at a confidence level β.

**Decision Variables**
- Portfolio weights \( x_j \) for each stock  
- \( \alpha \): Value-at-Risk (VaR) threshold  
- Auxiliary variables \( u_k \) to linearize tail losses  

**Objective**
Minimize CVaR (expected loss in the worst β% of cases)

**Constraints**
- Fully invested portfolio (weights sum to 1)  
- Minimum expected return (R = 0.02% daily)  
- Non-negativity constraints  
- Linearized loss constraints for CVaR  

---

## Experiments & Analysis

### Part 1: Baseline CVaR Optimization (β = 0.95)
- Optimized on 2019 data
- **2019 CVaR:** 1.11%
- **Out-of-sample 2020 CVaR:** 4.66%
- Significantly lower tail risk than the NASDAQ-100 index in both years

---

### Part 2: Sensitivity Analysis (β = 0.90, 0.95, 0.99)
- Lower β → more diversified portfolios
- Higher β → more conservative, concentrated portfolios
- Trade-off between diversification and extreme tail protection

---

### Part 3: Minimizing Maximum Monthly CVaR
- Introduced a **worst-case monthly risk constraint**
- Optimized the maximum CVaR across all months
- Resulted in more stable risk exposure across the year
- **Monthly CVaR ≈ 1.24%**, smoother than annual CVaR optimization

---

### Part 4: Monthly Rebalancing Strategy
- Re-optimized portfolio monthly using rolling 12-month windows
- **Average daily CVaR:** 3.22%  
- **31% improvement** over static portfolio on average
- However, exposed to extreme spikes (e.g., March 2020)

---

### Part 5: Portfolio Stability & Turnover
- Monthly rebalancing caused frequent weight changes >5%
- High turnover during market stress
- Identified trade-off between adaptability and implementation cost

**Proposed Stability Enhancements**
- Add weight-change constraints between months
- Penalize excessive reallocation in the objective function

---

## Key Findings
- CVaR optimization significantly reduces downside risk vs. market index
- Static portfolios are stable but less adaptive
- Monthly rebalancing lowers average risk but increases volatility and turnover
- Risk management strategy choice depends on investor priorities:
  - Stability vs. responsiveness
  - Predictability vs. adaptability

---

## Tools & Technologies
- **Python**
- **Gurobi Optimizer**
- **Pandas / NumPy** – Data processing
- **Matplotlib** – Visualization
- **Linear Programming**

---

## Authors

- Abhiroop Kumar
- Manny Escalante
- Simoni Dalal
- Stiles Clements

---

## Disclaimer

This project is for academic purposes only and does not constitute financial or investment advice.
