# Asymmetry Index

Most volatility indicators treat upside and downside moves as equal — but they're not. The Asymmetry Index separates them, measuring whether an asset tends to move faster and harder up or down.

<img width="1810" height="914" alt="kuva" src="https://github.com/user-attachments/assets/9a493a1b-3d9d-4115-8f09-92ce6704bdd2" />

## Metrics

| Metric | Description |
|--------|-------------|
| **SI** (Sensitivity Index) | Intensity of downside streaks |
| **UI** (Upside Index) | Intensity of upside streaks |
| **Reactivity** | (SI + UI) / 2 — overall two-sided reactivity |
| **Asymmetry** | UI / SI — the core metric |

### Reading Asymmetry

- **> 1.2** — Upside-biased: the asset tends to rally faster than it falls
- **0.8 – 1.2** — Symmetric: roughly equal upside and downside speed
- **< 0.8** — Downside-biased: the asset tends to drop faster than it rises

## How It Works

A **streak** is a run of consecutive days moving in the same direction with a total move ≥ threshold (default 2%). When a streak ends, it is recorded.

From the recorded streaks within the lookback window:
1. **Median filter** — only streaks above the median are counted as significant (noise reduction)
2. **Speed weighting** — shorter streaks are up-weighted (faster moves = higher reactivity)
3. **Annualization** — scaled to a 252-bar (1 year) equivalent
4. **Shrinkage** — dampens small sample sizes to prevent inflated scores

## Threshold Zones

Calibrated relative to RSP (S&P 500 Equal Weight ETF, benchmark ≈ 9.2):

| Zone | Reactivity vs RSP | Background |
|------|--------------------|------------|
| Low | < 3× RSP | 🟢 Green |
| Average | 3–6× RSP | 🟡 Yellow |
| High | 6–12× RSP | 🟠 Orange |
| Extreme | > 12× RSP | 🔴 Red |

## Installation (TradingView)

1. Open [Pine Script Editor](https://www.tradingview.com/pine-script-docs/) in TradingView
2. Copy the contents of `sensitivity_index.pine`
3. Paste into the editor and click **Add to chart**
4. Switch to the **Daily (1D)** timeframe

## Settings

| Input | Default | Description |
|-------|---------|-------------|
| Streak threshold (%) | 2.0 | Minimum total move to record a streak |
| Lookback (bars) | 252 | Window size (~1 trading year) |
| RSP Reactivity benchmark | 9.2 | Baseline for rating thresholds |
| Show Upside Index | true | Toggle UI line |
| Show Reactivity | true | Toggle Reactivity line |


You can find settings for the index by hovering your mouse over the legend section (Image 1), then pressing the settings icon after that (image 2).

<img width="231" height="292" alt="kuva" src="https://github.com/user-attachments/assets/d68bbda7-ba17-4325-936b-fb17e751f66d" /> 
<img width="230" height="74" alt="kuva" src="https://github.com/user-attachments/assets/540b953a-f973-46f4-84c2-37665e0be030" />
<img width="375" height="406" alt="kuva" src="https://github.com/user-attachments/assets/55532f57-cddd-4b39-aa24-96f4d4f1a70c" />


## Notes

- Best used on the **Daily (1D)** timeframe — intraday results are not meaningful
- Works on any asset with daily data: stocks, ETFs, crypto, forex
- The RSP benchmark (9.2) is calibrated for equities — for crypto, consider increasing it
- Suitable for all investor types: defensive, momentum, and volatility traders
