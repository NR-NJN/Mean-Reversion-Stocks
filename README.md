# Mean-Reversion-Stocks
Mean reversion, or reversion to the mean, is a theory used in finance that suggests that asset price volatility and historical returns eventually will revert to the long-run mean or average level of the entire dataset.<br/>
Reversion to the mean involves retracing a condition back to its long-run average state. The concept assumes that a level that strays far from the long-term norm or trend will again return, reverting to its understood state or secular trend.<br/>


## My implementation
I have used the C# SDK for Alpaca’s paper trading API to run a neat mean reversion algrorithm <br/>
To connect to the API, create a new REST client, giving it the keys and the API URL. Using the REST client, we check Alpaca’s clock and calendar API endpoints to figure out when the market will open and when we’re getting too near to close.

## Logic
It looks at data for one symbol — set here to SPY, as an example — and each minute, it checks on its current price and its average price over the last 20 minutes. If the current price is higher than the average, it doesn’t want to hold any position. However, if the current price is lower than average, it wants to allocate a certain percentage of your portfolio to holding shares. It’s following the economic theory of mean reversion, assuming that when the price is below the average, it’s more likely to come back up.<br/>
The “scale” variable at the top determines how much of your portfolio goes into the position.</br>
```
Decimal avg = bars.Average(item => item.Close);         
       Decimal currentPrice = bars.Last().Close;
Decimal diff = avg - currentPrice;

Decimal portfolioShare = diff / currentPrice * scale;
```
