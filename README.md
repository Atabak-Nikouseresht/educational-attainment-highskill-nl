# Educational Attainment & High-Skill Employment in the Netherlands (OLS on IPUMS 2011)

This project analyzes how educational attainment affects the probability of working in high-skill occupations in the Netherlands, using IPUMS International 2011 census microdata and OLS regression models.

## Objective

- Quantify the relationship between education levels and high-skill employment.
- Generate labour-market risk insights by linking education to high-skill job odds.

## Data

- Source: IPUMS International – Netherlands 2011 census microdata.
- Access: Data are **not** included in this repository due to IPUMS terms of use.
  - Users must request access and recreate the extract from IPUMS.
- Key variables:
  - Education (categorical)
  - Occupation (ISCO-based, recoded into a high-skill indicator)
  - Demographics (age, gender, etc.)

## Methods

- Econometric framework: OLS on individual-level microdata.
- High-skill employment defined via ISCO recode (binary indicator).
- Estimation and analysis performed in **Stata** via `.do` scripts in the `code/` folder.

## Repository Structure

- `code/` – Stata `.do` files for data cleaning, variable construction, and regressions.
- `paper/` – PDF of the project report summarising motivation, methodology, and results.
- `output/` – Regression tables and selected figures.

## Tools

- Stata
- IPUMS International microdata
