# Mean Reversion Trading Strategy

## Overview

This project implements a systematic **mean reversion trading strategy** based on statistical deviation from short-term equilibrium levels.

The objective is to:

- Identify overextended price movements
- Construct contrarian signals
- Backtest reversion dynamics
- Evaluate profitability under realistic trading assumptions
- Analyze risk characteristics of reversion-based strategies

Mean reversion assumes that prices fluctuate around a local equilibrium and tend to revert after extreme deviations.

---

## Strategy Intuition

If price moves significantly above its recent average:

→ It may be overbought  
→ Expect downward correction  

If price moves significantly below its recent average:

→ It may be oversold  
→ Expect upward correction  

The strategy systematically exploits these temporary dislocations.

---

## Signal Construction

### Rolling Mean

Let:

price_t = asset price at time t  
MA_t = rolling moving average  

MA_t = average of price over last N periods

---

### Deviation from Mean

Deviation_t = price_t - MA_t

To normalize across volatility regimes:

Z_t = (price_t - MA_t) / rolling_std

Where:

rolling_std = rolling standard deviation over same window

---

## Trading Rule

If Z_t > threshold:

→ Open short position

If Z_t < -threshold:

→ Open long position

Otherwise:

→ No position

Positions are typically scaled or capped to control leverage.

---

## Portfolio Return Calculation

Portfolio return at time t:

R_portfolio_t = weight_t-1 * return_t

Return_t = (price_t - price_t-1) / price_t-1

Signal is shifted forward to avoid look-ahead bias.

---

## Risk Management

Possible controls include:

- Maximum holding period
- Stop-loss level
- Volatility filter
- Position size normalization

Volatility-adjusted position sizing:

weight_t = target_risk / rolling_volatility

---

## Backtesting Framework

The backtest includes:

- Rolling signal generation
- Position lagging
- Transaction cost deduction
- Cumulative NAV tracking
- Performance metric computation

Transaction-adjusted return:

R_net_t = R_gross_t - cost_per_trade * turnover_t

Turnover_t = absolute(weight_t - weight_t-1)

---

## Performance Metrics

Annualized Return:

Annual_Return = mean(daily_returns) * 252

Annualized Volatility:

Annual_Volatility = std(daily_returns) * sqrt(252)

Sharpe Ratio:

Sharpe = Annual_Return / Annual_Volatility

Maximum Drawdown:

Drawdown_t = (Peak_NAV - NAV_t) / Peak_NAV

---

## Statistical Interpretation

Mean reversion can be interpreted as:

1. Short-term liquidity imbalance  
2. Temporary order-flow pressure  
3. Behavioral overreaction  
4. Ornstein-Uhlenbeck type dynamics  

Continuous-time analogue:

dX_t = kappa * (mu - X_t) dt + sigma dW_t

Where:

kappa = speed of reversion  
mu = long-run mean  
sigma = volatility  

---

## Extensions

The strategy can be extended to:

- Cross-sectional mean reversion
- Pair trading (cointegration-based)
- Kalman filter equilibrium estimation
- Regime-dependent thresholds
- Machine learning residual modeling

---

## Applications

Mean reversion strategies are commonly used in:

- Statistical arbitrage
- Market-making
- Intraday trading systems
- Relative value hedge funds

---

## Disclaimer

This project is for research and educational purposes only.  
It does not constitute investment advice.
