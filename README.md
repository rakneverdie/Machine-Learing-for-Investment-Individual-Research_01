**Machine Learning for Trading and Portfolio Optimization using LSTM and Quantitative Methods**
**Rak Kantarak**
*Individual Interested Research*
**1. Introduction**
This project explores how modern machine learning can be combined with classical portfolio theory to support investment decisions. I build a simple Long–Short trading pipeline where an LSTM forecasts next-period prices using only two inputs price and RSI and then convert those forecasts into trading signals under explicit transaction costs (10 bps, i.e., 0.10%). Signals are backtested with next-bar execution on 4-hour data (annualization factor ≈ 1,560) across a small cross-asset universe (e.g., XAUUSD, XAGUSD, BRN1!, S501!, selected SET names) sourced via TradingView’s tvDatafeed.
On top of the single-asset backtests, I apply portfolio analytics in two ways: (i)               a mean–variance layer to compute the efficient frontier and tangent (max-Sharpe) portfolio under bounds, and (ii) a simple HJB/Merton-style dynamic allocation that updates weights using exponentially weighted estimates of means and covariances. Hyperparameters of the LSTM (sequence length, hidden size, layers, dropout, learning rate, thresholds) are tuned with Optuna against a risk-aware objective (profit minus a penalty on drawdown).
This is a personal research project built to learn about data handling, trading mechanics, and quantitative finance. It is not investment advice and not work-related. Any proprietary components are excluded; the code runs on publicly available market data only.

**2. Method**
Steps I used in this project:
1.	Data – I collected price data from gold, silver, oil, wheat, and Thai stocks.
2.	Features – I used price and RSI (Relative Strength Index).
3.	Model – I trained an LSTM model with PyTorch.
4.	Optimization – I used Optuna to find the best hyperparameters.
5.	Signals – Predictions are changed into buy/sell/hold signals.
6.	Back test – I tested with transaction cost and next-bar execution.
7.	Portfolio – I compared Tangent Portfolio (MPT) with Dynamic Portfolio (HJB).
8.	Metrics – I measured return %, drawdown %, volatility, and win rate.





**3. Results** (Work in Progress) This project is still ongoing research.
Early experiments show that:
•	The LSTM can collect data and run multiple trials of hyperparameter optimization for each asset, under the constraint of high average profit, low average loss, and high win rate.
•	The LSTM + RSI model can generate trading signals, with some periods showing profit even after transaction costs.
•	The Dynamic Portfolio (HJB) appears to give smoother equity growth compared to the Tangent Portfolio.
More testing is in progress, and the models will be refined further.

**4. Discussion**
Good points:
•	End-to-end process (data -> model -> signals -> backtest -> portfolio).
•	Mix of AI and finance methods.
•	Include transaction cost for more realistic test.

**Methodology Diagram**

<img width="705" height="1254" alt="image" src="https://github.com/user-attachments/assets/7524bd07-f569-449a-bd31-034cca705f37" />



















 






**Figure**
<img width="975" height="328" alt="image" src="https://github.com/user-attachments/assets/1b5912fe-ff8e-4ef4-a8de-d0efad4ce581" />
**Figure 1.** Example of fetching historical market data using tvDatafeed. 
Assets include gold (XAUUSD), silver (XAGUSD), wheat futures (ZW1!), Thai stock (AOT), Brent oil futures (BRN1!), and SET50 index futures (S501!).


<img width="975" height="321" alt="image" src="https://github.com/user-attachments/assets/e32267be-e1d4-4977-a688-d9e213851191" />
**Figure 2.** Example of Optuna hyperparameter tuning log. 
Each line shows the trial number, objective value, and selected parameters. In this project, tuning was used to search for the best sequence length, hidden size, number of layers, dropout rate, learning rate, and epochs to optimize model performance.


<img width="975" height="196" alt="image" src="https://github.com/user-attachments/assets/4ee22b54-cb7f-4152-b17e-d6adbebb231d" />
**Figure 3.** Best Trial from Hyperparameter Tuning (Optuna)
The output shows the best hyperparameters found during Optuna tuning for the LSTM model. Parameters such as sequence length, hidden layer size, number of layers, dropout, learning rate, and thresholds are optimized. The best configuration achieved a profit               of +2.65% with low drawdown (−0.29%).


 <img width="975" height="182" alt="image" src="https://github.com/user-attachments/assets/1f2d496b-da5d-4186-b34c-4232492b0813" />
**Figure 4.** Training Log for XAUUSD (Gold)
The log displays the training process of the LSTM model on XAUUSD with the best parameters from tuning. The model runs for 610 epochs, and the training loss converges around 0.036, showing stable learning of price dynamics.


 <img width="975" height="245" alt="image" src="https://github.com/user-attachments/assets/68cc2ca5-aee4-42b6-b041-32c072e2de86" />
**Figure 5.** Example of trading simulation with machine learning (XAGUSD). 
The top panel shows trading signals: green markers indicate long entries and red markers indicate short entries.
The dashed line represents the predicted next-step price.
The bottom panel shows the equity curve, starting from the initial investment balance.


 <img width="975" height="234" alt="image" src="https://github.com/user-attachments/assets/87b3c173-0363-49bc-8f41-cd0462048fae" />
**Figure 6.** Portfolio Value by Ticker
This chart shows how the portfolio value changes over time for each asset: XAUUSD (gold), XAGUSD (silver), ZW1! (wheat), AOT, BRN1! (brent), and S501! (SET50 futures). The solid lines represent individual asset portfolios, while the dashed cyan line shows the expected (average) portfolio. Some assets, like ZW1! and S501!, perform steadily, while others such as AOT show a significant drop. This figure helps compare risk and return behavior across different assets.



<img width="975" height="211" alt="image" src="https://github.com/user-attachments/assets/a34f5acf-2c83-4a3c-9e68-690504038b40" />
 **Figure 7.** Performance Summary Table
This table reports the backtesting results of each asset. It shows portfolio value, profit/loss (cash and percentage), win rate, average profit/loss, maximum drawdown, volatility (σ), and number of trades. For example, wheat futures (ZW1!) produced a +4.52% return with 100% win rate, while AOT experienced a -24.30% loss with large drawdown.


 <img width="975" height="244" alt="image" src="https://github.com/user-attachments/assets/4262e451-9420-4908-a0fa-d6c8e4743c26" />
**Figure 8.** Return vs Sigma with Tangent Line
The scatter plot shows the relationship between return (%) and volatility (σ) for individual assets. A polynomial fit (red curve) represents the general trend, while the tangent line (cyan) indicates the optimal trade-off between risk and return. The tangent point (purple X) highlights the portfolio with the highest Sharpe ratio.





 
<img width="975" height="238" alt="image" src="https://github.com/user-attachments/assets/a814fc77-ec76-4ab0-ba97-c3638545b7a4" />
<img width="545" height="105" alt="image" src="https://github.com/user-attachments/assets/569bcb30-2ba2-4e49-87f1-eb21c946a118" />
**Figure 9.** Efficient Frontier: MPT vs MDP (HJB)
This figure compares Modern Portfolio Theory (MPT) with the Merton Dynamic Portfolio (MDP/HJB). The red curve shows the efficient frontier from static portfolios, while the dashed cyan line represents the Capital Market Line (CML). The tangent portfolio (purple star) and the MDP/HJB solution (blue dot) illustrate different approaches to achieving optimal portfolios.
