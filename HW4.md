# HW4: One New Model on the Fraud Data

**Due:** Thursday, November 12, 11:59 PM on Gradescope
**Points:** 100 (+5 bonus)
**Work:** individual

One notebook, four short parts. You take the Day 3 fraud data, which you already know, and fit one of the Day 4 models, XGBoost, on it. The features, the split and a baseline are built for you in the setup cell, so the work is the Day 4 part: fit it honestly, turn it into dollars, ask it why, and say what more modelling could and couldn't buy. This homework should take much less time; the project is the big job these two weeks.

## Getting the notebook

The course repo is https://github.com/DSE200-2026/DSE200 and the notebook is `DSE200_HW4.ipynb` inside it.

**In Colab.** File, then Open notebook, then the GitHub tab. Paste the repo URL and pick `DSE200_HW4.ipynb`. Then File, Save a copy in Drive before you type anything. The first cell installs what you need.

**On your own machine.** Pull the repo and install into the virtual environment from HW1:

```
cd DSE200
git pull
source .venv/bin/activate          # Windows: .venv\Scripts\activate
uv pip install jupyter numpy pandas matplotlib scikit-learn xgboost
jupyter notebook DSE200_HW4.ipynb
```

**The data.** The setup cell downloads `fraud_training.csv` from the course repo. If that fails, get it from https://github.com/DSE200-2026/DSE200/blob/main/fraud_training.csv and put it next to the notebook.

Don't change the setup cell: everyone uses the same features and the same split, so your numbers can be compared.

## The setup cell

It builds the Day 3 customer features (`amount_ratio`, `mins_since_prev`, `new_merchant`, and the rest), then splits by time the way Day 4 split the weather years:

| Months | Name | Job |
| --- | --- | --- |
| January to June | `fit` | trains the model |
| July | `tune` | early stopping watches it |
| August and September | `test` | scored once, at the end |

It also fits the baseline to beat, Day 3's logistic regression, and gives you `net_dollars()` from the challenge.

## Part 1: Fit XGBoost (30 pts)

Fit the exact model given in the notebook, with early stopping on July. Print `best_iteration`, and PR-AUC on the test months next to the baseline's. Then one sentence: why does early stopping watch July and not the test months?

## Part 2: Turn it into dollars (30 pts)

One table of net dollars on the test months: approve everything, the baseline at the cost threshold, XGBoost at 0.5, and XGBoost at the cost threshold (flag when P(fraud) > 0.02 / 1.02, from the Day 3 cost table). Then explain why XGBoost at 0.5 does badly when its PR-AUC is the best in the table.

## Part 3: Ask it why (20 pts)

Permutation importance on the test rows, scored by PR-AUC (Day 4 section 10.3), top 8 as a bar chart. Then two sentences: do the top features make sense for fraud, and does any one look implausibly important, the way a leak would?

## Part 4: What more modelling can and cannot buy (20 pts)

Two short written answers:

1. **The ceiling.** A colleague expects AutoGluon to give a big jump in PR-AUC on the same features. What do you expect, and why? Use the Bayes optimal classifier from Day 4 section 9.5.
2. **Seeing is not doing.** A manager reads your chart and proposes making every customer wait 30 minutes between purchases. What did the model actually show, and what would you need to know before doing that?

## Bonus (5 pts)

Run AutoGluon (with `tuning_data=tune`) or TabPFN (on a sample of `fit`) on the same features and add its PR-AUC and net dollars to your Part 2 table. One sentence on what you found.

## What to submit

`DSE200_HW4.ipynb` on Gradescope by 11:59 PM on Thursday, November 12, with every cell run and outputs saved: Runtime, then Run all, then save. In Colab, File, Download, .ipynb gets it out. Don't submit the CSV.

## Grading

| | pts |
| --- | --- |
| Part 1: XGBoost fitted with early stopping on July | 15 |
| Part 1: best iteration and PR-AUC against the baseline | 10 |
| Part 1: why July | 5 |
| Part 2: net-dollar table, four strategies | 20 |
| Part 2: why 0.5 loses money | 10 |
| Part 3: permutation importance chart | 12 |
| Part 3: does it make sense, any leak | 8 |
| Part 4: the ceiling | 10 |
| Part 4: seeing is not doing | 10 |
| Bonus: AutoGluon or TabPFN | +5 |
