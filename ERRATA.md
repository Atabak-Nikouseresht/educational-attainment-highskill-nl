# Errata and interpretation limits

These notes correct identifiable descriptions in the archived group report and explain the limits of its saved output. **No PDF, data, estimate, standard error, or figure has been changed or recomputed.** Page references below are one-based PDF pages; command numbers are the printed numbers in `Results.pdf`. Official documentation explains statistical semantics, not undocumented original project decisions.

## 1. Correction: predictive margins are probabilities, not differences

**Report:** `group_15.pdf`, p. 3, “Econometric models” describes post-logit “predictive marginal effects” as probability differences; “Justification for robustness model” also invokes marginal effects to ensure comparison with the LPM.

**Saved evidence:** `Results.pdf`, p. 2, command 9 fits `logit HighSkill i.educnl age i.sex i.marst i.nativity`. Page 3, command 11 is **`margins educnl`**. Its heading is `Predictive margins`, its expression is `Pr(HighSkill), predict()`, and its column is `Margin`. The no-education and tertiary rows report **0.0511737** and **0.7998765**, respectively.

**Correct reading:** these are adjusted predicted probability levels, averaging the model's predictions over the other observed covariates with education set in turn to each category. They are not within-category raw employment proportions and not reported changes relative to no education. Stata's `[R] margins`, “Obtaining margins of responses” (p. 12), defines predictive margins; `dydx()` requests effects rather than response levels (p. 6), and factor-variable effects use discrete differences from the base category (“Derivatives versus discrete differences,” pp. 29–30).[1]

The LPM education coefficients are conditional differences on a 0–1 probability scale (`Results.pdf`, p. 1, command 7), whereas logit coefficients are on the log-odds scale and the saved margins are probability levels.[2][3] Multiply a probability-scale difference by 100 to express it in percentage points; do not call the unscaled coefficient a percentage-point value. Direct numerical comparison would require comparable probability contrasts, including their own uncertainty. An unsaved `margins, dydx(educnl)` or an explicit contrast could request that estimand, but neither is supplied as a result here.[1] No contrast has been calculated and no significance claim about a difference follows from the separate margins' reported tests.

**Impact — local interpretation issue:** the reported estimand was mislabeled; saved probability levels remain unchanged, and no probability-difference estimate or uncertainty has been reconstructed.

## 2. Correction: EDUCNL is Netherlands-specific; its codes are not a continuous schooling scale

**Report:** `group_15.pdf`, p. 1 calls `educnl` an IPUMS international classification whose higher values represent higher schooling. Page 3 instead correctly specifies categorical indicators.

**Official definition:** IPUMS defines EDUCNL as the highest educational level in the Netherlands attended or completed. Its code listing includes **998 = Unknown** and **999 = NIU (not in universe)**; these are not higher educational attainment. The variable is Netherlands-specific, rather than a generic cross-country schooling classification.[5]

**Saved evidence:** `Results.pdf`, p. 1, `summ age HighSkill educnl` reports education codes ranging from 0 to 998 and a mean of 289.251. `tab educnl` gives named categories, and both regression commands use `i.educnl` (pp. 1–2). The code mean is not years of education or a meaningful mean schooling level. Read the categorical distribution and coefficients, not the numeric-code mean. The official coding explains the special-code issue; it does not establish that the original extract or value labels were unmodified.

**Impact — wording only:** qualify the description of education codes. The displayed estimation already uses category indicators; this does not establish a miscoded continuous-regressor model.

## 3. Clarification: removal of Stata missing values does not imply removal of Unknown categories

**Report:** `group_15.pdf`, p. 1 says observations missing age, sex, education, or occupation were removed.

**Saved evidence:** `Results.pdf`, p. 1, `tab educnl` retains **2,680** observations labeled **Unknown**. Unknown also has a fitted education coefficient in the LPM and logit and a predictive-margin row (pp. 1–3). Marital status and nativity each have fitted rows labeled **Unknown/missing** (p. 2, both models).

**Correct reading:** Stata system missing `.` and extended missing `.a`–`.z` are distinct from finite numeric codes with labels such as Unknown.[4] The fitted category rows demonstrate that these labels were retained as model categories; their wording alone does not make them Stata missing values. In particular, the public EDUCNL codebook's 998 is a finite special code.[5]

The missing-removal statement can coexist with retaining coded Unknown values. It would be incorrect to say all substantively unknown information was excluded. Conversely, these output rows do **not** prove that the report's statement about removal of actual Stata missing values was false. The original import, missing-code recodes, occupation construction, exclusions, and before/after counts are unavailable; do not infer which omitted cases became zero, missing, or excluded.

## 4. Clarification: conventional LPM standard errors are established for the displayed fit

**Saved evidence:** `Results.pdf`, p. 1, command 7 prints:

```stata
reg HighSkill i.educnl age i.sex i.marst i.nativity
```

There is no `svy:` prefix, weight expression, or `vce()` option in that command. The output includes the conventional Source/SS/df/MS ANOVA table, `F(14, 231971)`, and an ordinary `Std. err.` column. This is affirmative command/output evidence, not a conclusion from the report's silence.

Stata documents `vce(ols)` as the default homoskedastic OLS variance estimator (`[R] regress`, p. 3); `vce(robust)` allows heteroskedasticity, and the manual notes that robust fits suppress the usual ANOVA table (p. 13).[2] Thus the saved LPM uses conventional OLS standard errors, not heteroskedasticity-robust, clustered, or survey-design-adjusted errors. This conclusion is limited to the printed fit; it does not reconstruct unseen runs.

**Interpretation limit:** robust uncertainty should be considered for an LPM rather than treating conventional OLS uncertainty as automatically reliable for a binary outcome. Which weighting/design and dependence adjustments are warranted additionally depends on the sample and analysis target.[2][6] No heteroskedasticity test has been performed here and no replacement error, interval, or p-value is asserted. Separately, `Results.pdf`, p. 3 explicitly reports logit margins with **`Model VCE: OIM`** and **Delta-method** errors; that is not a robust or survey-adjusted output label.[3]

## 5. Clarification: weights and survey design are relevant, but the correct specification is not recoverable

**Report/output evidence:** `group_15.pdf`, p. 1 explicitly states that descriptives are unweighted. `Results.pdf`, p. 1 prints unweighted `summ` and `tab` commands; its LPM and logit commands (pp. 1–2) contain neither weight expressions nor `svy:`. These specific saved results are therefore not documented as weighted/design-adjusted fits. Absence of a methods paragraph or `svyset` text alone would not establish this; the actual estimation commands are the evidence.

**Sample-specific primary evidence:** the IPUMS Sample Design Summary's **Netherlands 2011** row flags **Persons not organized into households** and **Differential weighting**; it does not flag household clustering.[7] The Netherlands Sample Characteristics page, **2011**, describes a **2.5% stratified sample**, weights computed by the statistical agency, and no identified households.[11] The summary's absence of a complex-stratification flag should not be read as proving no stratification: the detailed description explicitly calls the sample stratified.[7][11]

IPUMS advises weighting for representative estimates and accounting for relevant design characteristics in variance estimation; it discusses PERWT, clustering, and stratification, while emphasizing that designs vary.[6] Consequently, the unweighted archive should not be presented as automatically population-representative. Nor should a generic household-cluster correction be prescribed for this person-record sample. The correct available strata/design identifiers, domain treatment for the restricted analysis sample, actual extract weights, and intended estimand require the original extract and design metadata. No specific `svyset` command is invented, and neither the magnitude nor direction of any change to estimates or uncertainty is established.

## 6. Clarification: association, figure provenance, and credit

- **Causality:** `group_15.pdf`, p. 1 uses “affects” and p. 2 states directional hypotheses, but p. 3, “Identification strategy,” explicitly limits coefficients to conditional associations because unobserved differences remain. Read the results under that explicit limitation. The LPM/logit comparison is a functional-form check, not new causal identification.
- **Figure:** `Graphs.pdf`, p. 1 shows age-density bars and an overlaid smooth curve. `Results.pdf`, p. 1, command 6 prints `hist age, width(1) normal`. With no generating code or linkage record, the figure is inspectable but not independently regenerable or proven to be the exact product of that logged command.
- **Authorship:** `group_15.pdf`, p. 1 names **Atabak Nikouseresht, Kimia Shokri, and Mahgol Lamei**. Local Git history attributes the PDF upload (`83db4ee`) and documentation maintenance to Atabak Nikouseresht; it does not establish each author's original research tasks. Individual contributions remain **unseparated**.

## Documentation boundary

**ERRATA.md** is used rather than only interpretation notes because sections 1–2 identify actual wording/estimand errors supported by the archived output and official documentation. Sections 3–6 are explicitly clarifications or limits, not claims of additional proven analysis errors. The repository remains **Archival report-only**: saved outputs without original executable analysis code do not constitute partial reproduction. Nothing here reconstructs the analysis, changes historical numbers, edits PDFs, or resolves historical privacy authorization.

## Sources

[1] https://www.stata.com/manuals/rmargins.pdf
[2] https://www.stata.com/manuals/rregress.pdf
[3] https://www.stata.com/manuals/rlogit.pdf
[4] https://www.stata.com/manuals/u12.pdf
[5] https://international.ipums.org/international-action/variables/EDUCNL
[6] https://international.ipums.org/international/variance_estimation.shtml
[7] https://international.ipums.org/international/sample_design_summary.shtml
[11] https://international.ipums.org/international-action/sample_details/country/nl
