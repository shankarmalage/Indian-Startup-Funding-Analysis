# Indian-Startup-Funding-Analysis.

A simple data-cleaning, analysis, and visualization script for a startup funding dataset. The main processing and plotting code is in mainn.py.&#x20;

## Table of contents

* [About](#about)
* [Features](#features)
* [Files](#files)
* [Requirements](#requirements)
* [Usage](#usage)
* [Dataset](#dataset)
* [What the script does (summary)](#what-the-script-does-summary)
* [Notes & troubleshooting](#notes--troubleshooting)
* [License & contact](#license--contact)

---

## About

This project reads a CSV of startup funding rounds, cleans and standardizes key columns, computes summary statistics (yearly/monthly totals, top sectors, cities, startups, and investors), and produces several visualizations (line plots and bar charts).

## Features

* Cleans common messy columns (dates, numeric amounts with commas/plus signs, non-ASCII characters).
* Fills missing values for important categorical fields.
* Extracts funding year and month.
* Aggregates funding by year, month, industry vertical, city, startup, investor, and investment type.
* Produces multiple matplotlib/seaborn visualizations.

## Files

* mainn.py — main script performing data cleaning, aggregation and plotting.&#x20;
* startup_funding.csv — (required) dataset file (not included in repo).

## Requirements

Recommended Python environment:

* Python 3.8+
* pandas
* matplotlib
* seaborn

Install dependencies (example):

bash
python -m venv venv
source venv/bin/activate    # Linux / macOS
venv\Scripts\activate       # Windows PowerShell
pip install pandas matplotlib seaborn


You may create a requirements.txt with:


pandas
matplotlib
seaborn


## Usage

1. Place your dataset file next to the script, named startup_funding.csv — or change the path in mainn.py.
2. Run the script. Note: mainn.py uses display() and df.info() which are notebook-friendly. For running as a plain script, run it in a Jupyter notebook or replace display() calls with print() or saving outputs to files.

Jupyter:

bash
jupyter notebook
# open a notebook and run the cells, or
jupyter lab


As a script (quick hack):

bash
python mainn.py


(If running as a script, you may need to remove/replace display() calls to avoid errors.)

## Dataset (expected columns)

The script assumes the CSV contains (at minimum) columns with these names:

* Sr No — unique or sequential id per row (used for counts)
* Startup Name
* Industry Vertical
* SubVertical
* City  Location
* Investors Name
* InvestmentnType  (note spelling; the script expects this exact name)
* Amount in USD — numeric amounts, possibly with commas / plus signs
* Date dd/mm/yyyy — date in dd/mm/yyyy format
* Remarks — optional; script drops it if present

If your file uses slightly different column names, either rename them in the CSV or update mainn.py accordingly.

## What the script does (summary)

1. Loads the CSV into a pandas DataFrame.
2. Drops Remarks if present.
3. Fills missing values in categorical columns with 'Unknown'.
4. Cleans Amount in USD (removes commas and plus signs) and converts to numeric (NaNs → 0).
5. Parses Date dd/mm/yyyy into datetime objects.
6. Normalizes text fields: strips, removes non-ASCII chars, squashes whitespace, converts to lowercase.
7. Adds FundingYear and FundingMonth columns.
8. Aggregates and displays:

   * Yearly funding totals and number of deals
   * Monthly funding totals and number of deals
   * Top sectors, cities, startups by funding
   * Top investors by funding and by number of deals
   * Investment types summary
9. Produces seaborn/matplotlib plots for trends and top lists.
