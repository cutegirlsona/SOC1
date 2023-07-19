# SOC Practice

### Indicator

##### 1. EMA 21 and SMA 21
![ASHOKLEY_2023-07-19_15-34-00](https://github.com/cutegirlsona/SOC1/assets/134861429/893dcada-8af8-4766-9401-f2afb810237a)

##### 2. MACD indicator ((14,21), (41,90), (90,200)
![BTCUSD_2023-07-18_22-41-11](https://github.com/cutegirlsona/SOC1/assets/134861429/d2d5b0bc-e19e-454f-9cf7-c1012d4ced89)

##### 3. Bollinger Band
![BTCUSD_2023-07-18_22-43-59](https://github.com/cutegirlsona/SOC1/assets/134861429/9733c930-02f5-43d3-b709-f399b334a00d)

### Strategy/Signal

##### 1. Dead Cross Over Strategy (golden cross and death cross)

```
strategy("death cross and golden cross", overlay=true)

float fastsma=ta.sma(close, 50)
float slowsma=ta.sma(close, 200)

switch
    ta.crossover(fastsma, slowsma) => strategy.entry("buy", strategy.long)
    ta.crossunder(fastsma, slowsma) => strategy.entry("sell", strategy.short )

plot(fastsma)
plot(slowsma)
```
![BTCUSD_2023-07-18_23-24-36](https://github.com/cutegirlsona/SOC1/assets/134861429/5eb6a35a-12fe-43c1-9cfa-4e3ec02a686f)


##### 2. Doji Signal

![BTCUSD_2023-07-18_23-34-32](https://github.com/cutegirlsona/SOC1/assets/134861429/440100b6-7750-44ea-a5f9-9d22462a8724)


##### 3. Inside candle signal

```
indicator("Inside Candle Signal", overlay=true)

inside_candle = high < high[1] and low > low[1]

plotshape(inside_candle, title="Inside Candle", style=shape.triangleup, location=location.belowbar, size=size.small)
```
![ASHOKLEY_2023-07-19_15-29-35](https://github.com/cutegirlsona/SOC1/assets/134861429/070e0037-f056-4e3c-bc2e-601ea44649a5)


##### 4. Alert the terminal when the condition is true

```
indicator("alertconditionexample", overlay=true)
alertcondition(close < open)
```
![NIFTY_2023-07-19_13-03-59](https://github.com/cutegirlsona/SOC1/assets/134861429/7e877e70-9708-4ef3-92ce-453319fe82d8)

##### 5. Intraday: Long the stock if open “Gap Up” and Short If “Gap Down”

```
strategy("Gap Up/Down Strategy", overlay=true)

switch
    open>close[1] => strategy.entry("long", strategy.long)
    open<close[1] => strategy.entry("short", strategy.short)
```
![ASHOKLEY_2023-07-19_15-18-09](https://github.com/cutegirlsona/SOC1/assets/134861429/d032bb6b-43c0-4b57-9a1f-110afb41b799)

##### 6. Swing Trade: Len = 14,21,60,90,120, Factor = 1.1, 1.03,1.06  ..  Price <  { Len } day Max price  and Price > Min Price{len}* Factor  AND volume is increasing or volume > avg volume(10 or 20 or 7 ) {Long the stock and share results} {mid cap / Nifty 50 }


##### 7. 5 EMA strategy

```
strategy("5 EMA", overlay=true)

emaline=ta.ema(close,5)
plot(emaline)

alert_candle = low>emaline or high<emaline
plotshape(alert_candle, title="Alert Candle", style=shape.triangleup, location=location.belowbar, size=size.small)

longg = high>=emaline
shortt = low<=emaline

switch 
    high[1] < emaline and longg==true => strategy.entry("Long", strategy.long)
    low[1] > emaline and shortt==true => strategy.entry("Short", strategy.short)
```
![NIFTY_2023-07-19_18-34-37](https://github.com/cutegirlsona/SOC1/assets/134861429/58ae8ec2-5ec2-4d98-a4b4-9ee86d6a7bb5)


##### 8. Inside Candle Strategy

```
strategy("insidecandle", overlay=true)

switch
    high<high[1] and low>low[1] and close>open => strategy.entry("long", strategy.long)
    high<high[1] and low>low[1] and close<open => strategy.entry("short", strategy.short)
```
![NIFTY_2023-07-18_23-50-10](https://github.com/cutegirlsona/SOC1/assets/134861429/acc2f872-baf0-4cf2-aa03-57bc32662113)


##### 9. Bollinger Band Strategy

```
strategy("Bollinger Bands Strategy", overlay=true)

basis = ta.sma(close, 20)
dev = 2 * ta.stdev(close, 20)

upper = basis + dev
lower = basis - dev

offset = input.int(0, "Offset", minval = -500, maxval = 500)
plot(basis, "Basis", color=#FF6D00, offset = offset)
p1 = plot(upper, "Upper", color=#2962FF, offset = offset)
p2 = plot(lower, "Lower", color=#2962FF, offset = offset)
fill(p1, p2, title = "Background", color=color.rgb(33, 150, 243, 95))


buyEntry = ta.crossover(close, lower)
sellEntry = ta.crossunder(close, upper)

if buyEntry
	strategy.entry("Long", strategy.long, stop=lower, oca_name="BollingerBands", oca_type=strategy.oca.cancel)
else
	strategy.cancel(id="Long")

if sellEntry
	strategy.entry("Short", strategy.short, stop=upper, oca_name="BollingerBands", oca_type=strategy.oca.cancel)
else
	strategy.cancel(id="Short")

```

![TSLA_2023-07-19_19-31-03](https://github.com/cutegirlsona/SOC1/assets/134861429/d63ed0c0-eed8-47ac-8097-42d23e4adce7)



##### 10. Monthly Candle strategy




# Self-developed strategies


