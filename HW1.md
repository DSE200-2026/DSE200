# HW1: Python, NumPy, and How Python Holds Data

**Due:** Thursday, October 8, 11:59 PM on Gradescope
**Points:** 100
**Work:** individual

Two parts, one notebook. Part 1 is fifteen short Python and NumPy exercises plus a puzzle. Part 2 is the real work: find a messy real-world dataset, clean it, and load it into memory a few different ways so you can see what each container does for you and what it costs you. Everything goes in `DSE200_HW1.ipynb`.

## Getting the notebook

The course repo is https://github.com/DSE200-2026/DSE200 and the notebook is `DSE200_HW1.ipynb` inside it. Two ways to open it, pick whichever you like.

**In Colab.** Go to File, then Open notebook, then the GitHub tab. Paste the repo URL and pick `DSE200_HW1.ipynb`. Before you type anything, do File, Save a copy in Drive. If you skip that step your work vanishes when you close the tab. Nothing to install.

**On your own machine.** Clone the repo and run Jupyter. We recommend `uv`, it handles Python versions and packages in one tool and it's fast. Install it once from https://docs.astral.sh/uv/getting-started/installation/ (on a Mac, `brew install uv` also works). Then:

```
git clone https://github.com/DSE200-2026/DSE200.git
cd DSE200
uv venv --python 3.12
source .venv/bin/activate          # Windows: .venv\Scripts\activate
uv pip install jupyter numpy pandas matplotlib
jupyter notebook DSE200_HW1.ipynb
```

If you'd rather not use `uv`, plain Python works too. You need 3.10 or newer, then `pip install jupyter numpy pandas matplotlib` and the same `jupyter notebook` command. Either way, keep it in a virtual environment. Installing into your system Python is how you end up with two broken Pythons by week 3.

**The data for Part 1.** The Final Challenge cell downloads `noisy_data.npy` for you. If that fails, grab it here and put it next to the notebook:

- On GitHub: https://github.com/DSE200-2026/DSE200/blob/main/noisy_data.npy
- Raw file, for code: https://raw.githubusercontent.com/DSE200-2026/DSE200/main/noisy_data.npy

```python
import urllib.request
urllib.request.urlretrieve(
    "https://raw.githubusercontent.com/DSE200-2026/DSE200/main/noisy_data.npy",
    "noisy_data.npy",
)
```

Work in your own copy. Don't push back to the course repo.

## Part 1: Python and NumPy (30 pts)

Fifteen short exercises and a puzzle, all in the notebook. Each one has a cell marked `COMPLETE THE CELL BELOW`. Write your code there.

- **Python basics, 1 through 10.** Variables and types, a couple of functions, loops, string handling, and one small class. Nothing you haven't seen in lecture. Some cells have starter code with blanks, fill the blanks. Some are empty, write it from scratch.
- **NumPy, 11 through 15.** Random arrays, transpose and inverse, slicing, broadcasting, reshaping. Read the hint in each one, it names the function you want.
- **Final Challenge.** There's a message hidden in `noisy_data.npy`. Plot it, find the spikes, decode them.

You don't need to explain your approach unless a question asks for it. Both the code and the answer have to be right for full marks.

Before you submit, run everything from the top (Runtime, then Run all) and save so the outputs are in the file.

If you're stuck on a cell for more than 15 minutes, come to office hours or post on the discussion board.

## Part 2: One dataset, four containers (70 pts)

### Step 1: Find a dataset (10 pts)

- Between 500 and 50,000 rows, in a file you can open in a text editor. CSV, TSV, or Excel. No APIs, no databases, no PDFs this time.
- At least 5 columns, and at least 2 of them numeric.
- You have to be able to answer all three of these: where did it come from (a URL), what is it supposed to represent, and what license is it under. If you can't answer all three, pick a different one.

Post the link on Rippple by Thursday, October 1.

Write this up in a markdown cell under the "Step 1" heading: those three answers, the row and column count, and three sentences on why you think it's messy.

### Step 2: Clean it (20 pts)

Write a function `clean(raw_path, clean_path)` in a code cell. It reads the raw file and writes a clean one. Have it print rows in, rows out, and what got dropped.

Colab tip: upload the raw file with the folder icon on the left, or drop it in your Drive and mount it. Locally, just put it next to the notebook.

Things you'll probably run into, roughly in the order they bite:

| Problem | What it looks like |
| --- | --- |
| Column names | `Total Amount $`, `total_amount`, trailing spaces |
| Numbers stored as text | `"1,234"`, `"$45.00"`, `"12 kg"`, `"N/A"` |
| Dates | `03/04/2023` next to `2023-04-03` next to `Apr 3, 2023` |
| Missing values | empty, `NA`, `N/A`, `-`, `999`, `unknown`, or `0` where 0 can't be right |
| Duplicates | the same row twice, or twice with one field different |
| Junk rows | the header repeated in the middle, a totals row at the bottom, blank lines |
| Encoding | `Ã©` where `é` should be |

### Step 3: Load it four ways (25 pts)

**A. List of dicts.** One dict per row, keys are the column names.

```python
rows = [{"city": "San Diego", "temp": 21.4}, ...]
```

**B. Dict of lists.** One key per column, each holding a list of every value in that column.

```python
cols = {"city": ["San Diego", ...], "temp": [21.4, ...]}
```

**C. NumPy.** Numeric columns only. Pick your dtypes deliberately and say why you picked them.

**D. pandas.** A DataFrame, the normal way: `pd.read_csv` on your cleaned file.

Now ask the same three questions of all four containers. The answers have to match.

1. A filter. How many rows match some condition.
2. A group. Average or count of something, per category.
3. A sort. Top 10 rows by some column.

### Step 4: Compare them (15 pts)

Measure two things for each of the four versions:

- **Memory.** For A and B, use `pympler.asizeof` or write a small recursive sizer yourself. Plain `sys.getsizeof` on a list only counts the pointers, not the objects they point to, so it'll be off by 10x or more. For C use `arr.nbytes`. For D use `df.memory_usage(deep=True).sum()`.

  Pympler isn't installed by default. In a notebook, put this in a cell and run it once:

  ```python
  %pip install pympler
  from pympler import asizeof
  asizeof.asizeof(rows)
  ```

  From a terminal it's just `pip install pympler`.
- **Time.** How long each of your three questions took. Use `timeit` and run it several times. One run mostly measures noise.

Put the numbers in a markdown table. Then answer these in markdown:

1. Which container would you actually use for this dataset, and why?
2. A is a list of dicts. Where did that cost you: memory, speed, or how much code you had to write?
3. B is a dict of lists. Same data, different shape. Which of your three questions got easier and which got harder?
4. What did you have to give up to get the data into NumPy, and what did you get back?
5. Describe one dataset where you'd pick something other than pandas, and say why.

Then two short experiments. These are about how Python holds data, not about your dataset:

**Mutation.** Pull one row out of your list of dicts into a variable. Change a value on it. Then look at the original list.

```python
row = rows[0]
row["temp"] = 999
print(rows[0])   # explain what you see
```

**Copying.** Same thing, but with `copy.copy` and then `copy.deepcopy`. Explain the difference and say which one you'd actually want here.

### Step 5: Write it up

At the end, write about:

- What you found.
- What you did about it.
- What you left alone and why.
- If you dropped rows, how many and what they were.

## What to submit

Two files on Gradescope by 11:59 PM on Thursday, October 8:

1. `DSE200_HW1.ipynb`, with every cell run and outputs saved. Runtime, then Run all, then save. If you're in Colab, File, Download, .ipynb gets it out.
2. Your raw data file


## Grading

| | pts |
| --- | --- |
| Part 1 exercises correct, Final Challenge decoded | 30 |
| Dataset is actually messy and properly sourced | 10 |
| Cleaning function handles the real problems | 20 |
| Four containers work and agree on all three questions | 25 |
| Comparison is measured, and the reasoning holds up | 15 |
