<div align="center">

<!-- DYNAMIC TYPING HEADER -->
<a href="https://github.com/Madhvansh">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=28&duration=3000&pause=1000&color=58A6FF&center=true&vCenter=true&multiline=true&repeat=true&width=900&height=100&lines=%F0%9F%8F%AD+Building+AI+that+runs+real+factories;MPC+%2B+Chronos-2+%2B+Physics+%E2%86%92+Zero+critical+failures" alt="Typing SVG" />
</a>

<br/>

<!-- BADGES ROW -->
[![GitHub](https://img.shields.io/badge/Madhvansh-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Madhvansh)
[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](#)
[![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](#)
[![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](#)
[![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)](#)

</div>

---

## `$ whoami`

**Madhvansh Choksi** — building production AI systems for industrial water treatment.

I don't make demos. I make systems that **run 24/7 on real cooling towers**, replacing chemical dosing decisions that used to require a human operator staring at a SCADA screen.

Currently shipping **[TGF](https://github.com/Madhvansh/TGF)** — an autonomous cooling tower control system that predicts water chemistry 6–24 hours ahead and optimizes chemical dosing across 7 simultaneous treatment chemicals using Model Predictive Control.

**The short version:** Nalco and ChemTreat charge $50K+/year to reactively dose 1–2 chemicals. TGF predicts the future and optimizes all 7 at once — delivering 15–30% chemical savings with zero critical failures.

---

## 🏗️ Flagship: TGF — AI-Driven Autonomous Cooling Tower Control

<div align="center">

[![TGF](https://img.shields.io/badge/🏭_TGF-Autonomous_Cooling_Tower_Control-blue?style=for-the-badge)](https://github.com/Madhvansh/TGF)
[![Python 94%](https://img.shields.io/badge/Python-94.2%25-3776AB?style=flat-square&logo=python&logoColor=white)](https://github.com/Madhvansh/TGF)
[![License](https://img.shields.io/badge/License-Open_Source-green?style=flat-square)](https://github.com/Madhvansh/TGF)

</div>

### The Problem

Industrial cooling towers waste **billions of dollars** annually on chemical treatment because dosing is reactive — operators wait for pH to drift, then dump chemicals. Meanwhile, scaling corrodes heat exchangers, biofouling clogs fills, and plants lose efficiency.

Every major vendor (Nalco/Ecolab, ChemTreat, Solenis) sells the same thing: a fluorescent tracer that measures **one** chemical accurately, then charges you for the privilege of vendor lock-in.

### The Architecture

```
Sensors (pH, Conductivity, Temp, ORP)
        │
        ▼
┌───────────────────────┐     ┌────────────────────────────┐
│  Chronos-2 Forecaster │────▶│  Statistical Fallback      │
│  (Zero-shot p10/50/90)│     │  (when GPU unavailable)    │
└──────────┬────────────┘     └────────────────────────────┘
           │
           ▼
┌───────────────────────┐     ┌────────────────────────────┐
│  Physics Engine       │◀───▶│  Chemical Residual Tracker  │
│  (LSI/RSI/CoC/Risk)   │     │  (Mass balance × 7 chems)  │
└──────────┬────────────┘     └───────────┬────────────────┘
           │                              │
           ▼                              ▼
┌──────────────────────────────────────────────┐
│  MPC Dosing Optimizer                         │
│  scipy L-BFGS-B · 2-hour receding horizon    │
│  Cost = chemical_cost + risk_penalties        │
└─────────────────┬────────────────────────────┘
                  │
                  ▼
┌──────────────────────────────────────────────┐
│  Safety Layer                                 │
│  Sensor fault detection · Hard limits         │
│  Rate limiting · PID backup · Emergency stop  │
└─────────────────┬────────────────────────────┘
                  │
                  ▼
           Pump Commands + Blowdown
```

### Results (5,614 control cycles · 19.5 simulated days)

| Metric | Value |
|---|---|
| **LSI in optimal range** | 86.2% |
| **CRITICAL risk cycles** | **0.0%** |
| **Preemptive decisions** | 78% (forecast-driven, not reactive) |
| **Chemical adequacy** | 52–86% across all 7 chemicals |
| **Risk profile** | 47.5% LOW · 44.7% MODERATE · 7.8% HIGH |

### Why This Beats the Industry

| | Nalco TRASAR | ChemTreat | **TGF** |
|---|---|---|---|
| Chemicals tracked | 1–2 (fluorescent) | 1 (tracer) | **All 7 (mass balance)** |
| Prediction | None (reactive) | None (reactive) | **6–24h ahead (Chronos-2)** |
| Dosing strategy | Threshold-based | Threshold-based | **MPC-optimized** |
| Multi-vendor | ❌ Locked in | ❌ Locked in | **✅ Configurable** |
| Cost optimization | ❌ | ❌ | **✅ INR-minimizing** |

### Technical Decisions (and why)

- **MPC over RL (SAC/PPO):** Hard safety constraints are *guaranteed*, not learned. Works with 5K samples. Explainable to plant operators.
- **Chronos-2 over PatchTST:** Zero-shot works immediately on new towers. PatchTST needs fine-tuning on data we don't have yet.
- **Mass balance over virtual sensors:** We tried ML-based virtual sensors for hardness/alkalinity — R²=0.37 was too unreliable. Physics-based mass balance with weekly lab calibration is honest engineering.
- **Statistical fallback always ready:** Every Chronos-2 call has a Holt-Winters backup. No single point of failure.

---

## 🧰 Full Stack

```python
tech_stack = {
    "ai_ml": ["PyTorch", "Chronos-2", "MOMENT", "TransNAS", "scikit-learn"],
    "optimization": ["scipy (L-BFGS-B)", "Model Predictive Control"],
    "backend": ["FastAPI", "SQLite (WAL)", "uvicorn"],
    "physics": ["Langelier SI", "Ryznar SI", "Arrhenius decay", "Mass balance"],
    "infra": ["Real-time dashboards", "Alert systems", "Sensor simulation"],
    "research": ["State Space Models (S4/Mamba)", "CoreML", "Time-series AD"],
    "languages": ["Python", "JavaScript", "Java", "SQL", "HTML/CSS"],
}
```

---

## 📦 Other Projects

| Project | What it does | Stack |
|---|---|---|
| [**Cooling Tower Dashboard**](https://github.com/Madhvansh/Cooling-Tower-Dashboard-Atul-Ltd.-) | Production monitoring dashboard for 15 cooling towers at Atul Ltd. Real-time status, priority-based issue tracking, Chart.js viz. **Deployed at [Vercel](https://cooling-tower-dashboard-atul-ltd.vercel.app/) & Netlify.** | HTML · CSS · JS · Chart.js |
| [**SAiDL Spring 2025**](https://github.com/Madhvansh/SAiDL-Spring-Assignment-2025) | Research assignments — State Space Models (S4/Mamba), CoreML exploration | PyTorch · Jupyter |
| [**DSA**](https://github.com/Madhvansh/DSA) | Data structures & algorithms | — |
| [**OOPs**](https://github.com/Madhvansh/OOPs) | Object-oriented programming patterns | Java |

---

## 📊 GitHub Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=Madhvansh&show_icons=true&theme=github_dark&hide_border=true&count_private=true&include_all_commits=true" height="170" alt="GitHub Stats" />
<img src="https://github-readme-streak-stats.herokuapp.com?user=Madhvansh&theme=github-dark-blue&hide_border=true" height="170" alt="GitHub Streak" />

<br/>

<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Madhvansh&layout=compact&theme=github_dark&hide_border=true&langs_count=8" height="170" alt="Top Languages" />

</div>

---

## � What I'm Building Next

- **MOMENT foundation model integration** — reconstruction-based anomaly detection plugged into the TGF control loop (architecture is ready, awaiting model fine-tuning)
- **Multi-tower orchestration** — coordinated dosing across cooling tower farms sharing blowdown/makeup water
- **Edge deployment** — running the full MPC stack on industrial edge hardware (Raspberry Pi + sensor HATs for proof-of-concept)

---

## 🤝 Claude × TGF

I use Claude extensively in my development workflow — from debugging MPC cost functions to exploring Chronos-2 integration patterns to writing the physics engine's Arrhenius decay model. The TGF codebase is deeply intertwined with Claude-assisted development.

**What Claude Max would unlock:**
- Faster iteration on the MOMENT anomaly detection integration
- Multi-file refactoring across the 20+ module codebase
- Exploring novel MPC formulations with longer planning horizons
- Writing comprehensive test suites for safety-critical dosing logic

This isn't a side project. It's production software targeting a **$10B+ industrial water treatment market** where the incumbents haven't innovated in decades. Claude is the only AI assistant that can reason about the physics *and* the code simultaneously.

---

<div align="center">

<img src="https://komarev.com/ghpvc/?username=Madhvansh&style=for-the-badge&color=58A6FF" alt="Profile Views" />

<br/><br/>

**Building the future of industrial AI — one control cycle at a time.**

*If cooling towers interest you (or if you think MPC is underrated), let's talk.*

[![GitHub](https://img.shields.io/badge/GitHub-Madhvansh-181717?style=flat-square&logo=github)](https://github.com/Madhvansh)

</div>
