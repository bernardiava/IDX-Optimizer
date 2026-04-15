# IDX Portfolio Optimizer & Forecast System - User Guide

## 📋 Table of Contents
1. [Overview](#overview)
2. [How to Use the Optimizer](#how-to-use-the-optimizer)
3. [Understanding Investment Horizon](#understanding-investment-horizon)
4. [Understanding Forecasts](#understanding-forecasts)
5. [Reading the Charts & Graphs](#reading-the-charts--graphs)
6. [Portfolio Forecast Feature](#portfolio-forecast-feature)
7. [FAQ & Troubleshooting](#faq--troubleshooting)

---

## Overview

This application is a **single-page HTML tool** that helps you:
- **Select stocks** from the LQ45 index (Indonesia's 45 most liquid stocks)
- **Optimize portfolio weights** using Modern Portfolio Theory (MPT)
- **Forecast individual stock prices** using ARIMA + GARCH ensemble models
- **Visualize** efficient frontiers, correlations, and allocations
- **Export** results to PDF or CSV

**No installation required** - just open `index_diff.html` in any modern browser (Chrome, Firefox, Edge).

---

## How to Use the Optimizer

### Step 1: Select Your Stocks
1. Click on the **"Optimizer"** tab (default view)
2. You'll see a list of LQ45 stocks with checkboxes
3. **Select 3-10 stocks** for optimal diversification
   - Too few stocks (< 3): Poor diversification
   - Too many stocks (> 15): Over-diversification, harder to manage
4. Click **"Load Data & Optimize"** to fetch historical prices and run optimization

### Step 2: Choose Optimization Strategy
Four strategies are available:

| Strategy | Best For | Description |
|----------|----------|-------------|
| **Max Sharpe** | Balanced growth | Maximizes risk-adjusted returns (return per unit of risk) |
| **Min Volatility** | Conservative investors | Minimizes overall portfolio volatility |
| **Risk Parity** | Risk-balanced approach | Equalizes risk contribution from each stock |
| **Equal Weight** | Simple diversification | Each stock gets equal weight (1/n) |

### Step 3: Set Your Investment Profile
- **Conservative**: Lower risk tolerance, prefer stable returns
- **Moderate**: Balanced risk-return trade-off
- **Aggressive**: Higher risk tolerance, seek maximum returns

### Step 4: Review Results
After optimization, you'll see:
- **Allocation Donut Chart**: Visual breakdown of portfolio weights
- **Correlation Heatmap**: How stocks move together (darker = higher correlation)
- **Efficient Frontier**: Risk-return trade-off curve with your portfolio marked
- **Performance Metrics**: Expected return, volatility, max drawdown, VaR, CVaR
- **AI Commentary**: Automated analysis of your portfolio and individual stocks

### Step 5: Adjust & Export
- **Manually adjust weights** using sliders if needed
- **Export to PDF** for reports
- **Export to CSV** for further analysis in Excel

---

## Understanding Investment Horizon

### What is Investment Horizon?
**Investment horizon** is the length of time you plan to hold your investment before selling. It's a critical factor in both optimization and forecasting.

### Horizon Options in This Tool

| Horizon | Trading Days | Time Period | Best For |
|---------|--------------|-------------|----------|
| **1 Week** | 5 days | Short-term trading | Tactical adjustments, momentum plays |
| **1 Month** | 22 days | Monthly rebalancing | Swing trading, tactical allocation |
| **3 Months** | 66 days | Quarterly review | Strategic allocation, earnings cycles |
| **1 Year** | 252 days | Long-term investing | Strategic portfolio, retirement planning |

### Why Horizon Matters

#### For Optimization:
- **Shorter horizons** (1 week - 1 month): Focus on recent momentum and volatility
- **Longer horizons** (3 months - 1 year): Emphasize fundamental stability and long-term trends
- The optimizer uses **annualized metrics** but adjusts confidence intervals based on your horizon

#### For Forecasting:
- **Short horizons**: More accurate predictions, narrower confidence intervals
- **Long horizons**: Less certain, wider confidence intervals (uncertainty grows with √time)
- Example: A 1-week forecast might have ±5% confidence interval, while 1-year could be ±30%

### How to Choose Your Horizon
Ask yourself:
1. **When will I need this money?**
   - < 1 month: Use 1-week or 1-month horizon
   - 1-6 months: Use 3-month horizon
   - > 6 months: Use 1-year horizon

2. **What's my trading style?**
   - Day trader: 1 week
   - Swing trader: 1 month
   - Position trader: 3 months
   - Buy-and-hold: 1 year

3. **What's the market condition?**
   - High volatility/crisis: Shorter horizons (more uncertainty)
   - Stable market: Longer horizons (more predictable)

---

## Understanding Forecasts

### What is Forecasting?
Forecasting predicts **future stock prices** based on historical patterns using statistical models.

### The Ensemble Model
This tool uses **two models combined** (ensemble):

#### 1. ARIMA (AutoRegressive Integrated Moving Average)
- **Purpose**: Predicts price direction and trend
- **How it works**: Uses past returns to predict future returns
- **Strength**: Captures momentum and mean-reversion patterns
- **Limitation**: Assumes linear relationships

#### 2. GARCH (Generalized AutoRegressive Conditional Heteroskedasticity)
- **Purpose**: Predicts volatility (risk)
- **How it works**: Models how volatility clusters over time
- **Strength**: Identifies high/low volatility regimes
- **Output**: Classifies volatility as Low, Medium, High, or Crisis

### Forecast Outputs Explained

When you view the **Forecasts** tab, each stock shows:

#### 1. **Price Chart with Confidence Intervals**
- **Blue line**: Forecasted price path
- **Gray line**: Historical prices
- **Green dotted area**: 95% confidence interval
  - There's a 95% probability the actual price will stay within this range
  - Wider area = more uncertainty

#### 2. **Predicted Return (%)**
- Expected percentage change over your chosen horizon
- **Positive**: Stock expected to rise
- **Negative**: Stock expected to fall
- Example: "+5.234%" over 1 month means the model expects a 5.234% gain

#### 3. **Volatility Regime**
- **Low**: Calm market, predictable movements
- **Medium**: Normal market conditions
- **High**: Elevated uncertainty, larger price swings
- **Crisis**: Extreme volatility, avoid new positions

#### 4. **P(Positive Return)**
- Probability that the stock will end higher than today
- **> 60%**: Bullish signal
- **40-60%**: Neutral/uncertain
- **< 40%**: Bearish signal

#### 5. **Signal (Bullish/Neutral/Bearish)**
- **🟢 Bullish**: Strong buy signal (predicted return > 5%, low/medium volatility)
- **🟡 Neutral**: Hold/wait (mixed signals or moderate returns)
- **🔴 Bearish**: Sell/avoid (negative returns or crisis volatility)

### How to Use Forecasts

#### For Stock Selection:
1. Go to **Forecasts** tab
2. Look for **🟢 Bullish** signals with **high P(Positive Return)**
3. Avoid **🔴 Bearish** stocks unless you're hedging
4. Check **volatility regime** - avoid "Crisis" stocks for conservative portfolios

#### For Portfolio Construction:
- Combine forecasts with optimization:
  - Use **bullish stocks** as core holdings
  - Use **neutral stocks** for diversification
  - Limit or exclude **bearish stocks**

#### For Timing:
- **Short horizon forecasts** (1 week): Use for entry/exit timing
- **Long horizon forecasts** (1 year): Use for strategic allocation

---

## Reading the Charts & Graphs

### 1. Allocation Donut Chart
**Location**: Optimizer tab, top section

**What it shows**: Portfolio weight distribution

**How to read**:
- Each slice = one stock
- Slice size = percentage of portfolio
- Colors match stock tickers in the table below
- **Ideal**: Diversified across 5-10 stocks, no single stock > 30%

**Action**: If one slice is too large, consider manual rebalancing

---

### 2. Correlation Heatmap
**Location**: Optimizer tab, middle section

**What it shows**: How stocks move together (correlation matrix)

**How to read**:
- **Dark red (close to +1)**: Stocks move together strongly (bad for diversification)
- **White/gray (close to 0)**: No relationship
- **Dark blue (close to -1)**: Stocks move oppositely (excellent for diversification)
- Diagonal is always dark red (stock correlated with itself)

**Action**: 
- Avoid portfolios with many dark red pairs
- Seek stocks with low or negative correlations
- Example: If BBCA and BBRI are highly correlated, holding both adds less diversification

---

### 3. Efficient Frontier
**Location**: Optimizer tab, bottom section

**What it shows**: Risk-return trade-off for all possible portfolios

**How to read**:
- **X-axis**: Volatility (risk) - lower is better
- **Y-axis**: Expected return - higher is better
- **Curved line**: Efficient frontier (best possible portfolios)
- **Yellow star**: Your selected portfolio
- **Gray dots**: Sub-optimal portfolios

**Key insights**:
- Portfolios **on the curve**: Efficient (best return for given risk)
- Portfolios **below the curve**: Inefficient (could get better return for same risk)
- **Top-left**: Ideal (high return, low risk) - rarely exists
- **Bottom-right**: Worst (low return, high risk)

**Action**: 
- If your star is far from the curve, try a different strategy
- Max Sharpe should be near the "steepest" part of the curve
- Min Vol should be at the leftmost point

---

### 4. Individual Stock Forecast Chart
**Location**: Forecasts tab, each stock card

**What it shows**: Historical and predicted price path

**How to read**:
- **Gray line (left)**: Actual historical prices
- **Blue line (right)**: Forecasted future prices
- **Green dotted lines**: 95% confidence interval bounds
- **Shaded green area**: Range where price is 95% likely to stay

**Key patterns**:
- **Upward sloping blue line**: Bullish forecast
- **Downward sloping blue line**: Bearish forecast
- **Wide green area**: High uncertainty (high volatility)
- **Narrow green area**: Low uncertainty (stable forecast)

**Action**:
- Prefer stocks with upward slope + narrow confidence interval
- Be cautious with wide confidence intervals (unpredictable)

---

## Portfolio Forecast Feature

### Current Limitation
⚠️ **Important**: The current version only shows **individual stock forecasts**, not a combined portfolio forecast.

### What's Missing
You correctly identified that the forecast should include:
1. **Portfolio-level forecast**: Combined expected return based on optimized weights
2. **Portfolio confidence intervals**: Aggregated risk across all holdings
3. **Portfolio price path**: How the entire portfolio is expected to evolve

### Workaround (Current Version)
Until this feature is added, you can estimate portfolio forecast manually:

#### Step 1: Calculate Weighted Return
```
Portfolio Expected Return = Σ (Weight_i × Return_i)
```
Example:
- BBCA: 30% weight, +5% forecast → 0.30 × 5% = 1.5%
- TLKM: 25% weight, +3% forecast → 0.25 × 3% = 0.75%
- ASII: 25% weight, +2% forecast → 0.25 × 2% = 0.5%
- UNVR: 20% weight, +4% forecast → 0.20 × 4% = 0.8%
- **Portfolio Return** = 1.5% + 0.75% + 0.5% + 0.8% = **3.55%**

#### Step 2: Estimate Portfolio Volatility
Use the **volatility metric** shown in the Optimizer results (accounts for diversification benefits).

#### Step 3: Assess Overall Signal
- Count bullish vs bearish stocks in your portfolio
- If > 70% are bullish → Portfolio signal: Bullish
- If > 70% are bearish → Portfolio signal: Bearish
- Mixed → Portfolio signal: Neutral

### Future Enhancement (Recommended)
The tool should be updated to include:
1. **Portfolio Forecast Card**: Summary card showing aggregated forecast
2. **Portfolio Price Chart**: Combined historical and forecasted portfolio value
3. **Scenario Analysis**: Best-case, base-case, worst-case portfolio outcomes

---

## FAQ & Troubleshooting

### Q: Why don't I see any charts?
**A**: 
- Ensure you have an internet connection (charts use Plotly CDN)
- Wait 2-3 seconds after clicking "Load Data & Optimize"
- Try refreshing the page
- Check browser console for errors (F12)

### Q: The data isn't loading / I get an error
**A**:
- Yahoo Finance API may be temporarily unavailable
- Check if stock tickers are correct (e.g., "BBCA.JK" for Jakarta Stock Exchange)
- Try selecting fewer stocks
- Wait a few minutes and retry

### Q: What does "NaN" or "Infinity" mean in results?
**A**:
- Insufficient data (selected stocks need at least 1 year of price history)
- Highly correlated stocks causing matrix calculation issues
- Solution: Remove problematic stocks or choose different combination

### Q: Why are some forecast confidence intervals very wide?
**A**:
- High historical volatility (e.g., small-cap stocks, crisis periods)
- Long forecast horizon (1 year has more uncertainty than 1 week)
- This is normal - the model is honestly reporting uncertainty

### Q: Can I use this for non-LQ45 stocks?
**A**:
- Currently hardcoded for LQ45 tickers
- To add other stocks: Edit the `LQ45_STOCKS` array in the JavaScript code
- Format: `{ ticker: "STOCK.JK", name: "Company Name", sector: "Sector" }`

### Q: How often should I rebalance?
**A**:
- Depends on your horizon:
  - 1 week horizon: Rebalance weekly
  - 1 month horizon: Rebalance monthly
  - 3+ months horizon: Rebalance quarterly
- Also rebalance when:
  - Any stock weight drifts > 5% from target
  - Major market events occur
  - Forecast signals change significantly

### Q: Is this financial advice?
**A**: 
- **NO**. This is a quantitative analysis tool for educational purposes
- Always do your own research
- Past performance doesn't guarantee future results
- Consult a licensed financial advisor for personalized advice

### Q: Can I use this offline?
**A**:
- Partially. The HTML file works offline, but:
  - Data loading requires internet (Yahoo Finance API)
  - Chart rendering requires internet (Plotly CDN)
- For full offline use: Download Plotly.js and jStat.js locally

---

## Quick Start Checklist

✅ **First Time Setup**:
1. Open `index_diff.html` in Chrome/Firefox/Edge
2. Select language (EN/ID)
3. Choose 5-7 stocks from different sectors
4. Set investment profile (Conservative/Moderate/Aggressive)
5. Select optimization strategy (start with "Max Sharpe")
6. Click "Load Data & Optimize"
7. Review charts and metrics
8. Read AI commentary for insights
9. Export to PDF if satisfied

✅ **Regular Use**:
1. Check **Forecasts** tab for updated signals
2. Re-run optimization if market conditions changed
3. Adjust weights manually if needed
4. Export updated portfolio report

---

## Technical Details (For Advanced Users)

### Data Source
- **Yahoo Finance API**: Daily adjusted close prices
- **Lookback period**: ~2 years of historical data
- **Update frequency**: Real-time (market hours), daily close

### Optimization Algorithm
- **Mean-Variance Optimization**: Markowitz Modern Portfolio Theory
- **Constraints**: 
  - Weights sum to 100%
  - No short selling (weights ≥ 0)
  - Maximum single stock weight: 40% (configurable)
- **Solver**: Numerical optimization using gradient descent

### Forecasting Models
- **ARIMA(1,0,0)**: AR(1) process for returns
- **GARCH(1,1)**: Volatility clustering model
- **Ensemble**: Equal-weighted combination
- **Confidence Intervals**: Based on forecast error variance

### Risk Metrics
- **Volatility**: Annualized standard deviation of returns
- **Max Drawdown**: Largest peak-to-trough decline
- **VaR (95%)**: Value at Risk - worst 5% daily loss
- **CVaR (95%)**: Conditional VaR - average of worst 5% losses

---

## Support & Feedback

If you encounter bugs or have feature requests:
1. Check browser console for errors (F12 → Console tab)
2. Note steps to reproduce the issue
3. Screenshot the problem if possible

**Planned Improvements**:
- [ ] Portfolio-level forecasting
- [ ] Backtesting module
- [ ] Custom stock upload
- [ ] Dividend yield integration
- [ ] Multi-currency support
- [ ] Monte Carlo simulation

---

**Last Updated**: December 2025  
**Version**: 1.0  
**License**: MIT (see LICENSE file)