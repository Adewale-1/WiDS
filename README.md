
# 🔥 WiDS Wildfire Survival Prediction Challenge

## Overview

When a wildfire ignites, emergency managers must make critical decisions with limited information:

- Which fires will threaten populated areas?
- How quickly will they spread?
- Which communities should prepare first?

In this year’s **WiDS Global Datathon**, we build a **survival model** to help answer these questions using only the earliest signals available.

Our task is to predict the probability that a wildfire will threaten an evacuation zone within:

- **12 hours**
- **24 hours**
- **48 hours**
- **72 hours**

All predictions are based strictly on data from the **first five hours after ignition**.

This is not a simple yes/no classification problem. Instead, we generate **calibrated probability forecasts across multiple time horizons**. Emergency responders need:

- **Urgency rankings** — Which fires require immediate attention  
- **Reliable probability estimates** — Forecasts they can trust when making high-stakes decisions about evacuations, resource deployment, and public alerts  

---

## Problem Description

When a wildfire starts, emergency managers must decide:

- Which communities to warn  
- When to issue warnings  
- Where to deploy limited resources  

These decisions must be made **before certainty is available**.

To support this process, our model must provide:

- **Prioritization** — Which fires pose the most immediate risk  
- **Calibration** — How likely is a fire to threaten evacuation zones within actionable time windows  

This competition translates that operational need into a **survival analysis problem**, where we generate calibrated probability forecasts across multiple time horizons.

---

## Real-World Context

Many wildfire forecasting systems reduce the problem to a single question:

> Will this fire become dangerous?

But emergency response is more nuanced. Decisions are:

- Time-bound  
- Comparative  
- Resource-constrained  

Responders must evaluate:

- How soon is the threat likely?  
- How confident are we in that estimate?  
- Which incident should move to the front of the queue when crews, aircraft, and messaging capacity are limited?  

To address this gap, we frame the task as a **survival analysis problem using early-incident signals**.

---

## Target Definition

- We use features computed strictly from the **first five hours** after the initial perimeter observation (*t₀*).
- The target is the time from *(t₀ + 5 hours)* until the fire comes within **5 km of any evacuation zone centroid**.

---

## Dataset Description

### Data Limitations and Scarcity

The dataset contains **316 wildfire events** with:

- Verified early-stage perimeter observations  
- Confirmed outcomes  

This dataset reflects real-world operational constraints and how wildfire data is collected in practice.

---

## What We Receive

We receive features computed strictly from the first five hours after initial perimeter detection, representing:

- Early fire spread dynamics  
- Spatial relationships to evacuation zones  

---

## What We Predict

For each fire, we generate four probability estimates:

- `prob_12h` — Probability of reaching within 5 km by 12 hours  
- `prob_24h` — Probability by 24 hours  
- `prob_48h` — Probability by 48 hours  
- `prob_72h` — Probability by 72 hours  

Each probability reflects the likelihood that the fire comes within 5 km of an evacuation zone centroid within the specified time horizon.

---

## Understanding the Labels

This is **right-censored survival data**, so proper handling of censoring is essential.

- If a fire reaches an evacuation zone within 72 hours:  
  - `event = 1`  
  - `time_to_hit_hours` is observed  

- If a fire does not reach an evacuation zone within 72 hours:  
  - `event = 0`  
  - `time_to_hit_hours` is censored at the last available observation  

---

## Why Only 316 Fires?

Most wildfires do not meet the strict requirements needed for reliable labeling. Each fire must have:

1. Early perimeter updates within the first five hours (for feature extraction)  
2. Sufficient follow-up perimeter observations to confirm whether and when the 5 km threshold was reached  

This constraint is structural, not accidental. It reflects real incident data collection practices and changes what good modeling looks like.

---

## Our Modeling Focus

In this project, we focus on:

- Survival-aware modeling  
- Proper handling of censoring  
- Calibration over raw accuracy  

---

## Dataset Size

- **Train:** 221 fires  
  - 69 hits  
  - 152 censored  

- **Test:** 95 fires  

- **Total:** 316 fires  
