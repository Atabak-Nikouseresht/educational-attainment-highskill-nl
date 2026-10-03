# Education and High-Skill Employment — Netherlands, 2011

**Collaborative academic project · Archival report-only — outputs inspectable, analysis not rerunnable.**

An econometrics course project examining the **association** between educational attainment and high-skill occupation status. The report describes IPUMS International Netherlands 2011 individual-level microdata, an OLS linear probability model (LPM), and a logit functional-form comparison. The public evidence consists of **three PDFs**, not an executable analysis package.

**Authors:** Atabak Nikouseresht, Kimia Shokri, and Mahgol Lamei. Individual contributions are **unseparated**: the report credits the group, but the available materials do not document each person's original research role.

**Read the [ERRATA and interpretation limits](ERRATA.md) alongside the archived output.** They distinguish confirmed wording errors from unresolved cleaning and survey-design questions.

## Research question and methods

How does educational attainment relate to high-skill occupation status after accounting for age, sex, marital status, and nativity?

- **Reported sample:** 231,986 individuals, ages 17–67 (`group_15.pdf`, p. 1; `Results.pdf`, p. 1, `summ age HighSkill educnl`). These are the archived analysis sample's figures, not a population estimate.
- **Reported outcome:** `HighSkill`, with ISCO major groups 1–3 classified as high skill. The output labels the comparison group as ISCO 4–9 (`group_15.pdf`, p. 2; `Results.pdf`, p. 1, `tab HighSkill`). The original recoding is unavailable; treatment of other occupation codes cannot be audited.
- **Models:** `reg HighSkill i.educnl age i.sex i.marst i.nativity` and `logit HighSkill i.educnl age i.sex i.marst i.nativity` (`Results.pdf`, pp. 1–2, commands 7 and 9). Education is categorical, with no education as the reported reference category (`group_15.pdf`, p. 3).
- **Logit postestimation:** `margins educnl` reports adjusted predicted probabilities, **not education-category probability differences** (`Results.pdf`, p. 3, command 11). Stata distinguishes predictive margins from marginal effects and contrasts.[1]

The report's cross-sectional design supports conditional associations, not causal effects (`group_15.pdf`, p. 3, “Identification strategy”). Agreement between model forms does not supply a separate causal identification strategy.

## Inspectable evidence

| Artifact | Contents and reference |
| --- | --- |
| [group_15.pdf](group_15.pdf) | Three-page group report: sample description and authors (p. 1), outcome and hypotheses (p. 2), models and identification limits (p. 3). |
| [Results.pdf](Results.pdf) | Three-page Stata output: descriptive statistics and LPM (p. 1, continuing on p. 2), logit (p. 2), predictive margins (p. 3). |
| [Graphs.pdf](Graphs.pdf) | One-page age-density chart with bars and an overlaid curve; the saved output separately lists `hist age, width(1) normal` (`Results.pdf`, p. 1, command 6). No source file connects or regenerates the chart. |
| [ERRATA.md](ERRATA.md) | Page- and command-level corrections and interpretation limits; official Stata and IPUMS methodological references. The PDFs are unchanged. |

In the saved output, the LPM tertiary-education coefficient is **0.7372145** relative to no education (`Results.pdf`, p. 1). The logit predictive margins are **0.7998765** for tertiary education and **0.0511737** for no education (`Results.pdf`, p. 3). The coefficient is a conditional probability difference on a 0–1 scale; the two margins are probability levels. None is a causal estimate.

## Reading cautions

- **Missing is not the same as “Unknown.”** `tab educnl` includes 2,680 observations labeled Unknown; both models include this category. Marital status and nativity also retain categories labeled Unknown/missing (`Results.pdf`, pp. 1–2). The report's missing-value removal statement does not establish how special codes were handled. See the errata for the distinction from Stata system/extended missing values.[4]
- **Saved uncertainty is not robust or survey-design-adjusted inference.** The printed LPM command has no weight or `vce()` option and its output is conventional OLS; the logit margins explicitly show `Model VCE: OIM` (`Results.pdf`, pp. 1–3). This describes these saved fits, not an unseen original workflow.[2][3]
- **Weighting and design require sample-specific checks.** The report explicitly calls its descriptive statistics unweighted (`group_15.pdf`, p. 1). IPUMS documents both person weights and sample-specific variance considerations; an omitted discussion alone would not establish whether survey procedures were used. Here the printed commands support the narrower finding about the saved fits. The Netherlands 2011 design summary flags differential weighting and person records not organized into households, so a generic household-clustering prescription would be unjustified. The exact appropriate specification still requires the original extract/design information.[6][7]

## Reproducibility and data access

**Status: Archival report-only.** The tracked repository contains the three PDFs and documentation, but no original Stata do-files, microdata extract, extract specification, or executable environment record. Saved commands and tables make selected outputs inspectable; they do not reproduce the cleaning, construction of variables, estimation, or chart generation. “Partially reproducible” would require an available executable part of that workflow, not output alone.

A verified reproduction would need the original analysis code, matching authorized IPUMS extract and extract metadata, category/missing-code recodes, sample restrictions, weighting/design choices, and Stata version. These are recovery requirements, not supplied run instructions. IPUMS access is governed by its terms; authorized access does not authorize public redistribution of the microdata.[9]

## Academic credit and provenance

The report identifies this as an **Econometrics project, Group 15** and names all three authors (`group_15.pdf`, p. 1). The local Git history records the PDF upload in commit `83db4ee` under Atabak Nikouseresht and later documentation/privacy maintenance. Upload and maintenance attribution are not evidence of individual original modeling, coding, data-cleaning, or writing roles. The academic work is credited jointly; individual contributions remain unseparated.

## Sources

[1] https://www.stata.com/manuals/rmargins.pdf
[2] https://www.stata.com/manuals/rregress.pdf
[3] https://www.stata.com/manuals/rlogit.pdf
[4] https://www.stata.com/manuals/u12.pdf
[6] https://international.ipums.org/international/variance_estimation.shtml
[7] https://international.ipums.org/international/sample_design_summary.shtml
[9] https://international.ipums.org/international/terms.shtml
