# WiDS
Overview
When a wildfire ignites, emergency managers face an impossible question with incomplete information. Which fires will reach populated areas? How quickly? And which communities should prepare first?

This year's WiDS Global Datathon challenges participants to build survival models that answer these questions using only the earliest signals available. Your task is to predict the probability that a wildfire will threaten an evacuation zone within 12, 24, 48, and 72 hours, drawing on data from just the first five hours after ignition.

The goal is not a single prediction but a calibrated forecast across multiple time horizons. Emergency responders need both urgency rankings (which fires demand immediate attention) and probability estimates they can trust when making high-stakes decisions about evacuations, resource deployment, and public alerts.

Description
Problem
When a wildfire ignites, emergency managers and responders must decide which communities to warn, when to warn them, and where to position scarce resources. Decisions must be made before certainty is available. The response requires both prioritization (which fires are most urgent soon) and calibrated risk estimates (how likely a fire is to threaten evacuation zones within actionable time windows).

This competition turns that operational need into a survival analysis challenge. You will generate calibrated probability forecasts across multiple time horizons to support real-world decisions.

Real-World Context
Many wildfire forecasting approaches reduce the task to a single question. Will this fire become dangerous. Emergency response needs more. Decisions are time-bound and comparative. How soon is a threat likely. How confident should we be. Which incident should move to the front of the queue when crews, aircraft, and messaging capacity are limited.

This competition addresses that gap by framing the task as survival analysis using real early-incident signals. The dataset captures wildfire perimeter dynamics and their spatial relationship to evacuation zones. Features are computed strictly from the first five hours after the initial perimeter observation, t0. The target is the time from t0 plus 5 hours until the fire comes within 5 km of any evacuation zone centroid.


Dataset Description
Data Limitations and Scarcity
This page describes the data, provided files, their formats, and the required submission format.

The dataset contains 316 wildfire events with verified early-stage perimeter observations and confirmed outcomes.

What you receive
Features computed strictly from the first five hours after initial perimeter detection. These represent early spread dynamics and spatial relationships to evacuation zones.

What you predict
Four probabilities for each fire. Each probability represents the likelihood that the fire comes within 5 km of an evacuation zone centroid by the horizon. prob_12h prob_24h prob_48h prob_72h

Understanding the labels
This is right-censored survival data. If a fire reaches an evacuation zone within 72 hours, event is 1 and time_to_hit_hours is observed. If a fire does not reach an evacuation zone within 72 hours, event is 0 and time_to_hit_hours is censored at the last available observation.

Why 316 fires and not 3,000
Most wildfires do not have both requirements needed for reliable labels. Early perimeter updates within the first five hours for feature extraction

Sufficient follow-up perimeter observations to confirm whether and when the threshold was reached. This constraint is structural, not accidental. It reflects how real incident data is collected. It also changes what good modeling looks like.

This competition therefore emphasizes:

Survival-aware modeling
Proper handling of censoring
Calibration over raw accuracy
Dataset Size
Train: 221 rows (69 hits, 152 censored)
Test: 95 rows
Total fires: 316
