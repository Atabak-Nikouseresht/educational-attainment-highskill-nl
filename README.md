# Educational Attainment & High-Skill Employment – Netherlands 2011

This repository contains the Stata code and outputs for my econometrics project
on how educational attainment predicts high-skill occupation status in the
Netherlands using IPUMS International 2011 microdata.

## Repository Maintainer

**Atabak Nikouseresht**  
MSc Applied Economics and Markets — University of Bologna

## Project overview

- **Outcome:** `HighSkill` – indicator for ISCO 1–3 (managers, professionals, technicians).
- **Key regressor:** `educnl` – categorical education variable.
- **Controls:** age, sex, marital status, nativity.
- **Methods:** Linear Probability Model (OLS) and Logit with marginal effects.

Main finding: university education raises the predicted probability of holding a
high-skill job from about 5% (no education) to around 80%.

## Repository structure

- `stata/` – Stata do-files
  - `ipumsi_00002.do`: builds the raw dataset from the IPUMS extract.
  - `[your_analysis_file].do`: cleans data and estimates the models.

- `output/`
  - `Results.pdf`: regression tables and margins output.
  - `Graphs.pdf`: age histogram and other figures.
  - `group_15.pdf`: full project report (sample selection, model, identification).

- `data/`
  - *Not included in the repository due to IPUMS licence restrictions.*
  - You must download the same extract from IPUMS and save it as
    `data/ipumsi_00002.dat` before running the code.

## Data access

Microdata are provided by **IPUMS International**.  
To replicate the results, you must:

1. Register at IPUMS International.
2. Request the 2011 census extract for the Netherlands with the same variables.
3. Download the `.dat` file and rename/place it as `data/ipumsi_00002.dat`.
4. Open Stata and run `do stata/ipumsi_00002.do`.
5. Then run `[your_analysis_file].do` to reproduce the tables and figures.

## Requirements

- Stata 17 (or compatible version).
