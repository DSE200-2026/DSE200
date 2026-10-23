# Final Project

**Part 1, proposal:** Thursday, November 19, presented in class, slides on Gradescope by 11:59 PM the night before
**Part 2, analysis:** Thursday, December 3, 11:59 PM on Gradescope
**Points:** 100 (Part 1: 20, Part 2: 80)
**Work:** groups of 2 or 3, one submission per group

The final project is the whole course on data you chose: find data, clean and join it, explore it, ask one to three questions it can answer, answer them with Python, and say honestly what the answer is worth. Expect 24 to 32 hours per person across both parts. Start early: finding data that actually supports a good question is most of the work, and it's normal to throw away two or three datasets before you find one.

## How this relates to HW2 and HW3

The homework gave you practice on one Kaggle CSV. **The project has different rules**, listed below; the big one is that you need **at least two datasets you can join**. Your HW2 dataset can be one of them if it fits the rules, and your HW3 work on it carries over. You can also start fresh.

## The rules for your data

1. **At least two datasets that join in a meaningful way.** Two tables from one source (orders and customers) or two sources that share a key (county-level health data and county-level census data). Joining must add something neither dataset has alone.
2. **Open and shareable.** We have to be able to download it, and you have to be allowed to publish results about it. Kaggle, government portals, UCI, and public APIs are all fine. Your employer's data is not.
3. **Sources identifiable.** For each dataset: the URL, who collected it, what one row is, and the license.
4. **Big enough to mean something.** A few thousand rows after joining is a reasonable floor. Fifty rows can't support a model.

Where to look: Kaggle (https://www.kaggle.com/datasets), UCI (https://archive.ics.uci.edu), data.gov, data.gov.uk, the World Bank (https://data.worldbank.org), the WHO (https://www.who.int/data/gho), city open-data portals (San Diego: https://data.sandiego.gov).

## Part 1: Proposal (20 pts)

**Five minutes in class, three slides.** The point is to find out now, not in December, whether your data can answer your question.

1. **Data (slide 1).** Your datasets, their sources and licenses, what one row is in each, and the key that joins them. Show that the join works: rows before, rows after, how many failed to match.
2. **What you found (slide 2).** Your first exploration with pandas and matplotlib: one or two figures and the two or three facts that matter most, including what's broken or missing.
3. **Questions (slide 3).** One to three research questions, each with why it matters and how you'll answer it (which columns, which method). **Pick the questions; don't answer them yet.**

A good question is narrow enough to answer and broad enough to care about:

- **Too narrow:** "What was US GDP in 2011?" That's a lookup.
- **Too broad:** "What causes global poverty?" That's a dissertation, and no dataset settles it.
- **Good:** "Do movies whose reviews skew positive in the first week earn more at the box office, after accounting for budget?" Answerable with reviews joined to box-office data, and someone would care about the answer.

Upload the slides as a PDF to Gradescope by 11:59 PM the night before, so we can run them from one laptop.

### Part 1 grading

| | pts |
| --- | --- |
| Data: two or more open, sourced datasets and a working join, with the row counts | 6 |
| What you found: pandas summaries and figures that say something, issues named | 6 |
| Questions: one to three, each with why it matters and a feasible method | 6 |
| Five minutes, three slides | 2 |

We'll give feedback on your questions in class. Changing them after Part 1 is allowed and often a good idea; say what changed and why in Part 2.

## Part 2: Analysis (80 pts)

One notebook, `DSE200_FinalProject.ipynb` from the course repo, with these four sections. The steps aren't strictly in order: you'll go back to cleaning after the analysis shows you something, and that's how it should go.

### Step 1: The data (10 pts)

Every dataset: source URL, license, who collected it, what one row is, row and column counts. The code that downloads or loads it, so we can rerun it.

### Step 2: Clean, join, explore (25 pts)

- **Quality.** What's missing, broken, duplicated, or suspicious, and what you did about each. Look at every min and max.
- **The join.** Rows before and after, unmatched keys, and whether the key is unique on the side you expect.
- **Exploration.** How the data is distributed, the main trends, and the relationships between variables. Figures with titles that state findings, labeled axes, and a sentence under each.

### Step 3: Questions and analysis (30 pts)

For each question: restate it, then answer it with code. Use at least one Python library for the analysis (scikit-learn, statsmodels, scipy) and say why you picked the method. Whatever you claim, back it with the protocol from class:

- A baseline before any model, and a train/test split before anything is fit.
- The right metric: recall and precision when one class is rare, not only accuracy.
- A shuffle test or equivalent when you claim a difference between groups is real.
- Any feature must exist at the moment you'd make the prediction.

You're not graded on how sophisticated the method is or how high the score is. A linear regression you can explain beats a neural net you can't.

### Step 4: Findings and limits (15 pts)

What you learned, question by question, with the figure that shows it. Then a few paragraphs on limits: who and what the data covers and doesn't, which assumptions you made that might be wrong, and what would change your conclusions. Rarely does one analysis settle a question; say how far yours gets.

### Part 2 grading

| | pts |
| --- | --- |
| Step 1: sources, licenses, rows, reproducible loading | 10 |
| Step 2: quality issues handled, join verified, exploration with findings | 25 |
| Step 3: questions answered with code, a library, baselines, honest metrics | 30 |
| Step 4: findings tied to figures, limitations taken seriously | 15 |

## What to submit

**Part 1:** slides as a PDF, one per group, every member added on Gradescope.

**Part 2:** `DSE200_FinalProject.ipynb` with every cell run and outputs saved, plus your data files, or the code that downloads them if they're over 100 MB.

> **The course rule still applies:** every group member must be able to explain every cell you submit.
