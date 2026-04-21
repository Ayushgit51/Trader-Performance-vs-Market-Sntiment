# Trader Sentiment & Performance Analysis

This project analyzes the relationship between market sentiment (Fear & Greed Index) and personal trading performance to identify behavioral patterns and predict future profitability.

## 1. Setup & Installation
1. **Requirements**: Python 3.8+, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`.
2. **Data Files**: Ensure `historical_data.csv` and `fear_greed_index.csv` are in the root directory.
3. **Run**: Execute the Jupyter Notebook cells sequentially.

## 2. Methodology
- **Data Alignment**: Merged intraday trading logs with daily sentiment indices using date normalization.
- **Behavioral Metrics**: Engineered features such as 3-day rolling PnL and trade density to capture "trader state of mind."
- **Predictive Modeling**: Utilized a Random Forest Classifier with a time-series shift (t+1) to predict next-day profitability buckets.

## 3. Key Insights & Output
### Performance by Sentiment
| classification   |              sum |   mean |   count |
|:-----------------|-----------------:|-------:|--------:|
| Extreme Fear     | 739110           |  71.03 |   10406 |
| Extreme Greed    |      2.71517e+06 | 130.21 |   20853 |
| Fear             |      3.35716e+06 | 112.63 |   29808 |
| Greed            |      2.15013e+06 |  85.4  |   25176 |
| Neutral          |      1.29292e+06 |  71.2  |   18159 |

- **Sentiment Correlation**: The model identified `avg_size` as the strongest predictor of next-day performance.
- **Behavioral Bias**: Trades executed during 'Extreme Fear' show a higher variance in PnL, indicating emotional volatility.

## 4. Strategy Recommendations
- **Dynamic Sizing**: Reduce position sizes by 30% when the Fear & Greed index is below 20 (Extreme Fear) to mitigate volatility.
- **Cool-off Periods**: The high importance of `daily_pnl` on future outcomes suggests a "streak" effect. Stop trading for 24 hours after a 3-standard-deviation loss.
- **Sentiment Hedging**: If `sentiment_value` is the primary driver, pivot strategy from Trend-Following to Mean-Reversion during 'Neutral' phases.
