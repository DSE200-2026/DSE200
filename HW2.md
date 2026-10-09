# HW2: pandas, a Complete Pipeline, and Your Project Dataset

**Due:** Thursday, October 22, 11:59 PM on Gradescope
**Points:** 100
**Work:** individual

Five parts, one notebook. Parts 1 through 3 are pandas and rasterio exercises on data we hand you: Titanic passengers, beer reviews, and a satellite image of a place you pick. Part 4 is the real work: find a dataset on Kaggle, run it through a complete pipeline (load, clean, visualize, extract insights, build a basic predictor). Part 5 is one page on why that dataset and prediction task are worth anyone's time. Part 4 and Part 5 use the same dataset, and it becomes the starting point for your course project. Everything goes in `DSE200_HW2.ipynb`.

## Getting the notebook

The course repo is https://github.com/DSE200-2026/DSE200 and the notebook is `DSE200_HW2.ipynb` inside it. Two ways to open it, pick whichever you like.

**In Colab.** Go to File, then Open notebook, then the GitHub tab. Paste the repo URL and pick `DSE200_HW2.ipynb`. Before you type anything, do File, Save a copy in Drive. If you skip that step your work vanishes when you close the tab. The first cell installs everything you need.

**On your own machine.** Same setup as HW1. If you already have the repo and the virtual environment, pull and install the two new packages:

```
cd DSE200
git pull
source .venv/bin/activate          # Windows: .venv\Scripts\activate
uv pip install jupyter numpy pandas matplotlib requests pillow rasterio scikit-learn
jupyter notebook DSE200_HW2.ipynb
```

Starting fresh? Follow the HW1 instructions for `uv venv`, then run the install line above. `rasterio` ships binary wheels for Mac, Windows, and Linux, so it should install without a compiler. If it doesn't, do Part 3 in Colab.

**The data.** Parts 1 through 3 download their own data when you run the cells. Part 4 uses a CSV you download from Kaggle yourself. Kaggle needs a free account to download. Put the CSV next to the notebook, or in Colab upload it with the folder icon on the left.

Work in your own copy. Don't push back to the course repo.

## Part 1: Titanic (30 pts)

Five short sections on the Titanic passenger list, all in the notebook. Each question has a cell marked `YOUR CODE HERE`.

- **Get to know your data (4 pts).** Head, index, row count, how many rows have a missing value.
- **Summary statistics (6 pts).** `agg` and `groupby`. Min, max, mean, median of age and fare. Fare by sex. Age by sex and class.
- **Classes (6 pts).** Counts per class, one compound filter, survival rate per class.
- **Fares (7 pts).** Distinct fares, top 10 fares, filter with `isin`.
- **Ages (7 pts).** Range and mean, who sits within one standard deviation, most common ages.

You don't need to explain your approach unless a question asks for it. Both the code and the answer have to be right for full marks.

## Part 2: Beer reviews (10 pts)

Fifty thousand beer reviews, loaded for you.

- **6.1 (5 pts).** Top 15 beers by average overall rating.
- **6.2 (5 pts).** Which of palate, taste, aroma, or review length correlates most with the overall rating. Review length is the word count of the text, you'll have to make that column.

## Part 3: Geospatial data (10 pts)

Pick a bounding box at http://bboxfinder.com, and the notebook pulls a 1024 by 1024 aerial image of it from the USGS. Then three things:

1. **Show the image (3 pts).** RGB bands, displayed properly.
2. **Mask two colors (3 pts).** Green for vegetation and brown for bare soil is the obvious pair. Any two colors you can defend are fine.
3. **Measure something (4 pts).** Percent coverage of each mask, how it varies across the image, anything quantitative that uses the masks.

## Part 4: Complete pipeline on a Kaggle dataset (40 pts)

### Step 1: Find a dataset (5 pts)

- On Kaggle, at https://www.kaggle.com/datasets. One CSV file, between 1,000 and 200,000 rows, at least 6 columns.
- It has to have a numeric column you could sensibly predict from the others: a price, a score, a count, a duration. If you can't name that column in one breath, pick a different dataset.
- You have to be able to answer: where did it come from (the Kaggle URL and, if Kaggle says, the original source), what does one row represent, and what license is it under. Kaggle shows the license on the dataset page. If it says "Unknown" or "Other", pick a different one.
- Your HW1 dataset is fine if it's on Kaggle and has a target column. A new one is fine too.

Post the link on Rippple by Thursday, October 15.

Write this up in a markdown cell under the "Step 1" heading: those answers, the row and column count, and the numeric column you'll predict.

### Step 2: Load and clean (8 pts)

Write a function `load_clean(raw_path)` that reads the Kaggle CSV, fixes what's wrong, and returns a DataFrame. Have it print rows in, rows out, and what got dropped. Then a short markdown note: what was wrong, what you fixed, what you left alone.

Kaggle datasets are often cleaner than what you found for HW1. That's fine. If there's genuinely nothing to fix, say so and show the check you ran to be sure. Watch for the usual suspects anyway: wrong dtypes, sentinel values standing in for missing, duplicate rows, and columns that are just an ID.

### Step 3: Visualize (10 pts)

Four plots minimum, matplotlib or pandas `.plot`. Each gets a title, labeled axes, and one sentence under it saying what it shows.

1. Distribution of your target column.
2. One numeric feature against the target.
3. One categorical feature against the target, grouped.
4. Correlation among the numeric columns, heatmap or table.

A plot without a sentence is decoration. A sentence that just restates the title ("This shows the distribution of price") is worth zero.

### Step 4: Insights (7 pts)

Three insights. Each one is a sentence with a number in it, and the code cell that produced the number sits right above it.

```
Guess:    Older passengers paid more.
Insight:  Passengers over 50 paid a median fare of $26.00 versus $13.00 for everyone else.
```

At least one insight should be something you didn't expect going in.

### Step 5: Basic predictor (10 pts)

A baseline, one simple model, and an honest comparison.

- **Split.** `train_test_split` with `test_size=0.2, random_state=0`. Fit on train, score on test, never the other way around.
- **Baseline.** Predict the mean of the target for every row. `DummyRegressor` does exactly this. Report its score on the test set.
- **Model.** `LinearRegression`. Nothing fancier, this is not the modeling course. Numeric features only is fine. If you want a categorical column in, `pd.get_dummies` it.
- **Metric.** Mean absolute error. Same metric for baseline and model.

Then three short paragraphs in markdown:

1. Baseline score, model score, the metric. Did the model beat the baseline, and by how much?
2. Which features got the largest coefficients (`coef_`), and does that match what you saw in Step 3?
3. One thing that would make this prediction wrong in practice: a column that leaks the answer, a column that wouldn't exist at prediction time, a group the data doesn't cover.

A model that doesn't beat the baseline is not a failed assignment, as long as you can say why. A model that beats the baseline by a suspicious margin usually means a leak. Find it.

## Part 5: Project prep (10 pts)

About one page in a markdown cell, written for someone who has never seen your dataset. This is the seed of your project proposal, so write it like you mean it. Cover:

- **The question.** What are you predicting, for whom, and what decision would change if the prediction were good?
- **Why this data.** Why this dataset can answer that question. What's in it that makes the task possible, and what's missing.
- **What good looks like.** What score would someone need to see before trusting it, and how that compares to your Step 5 baseline.
- **What could go wrong.** Who is in the data and who isn't. Which columns leak the answer. Where the labels came from and whether they can be trusted.
- **Next step.** The one thing you'd do first if you kept going.

"This dataset is interesting" is not a reason. "Hospitals discharge patients without knowing who will come back within 30 days, and this dataset has 100,000 discharges with that label" is a reason.

## What to submit

Two files on Gradescope by 11:59 PM on Thursday, October 22:

1. `DSE200_HW2.ipynb`, with every cell run and outputs saved. Runtime, then Run all, then save. If you're in Colab, File, Download, .ipynb gets it out.
2. Your Kaggle CSV from Part 4

Part 3 downloads a satellite image into a `fire_data` folder. Don't submit that, we'll regenerate it from your bounding box.

## Grading

| | pts |
| --- | --- |
| Part 1: Titanic questions correct | 30 |
| Part 2: Beer reviews correct | 10 |
| Part 3: Image shown, two masks, one measurement | 10 |
| Part 4: Dataset meets the rules and is properly sourced | 5 |
| Part 4: Cleaning function and note | 8 |
| Part 4: Four labeled plots, each with a real takeaway | 10 |
| Part 4: Three insights with numbers | 7 |
| Part 4: Baseline, model, metric, and the three paragraphs | 10 |
| Part 5: One page that makes the case | 10 |
