# Mini Project: Starbucks Offers

**Due:** Thursday, November 5, 11:59 PM on Gradescope; presentations in class Friday, November 6
**Points:** 100
**Work:** groups of 2 or 3, one submission per group

Starbucks sends offers to app users: buy-one-get-one (BOGO), discounts, and plain ads ("informational"). Not everyone gets the same offer, and not every offer works. You get one month of simulated app data: the offers, the customers, and every event (offer received, viewed, completed, and every purchase). Find out which offers work for whom, and tell Starbucks what to do about it.

Everyone works on the same data, so the comparison between groups is part of the point: same tables, different questions, different answers.

## Getting the notebook and the data

The notebook is `DSE200_MiniProject.ipynb` in the course repo, https://github.com/DSE200-2026/DSE200. Open it in Colab (File, Open notebook, GitHub tab) and do File, Save a copy in Drive before you type anything. One person in the group owns the notebook and shares it with the others.

The data comes from Kaggle, https://www.kaggle.com/datasets/ihormuliar/starbucks-customer-data. The first cell downloads it with `kagglehub`; you don't need a Kaggle account. Three tables:

| File | One row is | Columns |
| --- | --- | --- |
| `portfolio.csv` | one offer (10 of them) | `id`, `offer_type`, `reward`, `difficulty` (minimum spend), `duration` (days), `channels` |
| `profile.csv` | one customer (17,000) | `id`, `gender`, `age`, `income`, `became_member_on` |
| `transcript.csv` | one event (306,534) | `person`, `event`, `value`, `time` (hours since the start) |

`value` is a dictionary stored as text: an offer id for offer events, an amount for transactions. Parsing it is part of the job.

## What to do

### 1. Clean and join (20 pts)

Turn three tables into one you can analyze. At minimum: parse `value`, decide what one row of your analysis table is (one offer sent to one customer is the natural choice), and join the offer and customer details onto it.

Then a markdown note: what was wrong and what you did about it. There are at least three things wrong with this data that will quietly change your answers if you miss them. Look at every min and max in `describe()`, and think hard about what "offer completed" means: does a completion prove the offer worked?

### 2. Explore (25 pts)

At least four figures, each with a title that states the finding, labeled axes, and one sentence under it. Cover:

- How offers perform: completion rate by offer type, and by the individual offer.
- Who responds: completion rate across at least two customer attributes (age, income, gender, tenure).
- Channels: does adding social or web change anything?
- One figure from the transactions: spending with versus without an active offer, or anything else you can defend.

At least one of your findings gets the shuffle test from Day 3. Report the share of shuffles that matched it.

### 3. Model or segment (25 pts)

Pick at least one:

- **Predict completion.** Will this customer complete this offer? Baseline first (`DummyClassifier`), then at least two models. Report recall and precision for the positive class, not only accuracy. Split before anything else.
- **Segment customers.** KMeans on scaled customer features. Name each segment in a sentence, then show how each segment responds to each offer type.

Either way: which features mattered, and does that match what you saw in step 2?

### 4. Recommend (15 pts)

Three recommendations to Starbucks, each with the number that backs it and what you'd expect it to change. "For customers earning under $50K, send a discount instead of a BOGO: they complete discounts 51% of the time and BOGOs 40%" is a recommendation. "Personalize offers" is not.

Then one paragraph on what the data can't tell you. This data is simulated, offers were not assigned at random, and a completion is not proof the offer caused the purchase. Say which of your recommendations that weakens.

### 5. Present (15 pts)

Five minutes in class, five slides at most: the question you went after, the one figure that answers it, your model or segments in one slide, your recommendations. Every group member speaks. We'll stop you at five minutes.

## What to submit

One submission per group on Gradescope, with every member added:

1. `DSE200_MiniProject.ipynb`, every cell run, outputs saved.
2. Your slides as a PDF.

## Grading

| | pts |
| --- | --- |
| Clean and join: one analysis table, the note on what was wrong | 20 |
| Explore: four figures with findings, one shuffle-tested claim | 25 |
| Model or segment: baseline, honest metrics, what mattered | 25 |
| Recommend: three backed by numbers, one paragraph on limits | 15 |
| Present: five minutes, five slides, everyone speaks | 15 |
