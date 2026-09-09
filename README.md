# secom-yield-optimization

Predicting manufacturing defects and optimizing inspection decisions 
under limited resources, using the SECOM semiconductor dataset.

## Background

In many manufacturing settings, sensors record far more data than 
is actually useful, and inspecting every single unit isn't practical 
due to time or cost. This project asks two questions: (1) can we 
predict which units are likely to be defective from sensor data, and 
(2) given a limited inspection budget, which units should actually 
be inspected?

Most public projects using this dataset stop at the prediction step. 
This one goes further — using the predicted risk as input to an 
inspection allocation problem, solved as an optimization model 
with Gurobi.

**Dataset**: [SECOM Dataset](https://archive.ics.uci.edu/dataset/179/secom) 
(UCI Machine Learning Repository, 2008) — 1,567 units, 590 anonymized 
sensor features, pass/fail label (1,463 pass / 104 fail), from a 
semiconductor fabrication line.

## Methodology

1. **Data cleaning** — Removed sensors with excessive missing values 
   (>60%), imputed the rest, and flagged which sensors had missing 
   readings (as those patterns can carry signal too).

2. **Prediction** — Trained a classifier to estimate each unit's 
   fail probability. Since fails are rare (~7% of units), standard 
   training missed all of them; adjusting the decision threshold 
   improved fail detection substantially, at the cost of more false 
   alarms.

3. **Optimization** — Framed inspection allocation as a 0/1 knapsack 
   problem: given a limited inspection budget and a cost per unit, 
   which units should be inspected to minimize the expected cost of 
   missed defects? Solved with Gurobi and compared against a greedy 
   (sort-by-risk) baseline.

## Key Results

- With the default classification threshold, the model missed every 
  real fail (0% recall) — a common failure mode when the positive 
  class is rare (~7% here). Adjusting the decision threshold improved 
  fail detection to **57%** recall.

- Under the same inspection budget, the Gurobi-optimized allocation 
  caught **14 of 21** real defects in the test set, compared to 
  **12 of 21** with a simple greedy (highest-risk-first) approach — 
  a measurable improvement at no extra cost.
