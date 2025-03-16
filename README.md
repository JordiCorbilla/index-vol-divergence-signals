# Index Vol Divergence Signals

This repository provides a **volatility-based trading strategy** for the S&P 500 (SPY) using the CBOE Volatility Index (VIX). The idea is to detect potential turning points (entries) based on **“second lower lows” in SPY accompanied by rising VIX**, while ensuring SPY is trading within ±2 standard deviations of its 30-day moving average.

## How It Works

1. **Data Fetching**  
   - Uses `yfinance` to download historical price data for SPY and VIX.

2. **Signal Detection**  
   - Computes a 30-day moving average (MA) and 2σ Bollinger bands.  
   - Looks for **local minima** in SPY.  
   - Confirms a “second lower low” compared to the first local minimum.  
   - Checks if VIX is **higher** at the second low than at the first low.  
   - Confirms SPY is still **within** its ±2σ Bollinger bands.

3. **Exit Strategy**  
   - Once an entry signal is triggered, the position is exited when either:
     1. SPY closes **above** its 30-day MA, or  
     2. SPY closes **below** its lower Bollinger band.

4. **Performance Calculation**  
   - Each entry/exit pair’s returns are calculated and aggregated to get the total return.

5. **Plotting**  
   - Generates a chart showing SPY price, the Bollinger bands, and entry/exit signals.  
   - Also plots the **RiskOptima** version stamp at the bottom for easy reference.

## Example Usage

```python
from riskoptima import RiskOptima

ANALYSIS_START_DATE = RiskOptima.get_previous_year_date(RiskOptima.get_previous_working_day(), 1)
ANALYSIS_END_DATE   = RiskOptima.get_previous_working_day()

df_signals, df_exits, returns = RiskOptima.run_index_vol_divergence_signals(start_date=ANALYSIS_START_DATE, 
                                                                            end_date=ANALYSIS_END_DATE)

### Support me

<a href="https://www.buymeacoffee.com/jordicorbilla" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/default-orange.png" alt="Buy Me A Coffee" height="41" width="174"></a>
