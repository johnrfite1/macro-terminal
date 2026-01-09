# Macro Terminal - Debt Cycle Tracker

A retro CRT-styled dashboard for monitoring macroeconomic deleveraging indicators. Track whether the U.S. economy is successfully "melting away" its debt burden through growth, or heading toward a debt crisis.

![Dashboard Preview](https://img.shields.io/badge/status-active-00FF41?style=flat-square) ![License](https://img.shields.io/badge/license-MIT-blue?style=flat-square)

## What Is This?

This dashboard visualizes the key question: **Can the economy outgrow its debt?**

When a nation accumulates large debts, there are only a few ways out:
1. **Default** - politically catastrophic
2. **Austerity** - economically painful
3. **Inflation** - erodes savings, creates instability
4. **Growth** - the "beautiful deleveraging" where nominal GDP growth exceeds interest rates

This tool tracks whether option #4 is working.

## The Four Gauges

### 1. Deleveraging Engine (The Spread)

```
Spread = Nominal GDP Growth - 10Y Treasury Yield
```

**Why it matters:** If the economy grows faster than the interest rate on debt, the debt-to-GDP ratio naturally shrinks over time. A positive spread means debt is "melting away" without requiring painful cuts or defaults.

| Value | Signal |
|-------|--------|
| > 0% (Green) | Debt burden shrinking organically |
| < 0% (Red) | Debt compounding faster than growth |

### 2. Productivity Velocity

```
Non-Farm Productivity Growth (%)
```

**Why it matters:** Productivity is the only sustainable source of real growth. Without it, GDP growth is just inflation or debt-fueled consumption. Target is **2.5%+** for healthy long-term deleveraging.

| Value | Signal |
|-------|--------|
| > 2.5% (Green) | Real wealth creation, sustainable growth |
| < 2.5% (Red) | Growth may be artificial or debt-driven |

### 3. Real Interest Rate

```
Real Rate = 10Y Treasury Yield - CPI Inflation
```

**Why it matters:** High real rates mean borrowers pay back more in purchasing power than they received. This crushes debtors (including governments). Low/negative real rates ease the debt burden.

| Value | Signal |
|-------|--------|
| < 1.0% (Green) | Accommodative, debt-friendly environment |
| 1.0-1.5% (Amber) | Neutral, watch closely |
| > 1.5% (Red) | Restrictive, debt burden increasing |

### 4. Data Signal Quality

```
Distortion Score (0-10 scale, manual assessment)
```

**Why it matters:** GDP data can be distorted by one-time factors like gold exports, inventory builds, or accounting quirks. This gauge flags when the headline numbers may not reflect underlying economic reality.

| Score | Signal |
|-------|--------|
| 0-2 (Green) | Data is clean and reliable |
| 3-5 (Amber) | Some distortion (gold/inventory noise) |
| 6-10 (Red) | High probability of accounting mirage |

## Usage

### Quick Start

1. Clone the repo:
   ```bash
   git clone https://github.com/johnrfite1/macro-terminal.git
   ```

2. Open `debt_cycle.html` in any browser

3. Update the data inputs in the `<script>` section:
   ```javascript
   const DATA_DATE = "JAN 08 2026";
   const GDP_REAL = 5.4;        // Atlanta Fed GDPNow
   const INFLATION = 2.4;       // CPI Estimate
   const YIELD_10Y = 4.18;      // 10Y Treasury
   const PRODUCTIVITY = 4.5;    // Recent Trend
   const QUALITY_SCORE = 4;     // 0=Good, 10=Bad
   ```

### Data Sources

| Metric | Source | Update Frequency |
|--------|--------|------------------|
| GDP Real | [Atlanta Fed GDPNow](https://www.atlantafed.org/cqer/research/gdpnow) | ~Weekly |
| 10Y Treasury | [Treasury.gov](https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_yield_curve) | Daily |
| CPI Inflation | [BLS CPI](https://www.bls.gov/cpi/) | Monthly |
| Productivity | [BLS Productivity](https://www.bls.gov/lpc/) | Quarterly |

## The Theory Behind It

This dashboard is inspired by Ray Dalio's concept of the "beautiful deleveraging" - the idea that debt crises can be resolved without catastrophic pain if policymakers balance:

- **Austerity** (spending cuts)
- **Debt restructuring** (defaults/haircuts)
- **Money printing** (central bank purchases)
- **Wealth transfers** (taxes on wealthy)

The key metric is whether **nominal growth exceeds nominal interest rates**. When it does, time is on your side. When it doesn't, the debt spiral accelerates.

## Design

The retro CRT terminal aesthetic is intentional - it evokes the Bloomberg terminals and Fed monitoring systems where these decisions get made. The scanline effect and monospace fonts reinforce the "raw data feed" feel.

## License

MIT - Use freely, no warranty implied. This is an educational tool, not financial advice.

---

*"There are only four ways a country can deal with its debts: growth, inflation, austerity, or default. Everything else is just commentary."*
