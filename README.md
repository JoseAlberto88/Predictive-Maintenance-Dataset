# Predictive Maintenance: Catching Machine Failures Before They Happen

**A machine learning system that predicts industrial equipment failure from live sensor data, built to cut unplanned downtime, not just to score well on a metric.**

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python&logoColor=white)
![scikit--learn](https://img.shields.io/badge/scikit--learn-ML%20models-orange?logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-gradient%20boosting-informational)
![pandas](https://img.shields.io/badge/pandas-data%20wrangling-150458?logo=pandas&logoColor=white)
![Status](https://img.shields.io/badge/status-complete-brightgreen)

---

## The headline result

> Out of 2,000 machines the model had never seen, it correctly caught **80.9% of real failures**, while wrongly flagging a healthy machine only **13 times (0.65% of the fleet)**. Simply choosing a better decision threshold cut false alarms by **59% with zero additional missed failures**, no retraining required.

| What it does | Business translation |
|---|---|
| Flags at-risk machines from live sensor readings (temperature, speed, torque, tool wear) | Maintenance gets a warning **before** a machine breaks, not a repair ticket after |
| Catches 4 out of every 5 real failures | Most unplanned downtime becomes plannable, scheduled downtime |
| Wrongly flags fewer than 1 in 150 healthy machines | Technicians can trust the alerts instead of tuning them out |
| Found a specific operating condition with a **22.8× higher failure rate** | Gives maintenance teams a concrete, physical early-warning signal — not just a black-box score |
| Recommendation re-tested on an independent data split before being finalized | The result isn't a lucky draw of the data — it holds up under scrutiny |

---

## The business problem

Manufacturers manage equipment maintenance one of three ways:

- **Reactive**, fix it when it breaks. Guarantees unplanned downtime, and the most expensive kind of repair.
- **Preventive**, service on a fixed schedule. Wastes labor and parts on healthy machines, and still misses failures that happen between visits.
- **Predictive**, act on the machine's actual condition. This is what this project builds: a model that turns live operating data into an early warning, so maintenance can be triggered by real risk instead of a calendar.

Not all mistakes cost the same here. A false alarm means someone checks a healthy machine, annoying, but cheap. A missed failure means unplanned downtime, potential equipment damage, and safety exposure. Every modeling decision in this project, which metric to optimize, which threshold to operate at, which model to ship, was made with that asymmetry front and center, not by chasing the highest accuracy number.

---

## What was built

Using the AI4I 2020 industrial maintenance dataset (10,000 machines, 339 real failures), this project went through the full lifecycle of a production-grade predictive maintenance model:

1. **Data investigation**, audited the data for quality issues and, critically, for *leakage*: several columns in the raw data effectively gave away the answer and were excluded so the model would learn from genuine operating conditions instead.
2. **Pattern discovery**, found that a narrow combination of low rotational speed and low temperature differential, just 1.5% of all machines, accounted for a failure rate **22.8× higher** than normal. This became an engineered feature, not just an observation.
3. **Model comparison**, built and tuned four different modeling approaches (from a simple, transparent linear model to gradient-boosted ensembles) and compared them head-to-head on the metrics that actually matter operationally: how many failures they catch, and how many false alarms they cost.
4. **Decision threshold optimization**, most models ship with a default 50/50 cutoff. Tuning that cutoff for this specific problem cut false alarms by 59% at *no cost* in missed failures, a free win that a default configuration would have left on the table.
5. **Error analysis**, didn't stop at "the model is 81% accurate on failures." Dug into *which* failures it misses and found a specific, explainable blind spot (wear-driven failures under unusual operating conditions), turning it into a concrete recommendation for a secondary safety check.
6. **Stress-testing the recommendation**, re-ran the entire final analysis on an independently drawn slice of data to confirm the model choice wasn't an artifact of one lucky data split, and was transparent about the one place the result was less stable than it first appeared.

---

## Why this matters beyond the numbers

This project was built to answer the question a business stakeholder actually asks, *"should we trust this, and what does it cost us if we're wrong?"*, not just the question a leaderboard asks. That shows up in a few deliberate choices:

- **The model isn't the smartest one on paper, it's the most useful one operationally.** The final model wasn't the top performer on every single metric; it was chosen because it offered the best real-world trade-off between catching failures and not crying wolf.
- **Every recommendation is backed by a decision log.** Every major choice, what data to include, how to handle class imbalance, which threshold to use, is documented with the evidence considered, the alternative that was rejected, and why.
- **Findings are stress-tested, not just reported.** The final recommendation was deliberately re-checked against a second, independent data split before being finalized, and the write-up says plainly which parts held up and which parts turned out to be more sensitive than initially thought.

---

## Skills demonstrated

`Business framing of an ML problem` · `Statistical data auditing & leakage detection` · `Exploratory data analysis` · `Feature engineering from domain reasoning` · `Handling severe class imbalance` · `Model selection & hyperparameter tuning` · `Decision threshold optimization` · `Model interpretability` · `Error/misclassification analysis` · `Robustness & validation testing` · `Technical writing for non-technical stakeholders`

---

## Repository contents

```
├── notebook.ipynb          # Full analysis: code, methodology, and inline commentary
├── report.docx              # Written report — business framing, results, and recommendation
├── data/
│   └── cleaned_dataset.csv  # Final, modeling-ready dataset (see report for derivation)
└── visuals/                 # Supporting charts referenced in the report
```

> Update the paths above to match your actual repo layout before publishing.

**Start here:**
- 📄 **[report.docx](./report.docx)**, the business case, key findings, and final recommendation, written for a non-technical audience (~5 pages)
- 📓 **[notebook.ipynb](./notebook.ipynb)**, the full technical implementation, for anyone who wants to see the work

---

## Tech stack

Python · pandas · scikit-learn · XGBoost · matplotlib · Jupyter

---

*This project was completed as part of a graduate predictive analytics course. Dataset: [AI4I 2020 Predictive Maintenance Dataset](https://archive.ics.uci.edu/dataset/601/ai4i+2020+predictive+maintenance+dataset), UCI Machine Learning Repository.*
