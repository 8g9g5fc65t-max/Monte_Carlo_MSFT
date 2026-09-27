Monte Carlo Simulation: Microsoft (MSFT) Stock Price Forecasting

Monte Carlo simulation of Microsoft's (MSFT) future stock price using Geometric Brownian Motion (GBM), calibrated on 5 years of historical daily price data.

Objective

The objective of this project is to model the future price path of MSFT stock under uncertainty, and to translate that uncertainty into concrete, probability-weighted risk and return estimates — rather than a single point forecast. The simulation is used to answer practical questions an investor would actually ask: what is the probability of losing money on this position over a 1-year horizon, and what does the range of likely outcomes look like?

Methodology

The analysis is structured into five sequential phases:

Data Acquisition — 5 years of daily OHLCV data for MSFT (2020–2026) pulled via the yfinance API.
Return Calculation — daily logarithmic returns are computed from adjusted closing prices, and used to estimate the drift and volatility parameters of the GBM process.
Simulation — 1,000 independent price paths are simulated over a 252-trading-day (1-year) horizon using the standard GBM discretisation, drawing pseudo-random shocks from a standard normal distribution.
Percentile & Distribution Analysis — the 5th, 50th and 95th percentiles of the simulated terminal price distribution are computed at each step and plotted alongside the full set of simulated trajectories.
Risk Metrics — the simulated terminal-price distribution is used to estimate the probability of a loss, the probability of a loss exceeding 10% or 50%, and the probability of doubling the investment.
Key Findings

Based on the 5-year calibration window and a starting price of $410.68:

Metric	Estimate
Expected (mean) price, 1-year horizon	≈ $482
Median (50th percentile) price	≈ $461
5th percentile (downside) price	≈ $291
95th percentile (upside) price	≈ $741
Probability of a loss	≈ 34%
Probability of losing more than 10%	≈ 22%
Probability of losing more than 50%	≈ 0.3%
Probability of doubling the investment	≈ 2.5%

Note: these figures are the output of a stochastic simulation and will vary slightly each time the notebook is re-run (a fixed random seed is not set). The conclusions are stable across runs even though the exact percentages fluctuate.

Over the analysed window, the simulation suggests a favourable risk/reward profile for MSFT: a relatively high probability of a positive outcome, with the probability of a severe loss (>50%) staying very low.

Limitations & Possible Extensions

This is a first-pass model, and several simplifying assumptions could be relaxed in future iterations:

Fat tails: the model assumes normally-distributed daily returns; real markets exhibit fat tails, i.e. extreme moves occur more often than a normal distribution predicts. A Student's-t or bootstrapped-residual approach would capture this better.
Dynamic volatility: volatility is assumed constant over the simulation horizon; in reality it clusters and varies over time (see the GARCH-based models used in my Master's thesis). Incorporating a GARCH-simulated volatility path would make the model more realistic.
More data: the 5-year estimation window could be extended to 10–15 years to obtain more robust drift/volatility estimates.
Repository Contents
montecarlo_msft.ipynb — the Jupyter notebook containing the full analysis: data download, return calculation, simulation, plots and risk metrics.
requirements.txt — Python dependencies required to run the notebook.

(Rename the files above to match the actual filenames in this repo.)

Setup
bash
pip install numpy pandas yfinance matplotlib scipy

Run the notebook top to bottom; it downloads its own data via yfinance, so no external files are required.
