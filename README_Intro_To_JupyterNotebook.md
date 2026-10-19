# Jupyter Notebook: A Simple Guide

A quick introduction to notebooks, their components and everyday data tasks.

## 1. What is Jupyter Notebook?

**Jupyter Notebook is a free, open-source web application for creating interactive documents.** A notebook combines runnable code, explanations, tables and charts in one `.ipynb` file. A **kernel** runs the code and remembers variables between cell executions. [1]

### What does “Jupyter” mean?

The name comes from **Ju**lia, **Pyt**hon and **R** — the three programming languages the project originally supported. It also supports other languages through kernels. [1]

### Why is it popular in data work?

- **Explore step by step:** run a small section and immediately inspect the result.
- **Experiment quickly:** adjust code without rerunning every earlier calculation.
- **Explain decisions:** place notes beside cleaning steps, calculations and charts.
- **Share findings:** keep the method and its results together. [1, 2]

For example, a data scientist can compare models; a data engineer can inspect missing values before testing a data transformation.

### Notebook vs Python script

| Feature | Notebook (`.ipynb`) | Python script (`.py`) |
| --- | --- | --- |
| Structure | Separate cells for code and formatted explanations | A plain-text file of code and comments |
| Running code | Run individual cells using a kernel | Usually run the file from top to bottom |
| Results | Can save tables, charts and other outputs inside the file | Outputs usually appear in a terminal or separate files/windows |
| Typical use | Exploration, learning and explaining results | Reusable programs and automated tasks |

Both run Python code. Choose the format that fits the task. [1, 2]

> **Good habit:** restart the kernel and run all cells from top to bottom before sharing. Running cells out of order can leave variables or outputs that no longer match the visible code.

## 2. Notebook Components

| Component | What it does | When to use it | Simple example |
| --- | --- | --- | --- |
| **Code cell** | Sends executable code to the kernel | Calculate, clean data or create a chart | `print(2 + 3)` |
| **Markdown cell** | Displays formatted text, headings, lists and links | Explain the aim, method or conclusion | `## Sales Analysis` |
| **Output area** | Displays results produced by a code cell | Inspect a value, table, chart or error | `5` appears below the code |

**“Output cells” usually means output areas attached to code cells.** You do not select Output as a separate editable cell type. Running a code cell generates its output; running a Markdown cell renders its text. [2]

### A tiny notebook example

**Markdown cell — explain the task:**

```markdown
## Total Sales
Add the sales from three days.
```

**Code cell — do the calculation:**

```python
sales = [10, 20, 30]
print(sum(sales))
```

**Output — inspect the result:**

```text
60
```

## 3. Common Uses

These are simple illustrative tasks you could complete in a notebook.

| Area | How a notebook helps | Simple example |
| --- | --- | --- |
| **Data Analysis** | Explore data and identify patterns | Load a sales CSV, calculate monthly totals and plot a bar chart |
| **Machine Learning** | Prepare data, train a model and compare results | Train a model to predict house prices and compare predictions with actual prices |
| **Data Engineering** | Inspect source data and prototype ETL: extract, transform, load | Read a CSV, remove duplicate rows, check missing values and save a cleaned CSV |
| **Reporting** | Combine explanations, calculations and visuals | Present monthly sales totals, a chart and a short conclusion; export as HTML |

Notebooks support interactive computation and presenting results. **nbconvert** can export notebooks to formats such as HTML and PDF, and can execute notebooks programmatically. [1–3]

### Simple Data Engineering example

This example needs **pandas** and a `sales.csv` file in the working folder.

```python
import pandas as pd

# Extract: read the source file
sales = pd.read_csv("sales.csv")

# Transform: remove duplicate rows
clean_sales = sales.drop_duplicates()

# Load: save the cleaned data
clean_sales.to_csv("clean_sales.csv", index=False)
```

Here, `index=False` prevents pandas from adding its row index as an extra CSV column. This example removes duplicates only; a real task may need additional checks. [4]

## Official Sources

1. [Project Jupyter — What is Jupyter?](https://docs.jupyter.org/en/latest/what_is_jupyter.html) — notebooks, kernels and the name’s origin.
2. [Jupyter Notebook — The Jupyter Notebook](https://jupyter-notebook.readthedocs.io/en/stable/notebook.html) — code, Markdown, execution and outputs.
3. [nbconvert — Command-line usage](https://nbconvert.readthedocs.io/en/latest/usage.html) — notebook execution and export formats.
4. [pandas — Getting started tutorials](https://pandas.pydata.org/docs/getting_started/intro_tutorials/index.html) and [drop_duplicates](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.drop_duplicates.html) — reading/writing tables and removing duplicates.

*Sources checked: 16 October 2026.*
