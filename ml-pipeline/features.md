# Predictive Engine: Feature Dictionary

This document outlines the high-level feature engineering strategies utilized in the GreenSlips predictive models. *Proprietary weighting and exact mathematical transformations have been redacted.*

## 1. Player Role & Archetype Features
* **Continuous Role Space (8D Latent Vector):** Extracted via PyTorch Autoencoder from 25 raw tracking statistics (e.g., touches, passes, distance traveled, defensive proximity). Replaces legacy discrete K-Means clustering.
* **PAPMY (Positionless Archetype Plus-Minus Yield):** A custom metric measuring a player's impact relative to their specific autoencoder-derived archetype rather than their listed roster position.

## 2. Form & Temporal Features
* **Kalman-Filtered Averages:** Optuna-tuned Q/R parameters applied to rolling game windows (L3, L5, L10, L20) to dynamically smooth variance in player performance based on recent volatility.
* **Synthetic Lines:** Generation of ±3.0 variance thresholds around standard sportsbook lines to map slope probabilities and identify edge opportunities.
* **Rest Disadvantage Metrics:** Factoring in back-to-backs, 3-in-4 nights, and travel mileage impacts.

## 3. Contextual & Matchup Features
* **DUSR v2 (Usage Redistribution):** Cosine-similarity-weighted algorithm that projects usage and stat redistribution when key teammates are marked as `Out` or `Questionable` in the live `InjuryReports` table.
* **Prior-Season RAPM:** Regularized Adjusted Plus-Minus utilized as a baseline prior for early-season predictions to prevent extreme variance in small sample sizes.
* **Defensive Zonal Allowed Rates:** Opponent allowed field goal percentages explicitly mapped to 5 distinct scoring zones (Restricted Area, Paint, Midrange, Corner 3, ATB 3).
