# HW3: Visualization, Segments, and Your First Classifier

**Due:** Thursday, November 5, 11:59 PM on Gradescope
**Points:** 100
**Work:** individual

Three parts, one notebook. Part 1 is matplotlib and seaborn practice on a cars dataset we hand you. Parts 2 and 3 go back to the dataset you picked in HW2: Part 2 is visual EDA and one claim you prove is not luck, Part 3 is segments with KMeans and a classifier you learn to distrust. Everything you need was covered on Day 3. Everything goes in `DSE200_HW3.ipynb`.

## Getting the notebook

The course repo is https://github.com/DSE200-2026/DSE200 and the notebook is `DSE200_HW3.ipynb` inside it. Two ways to open it, pick whichever you like.

**In Colab.** Go to File, then Open notebook, then the GitHub tab. Paste the repo URL and pick `DSE200_HW3.ipynb`. Before you type anything, do File, Save a copy in Drive. If you skip that step your work vanishes when you close the tab. The first cell installs everything you need.

**On your own machine.** Same setup as HW1. If you already have the repo and the virtual environment, pull and install the new packages:

```
cd DSE200
git pull
source .venv/bin/activate          # Windows: .venv\Scripts\activate
uv pip install jupyter numpy pandas matplotlib seaborn scipy scikit-learn
jupyter notebook DSE200_HW3.ipynb
```

Starting fresh? Follow the HW1 instructions for `uv venv`, then run the install line above.

**The data.** Part 1 downloads `cars.csv` from the course repo when you run the setup cell. If that fails, grab it from https://github.com/DSE200-2026/DSE200/blob/main/cars.csv and put it next to the notebook. Parts 2 and 3 use your HW2 Kaggle CSV. In Colab, upload it with the folder icon on the left.

Work in your own copy. Don't push back to the course repo.

## Part 1: Matplotlib and seaborn on cars (45 pts)

Six sections on about 5,000 cars from model years 2009 to 2012. Each question has a cell marked `YOUR CODE HERE`. Every plot gets a title and labeled axes.

- **Inspect (4 pts).** Unique car IDs, then unique ID and year pairs.
- **Distributions (9 pts).** Histogram with a density line for highway mpg, one bin per value. Then city mpg and horsepower.
- **Correlation (9 pts).** Horsepower against highway mpg with a line of best fit. Find and remove the outlier, redo it. Then horsepower against torque.
- **Subplots (10 pts).** One 2 x 2 figure: box plot, pie chart, histogram, and a scatter with marker size carrying a third column.
- **Heatmap (8 pts).** Top 8 makes against year plus transmission (`2009-AT`), counts in each cell. Most of the work is pandas, not plotting.
- **Pair plot (5 pts).** Six columns in seaborn, then say which pairs move together and which move opposite.

You don't need to explain your approach unless a question asks for it. Both the code and the answer have to be right for full marks.

## Part 2: Visual EDA on your project dataset (25 pts)

Same dataset as HW2 Parts 4 and 5. If you've switched since then, say so in 2.1 and say why.

### 2.1 The first five minutes (5 pts)

Shape, dtypes, missing values per column **and per row**, and `describe()`. Reuse your `load_clean` from HW2 if you have it. Then one sentence: the one thing in that output you'd have gotten wrong if you had skipped it.

### 2.2 Three figures whose title is the finding (12 pts)

Three figures, 4 points each:

1. Your target column. Print the mean and the median and say which you'd report.
2. A numeric feature against the target.
3. A categorical feature against the target, grouped and sorted.

The title states the finding. "Fare by class" is a label. "Third class paid a seventh of the first class fare" is a finding. Bars sorted, value axes start at zero, units in the axis labels. One sentence under each: what it shows and why it matters for your prediction task.

### 2.3 Not luck (8 pts)

Pick one group difference, from 2.2 or a new one, and run the shuffle test from Day 3. The notebook gives you `shuffle_test(data, col, target)`. Then two sentences: the gap you found, and what share of shuffles matched it.

0 to 1 percent means you found something. Over 5 percent means you haven't yet. Saying so plainly is a full-credit answer. Claiming a finding the shuffle test doesn't support is not.

## Part 3: Segments and a classifier (30 pts)

### 3.1 Segments with KMeans (10 pts)

1. Pick 2 to 4 numeric columns, scale them with `StandardScaler`, and plot inertia for k = 2 to 8 (3 pts).
2. Pick k and fit `KMeans(n_clusters=k, random_state=42, n_init=10)`. Show a `groupby` table: rows per segment, the median of each clustering column, and the mean of your target (4 pts).
3. Name each segment in one sentence a colleague would recognise (3 pts). If you can't, say so and why. Arithmetic you can't name is not a finding.

Forget to scale and the column with the biggest numbers decides everything. Day 3 section 6.8 showed what that looks like.

### 3.2 A classifier (15 pts)

HW2 predicted a number. Now predict a yes or a no.

- **The label (3 pts).** A binary column already in your data, or one you make from your HW2 target with a threshold you can defend: "price above the median", "delay over 15 minutes". Say what 1 means and what share of rows are 1. If you built the label from your target, drop the target from the features. It is the answer.
- **Split (2 pts).** `train_test_split(X, y, test_size=0.2, random_state=0, stratify=y)`.
- **Baseline (2 pts).** `DummyClassifier(strategy="most_frequent")`, accuracy on the test set.
- **Two models (5 pts).** `LogisticRegression(max_iter=1000)` and `DecisionTreeClassifier(max_depth=4, random_state=0)`. For each, test accuracy and **positives missed** (actual 1, predicted 0), from `confusion_matrix(...).ravel()`. One table with the baseline and both models.
- **Overfitting (3 pts).** Train and test accuracy for an unlimited tree (`max_depth=None`).

### 3.3 What the numbers hide (5 pts)

Three short paragraphs:

1. Which model you'd carry forward, with the evidence in positives missed, not only accuracy.
2. The train and test gap for the unlimited tree, and what it means.
3. Do the logistic regression coefficients agree with what you found in Part 2? Coefficients are per unit of each feature, so compare signs, not sizes, unless you scaled.

A model that barely beats the baseline is not a failed assignment if you can say why. One that beats it by a suspicious margin usually has a leak. Find it.

## What to submit

Two files on Gradescope by 11:59 PM on Thursday, November 5:

1. `DSE200_HW3.ipynb`, with every cell run and outputs saved. Runtime, then Run all, then save. If you're in Colab, File, Download, .ipynb gets it out.
2. The CSV you used in Parts 2 and 3. If it's the same file you submitted for HW2, submit it again anyway.

Don't submit `cars.csv`.

## Grading

| | pts |
| --- | --- |
| Part 1: Inspect | 4 |
| Part 1: Distributions | 9 |
| Part 1: Correlation | 9 |
| Part 1: Subplots | 10 |
| Part 1: Heatmap | 8 |
| Part 1: Pair plot and reading | 5 |
| Part 2: First five minutes | 5 |
| Part 2: Three figures with finding titles | 12 |
| Part 2: Shuffle test and the two sentences | 8 |
| Part 3: Segments, table, and names | 10 |
| Part 3: Label, split, baseline, two models, overfitting | 15 |
| Part 3: Three paragraphs | 5 |
