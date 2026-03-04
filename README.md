# Chicago Red Light Camera Causal Inference Analysis

## Executive Summary
This project investigates the causal impact of the 2017 red light camera deactivations on municipal revenue in Chicago. It employs a Difference-in-Differences (DiD) framework to isolate the treatment effect of the policy change. To mitigate selection bias inherent in camera placement, Propensity Score Matching (PSM) is used to construct a credible counterfactual. The analysis quantifies the trade-off between policy-driven decommission and city revenue.

## Project Highlights
* Geospatial Analysis: Visualized program rollout and camera density using Folium heatmaps.
* Causal Framework: Implemented a Quasi-Experimental design to evaluate a targeted 2017 decommission of 6 intersections.
* Econometric Matching: Utilized 3-Nearest Neighbor matching on pre-period volume to ensure group comparability.
* Statistical Rigor: Validated parallel trends via leads-and-lags event studies and placebo regressions.

## Methodology
1. Data Ingestion and Preprocessing: Standardized schema and cast temporal features to datetime objects. Filtered the observation window to 2016–2018 to isolate the policy shock from the COVID-19 pandemic.
2. Balanced Panel Construction: Constructed a balanced panel dataset by re-indexing the time-series. Forced zero-value entries for decommissioned intersections to ensure the model captures the drop to zero revenue post-treatment.
3. Propensity Score Matching (3-NN): Implemented a 3-Nearest Neighbor matching algorithm based on pre-period violation volume. This creates a control group of active intersections that share a statistically identical baseline with the treatment group.
4. Difference-in-Differences Estimation: Executed a fixed-effects OLS regression to estimate the Average Treatment Effect (ATE). Clustered standard errors at the intersection level to account for intra-group temporal correlation.
5. Robustness Checks: Placebo Evaluation: Assigned a "fake" treatment date in 2016 to confirm a non-significant interaction coefficient ($p > 0.05$).Event Study: Plotted relative time dummies to verify the absence of anticipatory effects and confirm the exact timing of the "cliff" in June 2017.

## Key Findings & Economic Impact
The analysis identified a highly significant causal drop in violations following the deactivations ($p < 0.001$).
* Monthly Impact: Average loss of 233.88 violations per intersection, per month.
* Annual Revenue Impact: Total estimated loss of $1,683,936.00 across the 6 removed intersections.
* 95% Confidence Interval: Annual impact ranges between $1.17M and $2.19M.
* Portfolio Percentage: This decommission represented a 2.8% reduction in total annual red light violation revenue (based on an estimated city-wide baseline of $60M).ConclusionWhile the 2017 decommission targeted safety improvements, it resulted in a non-trivial and permanent reduction in municipal revenue. This project demonstrates how econometric matching and DiD can be deployed to provide policymakers with a precise accounting of the financial trade-offs inherent in urban safety programs.

## Conclusion
While the 2017 decommission targeted safety improvements, it resulted in a non-trivial and permanent reduction in municipal revenue. This project demonstrates how econometric matching and DiD can be deployed to provide policymakers with a precise accounting of the financial trade-offs inherent in urban safety programs.

## Software & Libraries
* Language: Python 3.10+
* Data Manipulation: pandas, numpy
* Geospatial Visualization: folium (Interactive Heatmaps)
* Statistical Visualization: matplotlib, seaborn
* Econometric Modeling: statsmodels (OLS, Cluster-Robust Standard Errors)
* Machine Learning: scikit-learn (Nearest Neighbors for matching)

## Causal Inference Framework
* Difference-in-Differences (DiD): The primary estimator used to identify the average treatment effect on the treated (ATT) by comparing the change in violations across treatment and control groups.
* Propensity Score Matching (PSM): A 3-Nearest Neighbor (3-NN) algorithm was deployed to select control intersections with similar pre-period violation profiles, mitigating selection bias.
* Fixed Effects (FE): Incorporated to control for time-invariant intersection characteristics and city-wide temporal shocks.
* Event Study Design: Implementation of a leads-and-lags model to visualize the dynamic treatment effect and empirically test the parallel trends assumption.
* Placebo Testing: Counterfactual validation using "fake" treatment dates to ensure the model does not detect spurious effects.
