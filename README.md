# Multi-Objective Portfolio Optimization over On-Chain Trading Vaults: An Evolutionary Approach

**[Read the thesis (PDF)](https://github.com/eloysentana/Final-Thesis-Multi-Objective-Portfolio-Optimization-for-On-Chain-Vaults-An-Evolutionary-Approach/blob/main/Multi-Objective%20Portfolio%20Optimization%20for%20On-Chain%20Vaults%20An%20Evolutionary%20Approach.pdf)**

Given thousands of **vaults** (opaque trading strategies on a blockchain exchange,
where all you see is a daily return series), which ones do you invest in, and how much
in each?

## Why not just use Markowitz?

Modern Portfolio Theory describes each asset with two numbers, expected return and
variance, and assumes roughly Gaussian returns. Vault returns break both assumptions:
the distributions are heavy-tailed and negatively skewed, and mean/variance alone say
nothing about drawdown behavior or consistency.

This thesis keeps the core idea (balance reward against risk) and rebuilds the rest as
a **many-objective** optimization problem.

## Approach

Each vault is described by 23 performance metrics, reduced to 10 via group-aware greedy
forward selection (retaining 92.6% of standardized variance). Selecting a subset and
weight vector over thousands of vaults against those 10 objectives is solved in three stages:

| Stage | Method | Role |
|---|---|---|
| 1 | Data Envelopment Analysis | Pre-screen thousands of vaults down to ~80 candidates |
| 2 | NSGA-III | Many-objective genetic search producing a Pareto-approximating set |
| 3 | TOPSIS | Multi-criteria decision making, picking one portfolio from the front |

Objectives are computed on the aggregated portfolio return series, not as weighted
averages of per-vault statistics, which is the easiest mistake to make in this class of
problem. Results are validated with walk-forward backtesting against random
equal-weight portfolios.

## Results

The pipeline works as intended: the DEA shortlist beats the full universe on all ten
metrics, NSGA-III improves nine of ten consistently across generations, and TOPSIS
picks a portfolio with a better risk-return balance than a random pick of ten vaults.

Out of sample, results are positive but not decisive: the method beats a random pick in
23 of 28 tests, compounding about 1.2 percentage points per year faster. The honest
caveat: the vault universe as a whole loses money over the period studied, so beating
random means picking the best of a losing set.

## Contents

1. Introduction
2. Modern Portfolio Theory and Statistical Framework
3. Portfolio Construction Over On-Chain Trading Vaults
4. Data and Vault Characterization
5. Methodology: A Three-Stage Selection Pipeline
6. Results: Pipeline Validation and Walk-Forward Performance
7. Conclusions and Future Work
8. Regulatory Framework

## Limitations

Compute was the binding constraint: reported runs use a small population over a few
hundred generations, not enough to guarantee convergence. Everything is backtested on
blockchain vaults, so generalization to other markets is untested. No sensitivity
analysis was run on lookback/investment window length.

## Author

Eloy Sentana Seguí.

## Grading

This thesis received a 10/10 and was proposed for Honours (pending ratification) by Universidad Carlos III de Madrid, Spain.

## License

All rights reserved. This work is shared for reference only. No part of it may be
copied, redistributed, or reused without the author's written permission.
