#### **THE REALISTIC, HONEST, EXECUTABLE PROJECT**

#### 

#### **PROJECT TITLE:**

***Multi-Scale Energy Stress Analysis: Integrating Building Behavior and Grid Operations in Southern California***



##### **PART 1: GRID STRESS ANALYSIS (CAISO) - 5 WEEKS**

##### 

###### **Week 1: Data Prep + Baseline Anomaly Detection**



**Days 1-3: Data Processing** 



Load CAISO 5-minute data

Aggregate to hourly (since buildings are hourly)

Merge with weather variables

Create stress labels: (price > $100) OR (demand > 95th percentile) OR (renewable\_curtailment > threshold)

Check class balance (should be 5-15% stress events)



**Days 4-7: Simple Anomaly Detection**



Statistical thresholding (z-score > 2.5)

Isolation Forest

Compare methods

Identify major anomaly events (2020 blackouts, heat waves)



Deliverable: Baseline anomaly timeline + evaluation metrics



###### **Week 2: Advanced Anomaly Detection**



**Days 1-4: LSTM Autoencoder**



Architecture: Encoder-decoder, 168-hour input sequences

Train on normal periods only

Reconstruction error = anomaly score

Training time: 2-3 hours



**Days 5-7: Anomaly Interpretation**



Which features have high reconstruction error?

SHAP analysis on autoencoder

Case studies: Major stress events

Compare autoencoder vs Isolation Forest (which catches more real events?)



Deliverable: Trained autoencoder + interpreted anomalies



###### **Week 3: Grid Regime Detection**



**Days 1-3: K-Means Clustering**



Features: demand\_normalized, renewable\_share, net\_demand, price\_zscore

Optimal k (4-6 clusters via elbow method)

Label regimes: "Normal", "High Solar", "Evening Stress", "Heat Emergency"

Profile each regime (avg temp, demand, renewable %, time-of-day distribution)



**Days 4-7: HMM for Regime Transitions (OPTIONAL)**



If K-means works well, add HMM

Learn transition probabilities

Analyze: Which regimes follow which?

Duration analysis: How long in each regime?



Deliverable: Regime assignments + transition analysis



**--- MID-EVALUATION: This should be complete... NO EXCUSES ---**



###### **Week 4: Renewable Variability Analysis** 



**Days 1-3: Forecast Error Analysis**



Expected solar/wind: Historical average for hour/day/season

Actual solar/wind: From CAISO data

Error = Actual - Expected

Distribution analysis (when are errors largest?)



**Days 4-5: Mismatch Risk Scoring**



Combine: renewable\_forecast\_error + demand\_level + reserve\_margin

Create continuous risk score

Identify high-risk hours



**Days 6-7: Connect to Regimes**



Which regimes have highest renewable uncertainty?

Does forecast error predict regime transitions?



Deliverable: Renewable variability characterization + risk scores



**--- MID-EVALUATION: Try to complete till this part ---**



###### **Week 5: Grid Interpretation \& Policy**



**Days 1-3: SHAP Analysis**



Feature importance for anomaly detection

Feature importance for stress prediction (if you add XGBoost predictor)

Global and local explanations



**Days 4-5: Climate Sensitivity**



Temperature effects by regime

Solar/wind variability by season

Correlation analysis (NOT causal ML, just honest correlation)



**Days 6-7: Grid Policy Recommendations**



When do stress events occur? (summer evenings)

What predicts them? (temperature, hour, renewable share)

Operational recommendations (reserve activation, demand response timing)



Deliverable: Grid analysis synthesis report



##### **PART 2: BUILDING ENERGY ANALYSIS - 3 WEEKS**



###### **Week 6: Building Data Prep + Clustering**



**Days 1-2: Data Cleaning**



Load Southern California building dataset

Handle missing values

Feature engineering: EUI (energy per sqft), peak\_hour, load\_factor

Normalize features



**Days 3-5: K-Means Building Clustering**



Features: energy\_consumption, building\_type, HVAC\_consumption, lighting\_consumption, occupancy\_rate, energy\_star\_equivalent

Optimal k (5-8 clusters)

Profile clusters: Average characteristics, dominant building types



Example expected clusters:



Cluster 1: "Old inefficient commercial" (high HVAC, low occupancy)

Cluster 2: "Efficient modern residential" (low consumption, good load factor)

Cluster 3: "Industrial high-demand" (24/7 operation, high baseline)

Cluster 4: "Standard commercial" (9-5 weekday peaks)

Cluster 5: "Variable residential" (evening/weekend peaks)



**Days 6-7: Cluster Validation**



Silhouette score

Within-cluster vs between-cluster variance

Visual inspection (t-SNE or PCA projection)



Deliverable: Building archetypes with profiles



###### **Week 7: Building Behavior Analysis**



**Days 1-3: Temporal Patterns by Cluster**



Average daily load curves per cluster

Weekend vs weekday differences

Seasonal patterns (summer vs winter)

Peak hour distribution (which clusters peak 5-8pm?)



**Days 4-5: Feature Importance**



Random Forest: Predict energy\_consumption from building features

SHAP analysis per cluster

"Why is Cluster 1 inefficient?" → Old HVAC + poor insulation + oversized systems



**Days 6-7: Inefficiency Quantification**



Energy waste estimation per cluster

Savings potential if upgraded to best-in-class

ROI calculation for retrofits



Deliverable: Building behavior analysis + efficiency opportunities



###### **Week 8: Building Regime Detection (OPTIONAL)**



If you have time and want extra depth:

**Days 1-3: Building Operational Regimes**



Cluster building operational states (not buildings themselves, but their hourly states)

Features: energy\_consumption, HVAC\_ratio, occupancy\_rate, thermal\_comfort

States: "Low use", "Normal", "Peak", "Inefficient high-use"



**Days 4-5: Regime Analysis**



Which buildings frequently enter "inefficient" states?

Time-of-day patterns per regime

Connection to outdoor temperature



**Days 6-7: Transition Analysis**



Do buildings transition smoothly or abruptly?

What triggers inefficient states? (temperature extremes? occupancy spikes?)



Deliverable: Building regime timeline + patterns

NOTE: This is optional. Only do if Weeks 6-7 go smoothly.



##### **PART 3: BUILDING-GRID CONNECTION - 2 WEEKS**



###### **Week 9: Temporal Alignment Analysis**



**Days 1-3: Aggregate Building Demand by Cluster**



Sum hourly energy consumption for all buildings in each cluster

Create time series: cluster\_1\_demand(t), cluster\_2\_demand(t), etc.

Align with CAISO grid stress hours



**Days 4-5: Peak Overlap Analysis**



Grid stress hours: 5-8pm summer weekdays (example)

Building peak hours by cluster

Calculate: % of cluster demand occurring during grid stress hours



Example finding:

"Cluster 1 (old commercial) shows 68% of annual peak demand during grid stress hours, compared to 32% for Cluster 2 (modern residential)"

Days 6-7: Correlation Analysis



Pearson correlation: cluster\_demand vs grid\_stress\_indicator

Lag analysis: Do building peaks precede or follow grid stress?

Seasonal breakdown: Summer vs winter patterns



Deliverable: Building-grid temporal alignment analysis



###### **Week 10: Impact Quantification \& Policy**



**Days 1-3: Stress Contribution Scoring**



Method:

For each cluster, calculate:

stress\_contribution\_score = (

&nbsp;   avg\_demand\_during\_stress × 0.4 +

&nbsp;   peak\_overlap\_percentage × 0.3 +

&nbsp;   demand\_variability × 0.3

)

Output:

Ranking of clusters by contribution to grid stress

Days 4-5: Scenario Analysis

"What if we improve Cluster 1 efficiency by 20%?"



Estimated demand reduction during stress hours

Impact on grid stress frequency (rough estimate)

Policy insight: Prioritize Cluster 1 for demand response programs



**Days 6-7: Integrated Policy Recommendations**



Grid-level:



When to activate reserves (regime-based triggers)

Renewable curtailment management

Storage deployment timing



Building-level:



Which clusters to target for efficiency programs

Demand response timing (5-8pm, summer)

Time-of-use pricing impacts



Connection:



Target Cluster X buildings for demand response during grid Evening Stress regime

Estimated system-wide impact: 500-800 MW demand reduction



Deliverable: Integrated policy brief (8-12 pages)



##### **PART 4: DASHBOARD \& FINAL DELIVERABLES - 4 WEEKS**



###### **Week 11-12: Backend + Database (SDE person)**



Backend:



Flask/FastAPI

Data ingestion from CAISO + building datasets

Preprocessing pipeline

Model serving (load trained models)



Database:



PostgreSQL or MongoDB

Schema: time\_series\_grid, time\_series\_buildings, anomaly\_scores, regime\_assignments, cluster\_assignments



API Endpoints:



/grid/anomaly\_score?date=2024-01-15 → Returns anomaly score

/grid/current\_regime → Returns current grid regime

/buildings/clusters → Returns cluster profiles

/integrated/stress\_contributors → Returns building clusters ranked by grid stress contribution





###### **Week 13: Frontend Dashboard (SDE person)**



Page 1: Grid Stress Monitor



Real-time demand, temperature, stress indicator

Anomaly timeline (2018-2024)

Current regime with visual indicator

Renewable generation vs demand



Page 2: Regime Analysis



Regime timeline (colored bars)

Transition probability matrix (heatmap)

Climate distributions per regime (box plots)

Regime frequency by month/hour (heatmap)



Page 3: Building Archetypes



Cluster scatter plot (t-SNE visualization)

Cluster profiles table

SHAP feature importance per cluster

Example buildings from each cluster



Page 4: Building-Grid Connection



Temporal overlap visualization

Stress contribution ranking

Scenario simulator ("What if Cluster X improves 20%?")

Policy recommendations



Tech Stack: React + Plotly OR simple HTML/CSS/JS + Chart.js



###### **Week 14: Final Report + Presentation**



Report Structure (40-50 pages):



Introduction (grid stress problem, California context)

Literature Review (anomaly detection, regime analysis, building-grid integration)

Data Description (CAISO + building datasets)

Methodology:



Grid anomaly detection (autoencoder, baselines)

Grid regime detection (K-means, HMM)

Building clustering

Building-grid connection





Results:



Grid analysis findings

Building analysis findings

Integrated insights





Policy Recommendations

Limitations \& Future Work

Conclusion



Presentation (20 slides):



Problem motivation

Data overview

Key methods (1 slide per: anomaly detection, regime detection, building clustering)

Results highlights

Dashboard demo

Policy recommendations

Q\&A



##### **PART 5: STATISTICAL RIGOR LAYER (OPTIONAL ADVANCED) - 3 WEEKS**



###### **Week 15: Uncertainty Quantification \& Confidence Intervals**



**Days 1-2: Conformal Prediction**



What you're doing:

Add guaranteed coverage intervals to stress predictions

Method:



Split data: Train (60%), Calibration (20%), Test (20%)

Train XGBoost on training set

Use calibration set to compute conformal scores

Generate prediction intervals with 90% guaranteed coverage



Output:



Instead of: "Stress probability = 0.73"

Now: "Stress probability = 0.73, 90% interval: \[0.61, 0.84]"



Validation:



Check empirical coverage: Does 90% interval actually cover 89-91% of cases?

Stratify by regime: Does coverage hold in all regimes?



Deliverable: Coverage analysis plots, prediction intervals for all forecasts



**Days 3-4: Bootstrap Confidence Intervals**



What you're doing:

Construct CIs for key statistics using resampling

Statistics to bootstrap:



Mean demand during stress events ± 95% CI

Regime transition probabilities ± 95% CI

Temperature sensitivity coefficient ± 95% CI

Mean EUI per building cluster ± 95% CI



Method:



Resample data 1000 times with replacement

Calculate statistic on each sample

CI = 2.5th to 97.5th percentile of bootstrap distribution



Deliverable: Table of key statistics with bootstrap CIs, distribution plots



**Days 5-6: Calibration Analysis**



What you're doing:

Check if predicted probabilities match observed frequencies

Method:



Bin predicted probabilities (0-0.1, 0.1-0.2, ..., 0.9-1.0)

For each bin: What % actually experienced stress?

Plot reliability diagram (predicted vs observed)

Calculate Expected Calibration Error (ECE)



Stratified calibration:



By regime (Evening Stress vs Normal)

By season (summer vs winter)



Recalibration (if needed):



Apply Platt scaling or isotonic regression

Compare before/after ECE



Deliverable: Reliability diagrams, ECE scores, recalibrated model if needed



**Day 7: Integration \& Reporting**



What you're doing:

Synthesize uncertainty quantification results

Deliverable:



Summary report: "Uncertainty Quantification Framework"

Comparison table: Conformal vs Bootstrap vs Calibration approaches

Interpretation guide: "How to use prediction intervals operationally"





###### **Week 16: Hypothesis Testing Framework**



**Days 1-2: Research Hypotheses Formulation**



What you're doing:

Convert research questions into testable statistical hypotheses

Grid-level hypotheses:

H1: Climate Sensitivity Differs by Regime



Null: Temperature effect on demand is same across all regimes

Alternative: Temperature effect varies by regime

Test: ANOVA or Kruskal-Wallis



H2: Renewable Forecast Errors Are Heteroskedastic



Null: Forecast error variance is constant over seasons

Alternative: Variance differs by season

Test: Levene's test or Breusch-Pagan



H3: Evening Stress Regime Has Higher Temperature



Null: Mean temperature same in Evening Stress vs Normal regime

Alternative: Evening Stress has higher mean temperature

Test: Two-sample t-test or Mann-Whitney U



Building-level hypotheses:

H4: Building Clusters Have Different Peak Hours



Null: All clusters peak at same hours

Alternative: Different clusters have different peak hour distributions

Test: Chi-squared test of independence



H5: HVAC Consumption Drives Total Energy Use



Null: HVAC consumption has no effect on total consumption

Alternative: HVAC significantly predicts total consumption

Test: Linear regression with F-test



Deliverable: List of 6-8 hypotheses with justification



**Days 3-5: Hypothesis Testing Execution**



What you're doing:

Conduct statistical tests with proper procedures

For each hypothesis:



State null and alternative

Check assumptions (normality, equal variance, independence)

Choose appropriate test (parametric vs non-parametric)

Calculate test statistic and p-value

Compute effect size (Cohen's d, eta-squared, R-squared)

Apply multiple testing correction (Bonferroni or Benjamini-Hochberg)



Example output for H1:

H1: Climate Sensitivity Differs by Regime

\- Test: One-way ANOVA

\- F-statistic: 247.3, p < 0.001

\- Effect size: η² = 0.34 (large effect)

\- Post-hoc: Tukey HSD shows Evening Stress > Normal > High Solar (all p < 0.01)

\- Conclusion: Reject null, temperature sensitivity varies significantly by regime

Deliverable: Test results table with statistics, p-values, effect sizes, interpretations



**Days 6-7: Hypothesis Testing Report**



What you're doing:

Write formal hypothesis testing section for report

Structure:



Introduction: Research questions

Methods: Tests used, assumptions checked, corrections applied

Results: Table of all tests with statistics

Discussion: What do findings mean for grid operations?



Deliverable: Hypothesis testing section (5-8 pages) with tables and interpretation



###### **Week 17: Causal Inference Layer**



**Days 1-2: Granger Causality Tests**



What you're doing:

Test if variable X helps predict Y beyond Y's own history

Causal questions:

Q1: Does Temperature Granger-Cause Demand?



Compare: AR model (demand ~ lagged\_demand) vs VAR model (demand ~ lagged\_demand + lagged\_temp)

F-test: Does adding lagged temperature improve prediction?

Lag selection: Test 1h, 6h, 12h, 24h lags



Q2: Does Renewable Forecast Error Granger-Cause Price Spikes?



Test if renewable errors predict future price movements



Q3: Does Building Consumption Granger-Cause Grid Stress?



Aggregate building demand → test if it predicts grid stress



Method:



Use statsmodels.tsa.stattools.grangercausalitytests

Report: F-statistic, p-value, optimal lag

Interpret: "Temperature Granger-causes demand with 6-hour lag (F=124.5, p<0.001)"



Deliverable: Granger causality matrix (which variables cause which), lag structure analysis



**Days 3-4: Propensity Score Matching (OPTIONAL)**



What you're doing:

Estimate causal effect of building efficiency on grid stress contribution

Challenge:

You don't have interventional data (no before/after efficiency upgrades)

Workaround:



Treatment group: High-efficiency buildings (Cluster 2)

Control group: Low-efficiency buildings (Cluster 1)

Match buildings on: Size, age, location, occupancy

Compare: Grid stress contribution between matched pairs



Method:



Compute propensity scores (probability of being high-efficiency given covariates)

Match treatment to control units with similar propensity scores

Estimate Average Treatment Effect (ATE)



Assumptions (explicitly state):



Strong ignorability (no unobserved confounders)

Common support (overlap in propensity scores)

SUTVA (no interference between units)



Deliverable:



Propensity score distribution plots

Balance checks (are matched groups similar on covariates?)

ATE estimate with 95% CI

Sensitivity analysis (how robust is estimate to hidden confounding?)





**Days 5-6: Causal Graph \& Structural Equations**



What you're doing:

Formalize causal assumptions using directed acyclic graphs (DAGs)

Example causal graph:

Temperature → Cooling Demand → Grid Demand → Grid Stress

&nbsp;             ↓

&nbsp;          Solar Output (inverse relationship)

&nbsp;             ↓

&nbsp;          Grid Demand → Grid Stress



Building HVAC Efficiency → Building Consumption → Grid Demand → Grid Stress



Renewable Forecast Error → Reserve Activation → Grid Stress (inverse)

What you do:



Draw DAG using dagitty or manually

Identify: Confounders, mediators, colliders

Determine: Minimal adjustment set for causal effect estimation

State: Which effects are identifiable vs not



Structural equations (if time):

Demand\_t = β₀ + β₁·Temp\_t + β₂·Solar\_t + ε\_t

Stress\_t = γ₀ + γ₁·Demand\_t + γ₂·Renewables\_t + η\_t

Deliverable: Causal DAG diagram, identification analysis, structural equation specifications



**Day 7: Causal Inference Summary**



What you're doing:

Synthesize causal findings with explicit caveats

Structure:



Methods: Granger causality, propensity scores, causal graphs

Results: What causal relationships were found?

Assumptions: What must be true for these to be valid?

Limitations: What prevents stronger causal claims?

Interpretation: Distinguish correlation vs causation carefully



Key caveat to include:

"We use Granger causality to establish predictive relationships and propensity score matching to estimate associational effects under strong assumptions. True causal effects would require experimental manipulation or stronger identification strategies (e.g., natural experiments, instrumental variables) which are unavailable in our observational data."

Deliverable: Causal inference section (6-10 pages) with explicit assumptions and limitations

