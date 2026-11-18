# UK electricity gap forecast (Excel)

Will UK electricity consumption overtake electricity supply before 2040? And if not, how much would supply growth have to slow down for that to happen?

This started as a university group project. I rebuilt the analysis on my own in Excel afterwards, using the latest official data.

## Data

The data is from the government's Digest of UK Energy Statistics (DUKES), table "Electricity since 1920". I used electricity supplied (net) and total electricity consumed, in TWh, from 1965 to 2025. It's published under the Open Government Licence v3.0.

The figures change basis in 1986/87. Before that they only cover the major power producers, and from 1987 they cover all generating companies. This is explained on the Data tab.

## Method

1. Fit straight line trends (least squares) to supply and consumption, using 1965 to 2022 for the main result.
2. Extend the consumption trend to 2040.
3. Restart supply from its trend value in 2021, then work out the yearly supply growth that would only just meet demand in 2040.
4. Compare that with the fitted supply growth to get the slowdown needed for demand to catch up.
5. Test slowdowns from 0% to 40% on the Sensitivity tab.
6. I also tried cubic fits to compare, but they go negative before 2040, so I didn't use them.

Everything is done with formulas, so changing the fit end year on the Model tab updates the rest of the spreadsheet.

## Results

![Supplied and consumed with straight line trends to 2040](trends.png)

On the 1965 to 2022 trends, consumption reaches about 408 TWh in 2040. Supply stays ahead, and the two trend lines don't cross until around 2275, because their slopes are almost the same.

![Surplus or shortfall in 2040 for different supply growth slowdowns](sensitivity.png)

Supply growth would have to slow by about 26% from 2021 onwards for demand to overtake supply before 2040. Anything less than that still leaves a surplus.

| Fit years | Consumption trend (TWh per year) | Supply trend (TWh per year) | Slowdown needed |
|---|---|---|---|
| 1965 to 2022 (original project) | 2.82 | 2.76 | 26.1% |
| 1965 to 2025 (latest data) | 2.43 | 2.30 | 22.3% |

Adding the last three years of data lowers the slowdown needed to about 22%. Both trends flatten, but supply flattens more. On the 1965 to 2025 trends the lines cross around 2115 instead of 2275.

I kept the restart year at 2021 for both fits, so the only thing that changes between them is the trend. If each fit restarts supply from its own last year instead (2022 and 2025), the slowdown needed is about 28% in both cases, so this result depends on that choice.

## What the actual data shows

The trends say consumption won't overtake supply for a long time, but in the actual figures it already has. In 2024 and 2025, total consumption (277 and 280 TWh) was higher than electricity supplied (271 and 279 TWh). This is possible because consumption = supply + net imports - losses, so consumption is higher than supply whenever imports are bigger than losses, and in 2024 the UK imported 33 TWh against losses of 27 TWh. The trend lines miss this because they're dominated by the growth before 2005. Supply has fallen from 377 TWh in 2005 to 279 TWh in 2025, while its trend line says about 361 TWh.

2022 also stands out: the UK exported more electricity than it imported that year (net imports of -5 TWh), which is why supply jumps to 310 TWh.

## Limitations

- The straight line is the weakest assumption. Supply and consumption both peaked around 2005 and have fallen since, so a trend starting in 1965 is now about 80 TWh above the actual figures. So it's more of a stress test of the long-run trend than a forecast.
- The year the lines cross is very sensitive. The two slopes are so close that small changes to the data move it by decades.
- It doesn't include electric cars or heat pumps, which could push demand back up. A trend based on past data can't pick that up.

## Files

- `UK_Electricity_Gap.xlsx`: the spreadsheet, with Notes, Data, Model, Sensitivity and Forecast tabs
