<!-- ═══════════════════════════════════════════════════════════════════ -->
<!--                    SAURAV CHAUDHARI — README                   -->
<!-- ═══════════════════════════════════════════════════════════════════ -->

<div align="center">

```
╔═══════════════════════════════════════════════════════════════════╗
║  ∂²x/∂t² + γ(∂x/∂t) + ω²x = F(t)   →   P&L = ∫ α(τ) dS(τ)   ║
║           Signal Processing  ←──────────→  Quantitative Finance   ║
╚═══════════════════════════════════════════════════════════════════╝
```

# Saurav Chaudhari

**Researcher · Signal Processing → Quantitative Finance**


![Location](https://img.shields.io/badge/📍_Pune,_India-2d2d2d?style=flat-square)
![Patent](https://img.shields.io/badge/🏛_Patent-202521106451-8B5CF6?style=flat-square)

</div>

---

## ⚡ The Core Idea

> *Markets are noisy channels. Prices are corrupted signals. Alpha is the carrier buried in the noise.*

I work at the intersection of **RF & array signal processing** and **quantitative finance**, porting battle-tested algorithms from wireless communications (MIMO, OFDM, PLL, M-estimators) directly into market microstructure, portfolio construction, and lead-lag detection.

The insight: the mathematics that resolves multipath delays in Wi-Fi channels can also resolve the propagation delay of information across correlated assets.

---

## 🔬 Research Focus

```
┌──────────────────────────────────────────────────────────────┐
│  RF / Array Signal Processing          Quantitative Finance  │
│  ─────────────────────────────         ──────────────────    │
│  MUSIC algorithm          →→→          Lead-lag detection    │
│  Phase-Locked Loop        →→→          Adaptive price filter │
│  Tyler's M-estimator      →→→          Robust covariance     │
│  MIMO channel estimation  →→→          Factor model fitting  │
│  3D RF spatial mapping    →→→          Alternative data       │
└──────────────────────────────────────────────────────────────┘
```

**Key domains:** Market Microstructure · Robust Statistics · Array Processing · Portfolio Optimization · RF-Based Sensing · High-Frequency Signal Analysis

---

## 📌 Pinned Projects

### 🎯 [MUSIC for Lead-Lag Detection](https://github.com/SauravLChaudhari/MUSIC-for-Lead-Lag-Detection)
> *MIMO-OFDM inspired cross-asset lead-lag estimation*

In wireless systems, **MUSIC** (MUltiple SIgnal Classification) resolves sub-sample multipath delays by decomposing covariance matrices into signal and noise subspaces. Here I apply the same eigenspace decomposition to a **basket of correlated assets** (SPY, QQQ, AAPL, MSFT), treating them as an antenna array to estimate the millisecond-level propagation delay of information across assets.

```
y_i(t) = aᵢ · s(t − τᵢ) + noise    →    MUSIC spectrum peaks at true delays τ
```

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)
![Stars](https://img.shields.io/github/stars/SauravLChaudhari/MUSIC-for-Lead-Lag-Detection?style=flat-square&color=yellow)

---

### 🔒 [PLL for Market Microstructure](https://github.com/SauravLChaudhari/pll-market-microstructure)
> *Adaptive price denoising via spread-aware Kalman filtering*

A **Phase-Locked Loop** tracks a carrier by adapting its filter bandwidth to SNR. I implement a Kalman filter with **time-varying measurement noise** driven by the bid-ask spread — when the spread widens (low SNR), the filter trusts the noisy mid-price less and relies more on the state model.

```
R_k = (spread_k / 2)² × α      ←  spread = noise proxy
x_k = x_{k−1} + w_k            ←  true price as latent state
```

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)
![Stars](https://img.shields.io/github/stars/SauravLChaudhari/pll-market-microstructure?style=flat-square&color=yellow)

---

### 🛡️ [Tyler Covariance Estimation](https://github.com/SauravLChaudhari/tyler-covariance-estimation)
> *Robust portfolio covariance via Tyler's M-Estimator*

Sample covariance matrices collapse during flash crashes. **Tyler's M-Estimator**, borrowed from robust RF array processing, iteratively reweights observations to down-weight outlier returns — producing a covariance matrix that is stable through market dislocations, used directly for minimum-variance portfolio construction.

```
S = (p/n) · Σᵢ [ (xᵢxᵢᵀ) / (xᵢᵀ S⁻¹ xᵢ) ]   ←  fixed-point iteration
```

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white)
![Stars](https://img.shields.io/github/stars/SauravLChaudhari/tyler-covariance-estimation?style=flat-square&color=yellow)

---

## 📄 Publications

| Year | Title | Venue |
|------|-------|-------|
| 2025 | **3D Room Mapping Using RF Signal Analysis: A Novel Approach to Spatial Reconstruction Without Camera-Based Systems** *(with S. P. Gawande)* | Preprint / HTNP Industries |
| — | **Binomial Distribution Theorem in Portfolio Rebalancing: A Model for Outperforming the Nifty Index** | — |

> 🔗 Full list on [ORCID](https://orcid.org/0000-0003-1191-9015) · [ResearchGate](https://www.researchgate.net/profile/Saurav-Chaudhari)

---

## 🏛️ Patent

| Application No. | Status | Field |
|----------------|--------|-------|
| **202521106451** | Published · India | Signal Processing / RF Sensing |

---

## 🧰 Tech Stack

<div align="center">

| Layer | Tools |
|-------|-------|
| **Languages** | ![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![MATLAB](https://img.shields.io/badge/MATLAB-0076A8?style=flat-square&logo=mathworks&logoColor=white) |
| **Quant / Math** | ![NumPy](https://img.shields.io/badge/NumPy-013243?style=flat-square&logo=numpy&logoColor=white) ![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=flat-square&logo=scipy&logoColor=white) ![Pandas](https://img.shields.io/badge/Pandas-150458?style=flat-square&logo=pandas&logoColor=white) |
| **ML / Stats** | ![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat-square&logo=scikit-learn&logoColor=white) ![statsmodels](https://img.shields.io/badge/statsmodels-4B8BBE?style=flat-square) |
| **Notebooks** | ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=jupyter&logoColor=white) |
| **Signal Proc.** | `MUSIC` `Kalman Filter` `ESPRIT` `Beamforming` `M-estimators` |
| **Quant** | `Market Microstructure` `Portfolio Optimization` `Lead-Lag` `HFT Signals` |

</div>

---

## 📊 GitHub Stats

<div align="center">

<!-- Streak stats — demolab is far more reliable than vercel deployments -->
<img src="https://streak-stats.demolab.com/?user=SauravLChaudhari&theme=tokyonight&hide_border=true&date_format=j%20M%5B%20Y%5D" alt="GitHub Streak" />

<br/><br/>

<!-- Key metrics via shields.io dynamic badges — pulls live from GitHub API, never rate-limited -->
![Repos](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2FSauravLChaudhari&query=%24.public_repos&label=Public%20Repos&style=flat-square&color=1e90ff)
![Followers](https://img.shields.io/github/followers/SauravLChaudhari?style=flat-square&label=Followers&color=6366f1)
![Stars](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fapi.github.com%2Fusers%2FSauravLChaudhari&query=%24.public_gists&label=Gists&style=flat-square&color=10b981)
[![MUSIC stars](https://img.shields.io/github/stars/SauravLChaudhari/MUSIC-for-Lead-Lag-Detection?style=flat-square&label=⭐%20MUSIC-Lead-Lag&color=f59e0b)](https://github.com/SauravLChaudhari/MUSIC-for-Lead-Lag-Detection)
[![PLL stars](https://img.shields.io/github/stars/SauravLChaudhari/pll-market-microstructure?style=flat-square&label=⭐%20PLL-Microstructure&color=f59e0b)](https://github.com/SauravLChaudhari/pll-market-microstructure)
[![Tyler stars](https://img.shields.io/github/stars/SauravLChaudhari/tyler-covariance-estimation?style=flat-square&label=⭐%20Tyler-Covariance&color=f59e0b)](https://github.com/SauravLChaudhari/tyler-covariance-estimation)

<!-- Top languages via profile-summary-cards — separate deployment, independent uptime -->
<img src="https://github-profile-summary-cards.vercel.app/api/cards/repos-per-language?username=SauravLChaudhari&theme=tokyonight" height="165" />
<img src="https://github-profile-summary-cards.vercel.app/api/cards/productive-time?username=SauravLChaudhari&theme=tokyonight&utcOffset=5.5" height="165" />

</div>

---

## 💡 Philosophy

```python
def research_thesis():
    """
    The same mathematics that resolves a 3-nanosecond multipath
    delay in a Wi-Fi channel can resolve the 200-millisecond
    information propagation delay across correlated equities.

    Markets are imperfect channels.
    Prices are corrupted observations.
    The job is to estimate the latent signal — cleanly.
    """
    signal_processing_toolkit → quantitative_finance_alpha
    return "build things that work, mathematically"
```

---

<div align="center">

*"The market is a noisy channel. Build a better decoder."*

[![Profile Views](https://komarev.com/ghpvc/?username=SauravLChaudhari&color=6366f1&style=flat-square&label=Profile+Views)](https://github.com/SauravLChaudhari)

</div>
