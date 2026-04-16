# Sentinel Quant v3.2 - Public Edition

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.19284847.svg)](https://doi.org/10.5281/zenodo.19284847)
[![Dashboard](https://img.shields.io/badge/Live_Dashboard-sentinel--quant-blue)](https://sentinel-quant-dashboard.vercel.app)
[![Feedback Form](https://img.shields.io/badge/Feedback-Google%20Form-green)](https://forms.gle/jKDN18pMzP3mCpJU6)

Multi-strategy AI trading agent demonstrating a modular architecture for
quantitative research, AI-assisted analysis, and automated portfolio
monitoring.

This **Public Edition (SQ-PE)** is a sanitized showcase version intended
for engineering demonstration and portfolio purposes. Certain components
such as proprietary signals, calibrated thresholds, production broker
integrations, and optimized portfolio parameters are intentionally
omitted or simplified.

The goal of this repository is to demonstrate **systems architecture, AI
integration, and quantitative engineering practices** without exposing
proprietary trading logic.

---

## Associated Paper

This project is accompanied by the paper:

**Sentinel Quant: A Human-in-the-Loop Multi-Model Portfolio Management System with Formal AI Governance Architecture**
[https://doi.org/10.5281/zenodo.19284847](https://doi.org/10.5281/zenodo.19284847)

---

## Live Dashboard

> **[sentinel-quant-dashboard.vercel.app](https://sentinel-quant-dashboard.vercel.app)**

The public dashboard provides real-time visibility into the system's performance, including:

- Portfolio equity curve with S&P 500 (SPY) benchmark comparison
- Alpha vs SPY calculation showing risk-adjusted outperformance
- Position management across three strategy sleeves
- Risk governance state (regime, VIX, exposure, beta)
- AI intelligence calibration and accuracy metrics
- Quarterly ETF review with recommendation tracking
- Trade journal with AI post-mortem analysis
- Fund oversight and intelligence review cycle

---

## System Architecture

```
                        +------------------+
                        |   Market Hours   |
                        |      Gate        |
                        +--------+---------+
                                 |
                        +--------v---------+
                        |  Market Screener |
                        | Periodic scans   |
                        +--------+---------+
                                 |
                  +--------------+--------------+
                  |              |              |
         +--------v---+  +------v-----+  +-----v------+
         | Short-Term |  |  Mid-Term  |  |  Long-Term |
         | Momentum   |  |   Trend    |  | Portfolio  |
         | Signals    |  |   Signals  |  | Allocation |
         +--------+---+  +------+-----+  +-----+------+
                  |              |              |
                  +--------------+--------------+
                                 |
                        +--------v---------+
                        | Regime Detection |
                        | Market Volatility|
                        +--------+---------+
                                 |
                  +--------------+--------------+
                  |              |              |
         +--------v---+  +------v-----+  +-----v------+
         |    Risk    |  | Volatility |  |    Beta     |
         |   Engine   |  | Management |  | Monitoring  |
         +--------+---+  +------+-----+  +-----+------+
                  |              |              |
                  +--------------+--------------+
                                 |
                        +--------v---------+
                        | Intelligence     |
                        | Calibration +    |
                        | Meta-Model       |
                        +--------+---------+
                                 |
                  +--------------+--------------+
                  |              |              |
         +--------v---+  +------v-----+  +-----v------+
         | Execution  |  | Dashboard  |  | Notification|
         | Sim Broker |  |  Next.js   |  | System      |
         +------------+  +------------+  +-------------+
```

---

## Core Concepts

### Multi-Strategy Portfolio
The system manages three concurrent strategy sleeves with independent risk budgets: short-term momentum, mid-term trend following, and long-term strategic allocation via quarterly ETF review. Each sleeve operates with its own entry criteria, holding period, and exit logic.

### AI Governance Architecture
Every trade proposal passes through a multi-layered risk engine before execution. The system uses a human-in-the-loop governance model where AI generates recommendations and a formal risk framework enforces constraints. No trade executes without passing all governance checks.

---

## Risk Engine

The risk governance system implements a multi-layered protection framework with **16+ automated checks** covering:

- **Order integrity** — duplicate prevention, daily trade limits
- **Loss containment** — global and per-sleeve daily loss caps
- **Position management** — sleeve-level count and size limits, minimum trade thresholds
- **Earnings protection** — calendar-aware blocking around earnings announcements with configurable pre- and post-earnings windows
- **Portfolio protection** — drawdown circuit breaker, global exposure cap, cash reserve enforcement
- **Diversification** — sector concentration limits at both portfolio and sleeve level, correlation-based blocking for overlapping positions
- **Entry quality** — technical confirmation scoring, intraday momentum validation
- **Adaptive sizing** — loss streak detection with automatic position size reduction, regime-aware confidence adjustment
- **Sector intelligence** — momentum-based confidence adjustments favouring strong sectors and penalising weak ones
- **AI calibration** — confidence threshold enforcement based on model self-assessment

Short-term positions are managed with automated exit rules including stop-loss, take-profit, and time-based exits at calibrated thresholds.

---

## AI Intelligence Features

### Earnings Calendar Gate
Blocks buy proposals near scheduled earnings announcements with configurable time windows per strategy sleeve. Includes a post-earnings cool-off period to prevent chasing initial reactions. Uses free market calendar data with intelligent caching to minimise API calls.

### Sector Momentum Rotation
Monitors performance across all major market sectors using ETF proxies. Sectors showing strong relative momentum receive a confidence boost on buy proposals, while underperforming sectors receive a confidence penalty. Data is cached and injected into strategy prompts for both short-term and mid-term analysis.

### Sell-Side Thesis Tracking
When the AI recommends buying a stock, the original reasoning is stored alongside the position. When evaluating whether to sell, the original buy thesis is injected into the prompt so the AI can assess whether the thesis has broken or still holds, rather than reacting purely to price movement.

### Trade Journal Post-Mortem
After every closed trade, the AI analyses the decision with structured scoring across multiple dimensions. Results are stored in an append-only journal that builds a dataset for identifying systematic biases and improving future decision-making.

### Self-Learning Feedback Loop
Recent trade outcomes are injected into strategy prompts, allowing the AI to calibrate its confidence based on its own track record. The system tracks performance by sleeve and adjusts behaviour based on accumulated evidence.

### Entry Quality Filter
Before approving a buy, the system evaluates multiple technical confirmations. Trades that fail to meet the quality threshold receive a confidence penalty, reducing position size on marginal setups rather than hard-blocking them.

### Drawdown Circuit Breaker
If the portfolio experiences a significant intraday drawdown, all new buy proposals are temporarily suspended. This prevents the system from buying into a falling market and compounding losses during adverse conditions.

### Loss Streak Detection
After a configurable number of consecutive losing trades, position sizes are automatically reduced until the next winning trade resets the counter. This proven risk management technique prevents compounding during cold streaks.

---

## Dashboard Features

### AI vs S&P 500 Benchmark
The equity curve displays a dual-axis comparison: portfolio value vs S&P 500 percentage return with a toggle button. Returns are deposit-adjusted so periodic capital additions don't inflate apparent performance vs the benchmark.

### Alpha KPI Card
Displays portfolio return minus SPY return as a single metric, showing risk-adjusted outperformance at a glance.

### Trade Journal Viewer
When post-mortem entries exist, the dashboard displays scored journal entries with aggregate statistics and individual trade analyses, providing transparency into the AI's self-assessment process.

---

## Automated Reports

The system generates multiple automated reports on configurable schedules:

| Report | Description |
|--------|-------------|
| Weekly Trading Report | Trade summary, P&L breakdown, risk events |
| API Usage Report | AI API call breakdown, cost analysis |
| Weekend Portfolio Digest | Opus-powered narrative analysis with separate private and public editions |
| Monthly Review | Long-term trend analysis, strategy effectiveness assessment |
| Daily Lesson | Post-market single-paragraph lesson from the day's trading activity |

---

## Deployment

The system runs on cloud infrastructure with containerised trading agents, a modern web dashboard, and scheduled intelligence tasks.

| Component | Technology |
|-----------|------------|
| Trading agents | Python, Docker |
| Dashboard | Next.js, Recharts, Tailwind CSS |
| AI models | Claude Sonnet (trading), Claude Opus (reviews) |
| Hosting | Cloud VPS (agents), Vercel (dashboard) |
| Data | Yahoo Finance, Alpaca Markets API |

---

## Public vs Production

| Feature | Public Edition | Production System |
|---------|---------------|-------------------|
| Broker | Simulated environment | Live broker integrations |
| Signals | Simplified / partial | Proprietary signal models |
| Risk parameters | Generic examples | Calibrated portfolio parameters |
| Universe size | Reduced | Full research universe |
| AI prompts | Simplified | Tuned and optimized |
| Infrastructure | Demonstration | Production deployment |

---

## Technical Highlights

- Zero-trust architecture for AI-generated signals
- Multi-layered risk engine with 16+ automated governance checks
- Earnings-aware trading with calendar integration
- Sector momentum rotation with dynamic confidence adjustment
- AI self-reflection via trade journal post-mortems
- Deposit-adjusted benchmark comparison against S&P 500
- Regime-adaptive portfolio behaviour
- AI confidence calibration and self-correction
- Automated drawdown protection and loss streak management
- Modular quant research framework

---

## Live API

The system exposes a public metrics endpoint serving anonymized, real-time performance data:

```
GET https://sentinel-quant-dashboard.vercel.app/api/metrics
```

**Response** (JSON, CORS-enabled):

| Field | Description |
|-------|-------------|
| performance.total_return_pct | Cumulative portfolio return |
| performance.sharpe_ratio | Risk-adjusted return metric |
| performance.win_rate_pct | Percentage of profitable trades |
| performance.total_trades | Lifetime trade count |
| risk.regime | Current market regime (LOW_VOL / NORMAL / HIGH_VOL / CRISIS) |
| risk.vix_level | Current VIX reading |
| risk.portfolio_beta | Portfolio beta vs benchmark |

No authentication required. Position details and trade reasoning are
stripped for privacy. Data refreshes every 30 minutes during market hours.

---

## Risk Disclosure

Trading financial markets involves substantial risk. This repository is intended for **research and educational purposes only**. The public implementation is not intended for live trading and does not represent financial advice.

---

## Citation

If you reference this project or its architecture, please cite:

Oke, I. E. (2026). *Sentinel Quant: A Human-in-the-Loop Multi-Model Portfolio Management System with Formal AI Governance Architecture* (Version 1.0). Zenodo. https://doi.org/10.5281/zenodo.19284847

```bibtex
@report{oke2026sentinelquant,
  author = {Oke, Iyanuoluwa Enoch},
  title = {Sentinel Quant: A Human-in-the-Loop Multi-Model Portfolio Management System with Formal AI Governance Architecture},
  year = {2026},
  publisher = {Zenodo},
  version = {1.0},
  doi = {10.5281/zenodo.19284847},
  url = {https://doi.org/10.5281/zenodo.19284847}
}
```

---

## License

MIT License

---

## Attribution

Sentinel Quant - Public Engineering Showcase
Developed by **Iyanuoluwa Oke**

GitHub: https://github.com/Iyanuoluwa007

## Feedback

If you explore the project and have suggestions or comments, feedback is welcome:

**Google Form:** https://forms.gle/jKDN18pMzP3mCpJU6

Feedback from researchers, engineers, and quantitative developers is especially appreciated.
