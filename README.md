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

## The Gauges

### 1. Deleveraging Engine (The Spread)

```
Spread = Nominal GDP Growth - 10Y Treasury Yield
```

**Why it matters:** If the economy grows faster than the interest rate on debt, the debt-to-GDP ratio naturally shrinks over time. A positive spread means debt is "melting away" without requiring painful cuts or defaults.

**Basis rule:** Nominal GDP growth and the 10Y yield must be on the same basis (e.g., SAAR or YoY). Do not mix bases.

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
Market Real Yield = 10Y TIPS Real Yield
Trailing CPI Proxy = 10Y Treasury Yield - CPI (YoY)
```

**Why it matters:** High real rates mean borrowers pay back more in purchasing power than they received. This crushes debtors (including governments). Low/negative real rates ease the debt burden. The TIPS real yield is the primary signal, with a trailing CPI proxy shown as a check.

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

### 5. Primary Balance (% of GDP)

```
Primary Balance = Revenues - Non-Interest Spending
```

**Why it matters:** A healthy primary balance offsets debt dynamics when r − g is unfavorable. Persistent deficits make deleveraging much harder.

| Value | Signal |
|-------|--------|
| Surplus / near-balance (Green) | Fiscal tailwind |
| Moderate deficit (Amber) | Manageable drag |
| Large deficit (Red) | Structural headwind |

### 6. Interest Burden

```
Net Interest Outlays (% of GDP or % of Revenue)
```

**Why it matters:** High interest costs squeeze fiscal capacity and can force austerity or inflation, even if growth is solid.

| Value | Signal |
|-------|--------|
| Low (Green) | Room to maneuver |
| Medium (Amber) | Watch for rollover risk |
| High (Red) | Debt service pressure |

### 7. Debt Dynamics (Mini Panel)

```
r − g = 10Y Treasury Yield − Nominal GDP Growth
Debt/GDP pressure ≈ (r − g)·Debt/GDP + Primary Deficit
```

**Why it matters:** This ties the spread and fiscal stance together into a single pressure estimate. If it is positive and large, debt ratios tend to rise.

## Usage

### Quick Start

1. Clone the repo:
   ```bash
   git clone https://github.com/johnrfite1/macro-terminal.git
   ```

2. Open `debt_cycle.html` in any browser

3. Update the data inputs in the `<script>` section:
   ```javascript
   const macroData = {
     dataDate: "JAN 08 2026",
     nominalGdpGrowth: 5.9,          // SAAR (quarterly annualized), %
     nominalGdpBasis: "SAAR (quarterly annualized)",
     yield10y: 4.18,                 // Nominal annual yield, %
     cpiInflation: 2.4,              // YoY, %
     cpiBasis: "YoY",
     realYield10y: 1.6,              // 10Y TIPS real yield, %
     productivityGrowth: 4.5,        // YoY, %
     productivityBasis: "YoY",
     primaryBalancePctGdp: -3.2,     // + surplus, - deficit
     netInterestPctGdp: 2.6,         // % of GDP
     netInterestPctRevenue: null,    // % of revenue (optional)
     debtToGdp: 120,                 // % of GDP (optional)
     qualityScore: 4,                // 0=Good, 10=Bad
     lastUpdated: {
       spread: "JAN 05 2026",
       productivity: "DEC 31 2025",
       realRate: "JAN 05 2026",
       debtDynamics: "JAN 05 2026",
       quality: "JAN 05 2026",
       primaryBalance: "OCT 31 2025",
       interestBurden: "OCT 31 2025"
     }
   };
   ```

## Inputs & Units

All growth-rate inputs must share the same basis where they are compared. The spread uses nominal GDP growth and the 10Y yield on the same basis (SAAR or YoY). CPI YoY is only used for the trailing real-rate proxy.

| Variable | Definition | Units / Basis |
|---------|------------|---------------|
| `dataDate` | Display date | Text |
| `nominalGdpGrowth` | Nominal GDP growth | %, basis declared in `nominalGdpBasis` |
| `nominalGdpBasis` | Basis label for nominal GDP growth | "SAAR (quarterly annualized)" or "YoY" |
| `yield10y` | 10Y Treasury yield | Nominal annual %, same basis as `nominalGdpGrowth` |
| `cpiInflation` | CPI inflation | %, basis declared in `cpiBasis` |
| `cpiBasis` | Basis label for CPI | "YoY" (recommended for proxy) |
| `realYield10y` | 10Y TIPS real yield | % |
| `productivityGrowth` | Non-farm productivity growth | %, basis in `productivityBasis` |
| `productivityBasis` | Basis label for productivity | "YoY" or "QoQ SAAR" |
| `primaryBalancePctGdp` | Primary balance | % of GDP (surplus positive) |
| `netInterestPctGdp` | Net interest outlays | % of GDP |
| `netInterestPctRevenue` | Net interest outlays | % of revenue (optional) |
| `debtToGdp` | Debt-to-GDP ratio | % of GDP (optional) |
| `qualityScore` | Distortion score | 0-10 scale |
| `lastUpdated` | Per-metric timestamps | Text strings |

### Data Sources

| Metric | Source | Update Frequency |
|--------|--------|------------------|
| GDP Real | [Atlanta Fed GDPNow](https://www.atlantafed.org/cqer/research/gdpnow) | ~Weekly |
| 10Y Treasury | [Treasury.gov](https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_yield_curve) | Daily |
| CPI Inflation | [BLS CPI](https://www.bls.gov/cpi/) | Monthly |
| Productivity | [BLS Productivity](https://www.bls.gov/lpc/) | Quarterly |

## Beautiful Deleveraging Logic

The spread (nominal growth minus interest rates) is necessary but not sufficient. A positive spread can still fail to reduce debt if the fiscal primary balance is deeply negative or if interest costs absorb too much revenue. Adding Primary Balance and Interest Burden makes the dashboard harder to misread by tying growth to fiscal reality and debt service capacity.

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
