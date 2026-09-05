# secom-yield-optimization
Semiconductor yield prediction and inspection optimization using SECOM dataset

## Background

A complex semiconductor manufacturing process is monitored through 
hundreds of sensors and process measurement points. However, not all 
of these signals are equally valuable — the measurements contain a mix 
of useful information, irrelevant information, and noise, and engineers 
typically have far more signals available than are actually needed to 
detect a defect.

This creates a two-sided problem. First, an **inspection capacity 
constraint**: no factory can afford to run detailed quality inspection 
on every single unit, so engineers must decide which units to prioritize 
for inspection. Second, a **prediction problem**: sensor readings alone 
don't directly tell you whether a unit will pass or fail — a model needs 
to estimate that risk.

Most public projects using this dataset stop at the prediction step, 
reporting accuracy or F1 score on a held-out test set. But a probability 
score by itself doesn't tell a factory what to *do*. This project treats 
prediction as an input to a downstream decision: given limited inspection 
capacity, which units should actually be inspected to minimize the 
expected cost of missed defects?

**Dataset**: [SECOM Dataset](https://archive.ics.uci.edu/dataset/179/secom) 
(UCI Machine Learning Repository, McCann & Johnston, 2008) — 1,567 
production units, 590 anonymized sensor features, and a pass/fail label 
(1,463 pass / 104 fail), collected from a real semiconductor fabrication line.
