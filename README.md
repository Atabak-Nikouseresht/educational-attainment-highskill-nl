# Education and High-Skill Employment — Netherlands, 2011

An applied microeconometrics course project studying the association between educational attainment and high-skill occupation status in the Netherlands, using IPUMS International 2011 census microdata.

## Research design

The report defines high-skill occupations as ISCO major groups 1–3 and estimates a Linear Probability Model with education categories and demographic controls. A logit model and predicted margins are also reported. The report explicitly notes that the cross-sectional design does not establish a causal effect.

## Reported evidence

The committed Stata output reports an analysis sample of 231,986 individuals. In its logit margins table, the predicted probability for the tertiary-education category is approximately 0.800, compared with approximately 0.051 for the no-education reference category. These are model-based predicted margins in the saved output, not causal effects.

## Files in this repository

- [`group_15.pdf`](group_15.pdf) — full group report, including sample definition, model, and identification discussion.
- [`Results.pdf`](Results.pdf) — saved Stata regression and margins output.
- [`Graphs.pdf`](Graphs.pdf) — figures from the analysis.

## Data and reproducibility limits

The IPUMS microdata extract is not included because access is governed by IPUMS terms. The repository also contains no Stata do-files: earlier instructions referred to files that are not present. Consequently, the displayed outputs can be inspected, but the cleaning and estimation workflow cannot currently be rerun from this repository. Do not use the placeholder filenames from older documentation as run instructions.

To reproduce the analysis, the original do-files must first be recovered and committed, and a researcher must obtain a matching IPUMS extract under the applicable access terms. No data file should be redistributed here without confirming its license.

- **Academic context:** Econometrics project, University of Bologna
- **Authors:** Atabak Nikouseresht, Kimia Shokri, and Mahgol Lamei
