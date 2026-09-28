# MPDTA DiD Mini-Project

**Question:** How did state minimum-wage increases affect county-level teen employment?

This project uses the `mpdta` county panel distributed with the R [`did` package](https://github.com/bcallaway11/did). The CSV is an export of the package's official [`mpdta.rda` data file](https://raw.githubusercontent.com/bcallaway11/did/master/data/mpdta.rda). The dataset documentation describes 2,500 county-year observations from 2003 through 2007; `lemp` is log teen employment, `countyreal` identifies counties, and `first.treat` records the first minimum-wage increase in the county's state (`0` means never treated). The observed adoption cohorts are 2004, 2006, and 2007.

The notebook proceeds from data checks and treatment construction to county and year fixed effects (the conventional TWFE DiD baseline), coefficient interpretation, and a TWFE event study. It ends with identification assumptions and limitations. Callaway-Sant'Anna group-time ATT is deliberately left as an optional follow-up after the core analysis.

## Setup

```bash
conda activate base
python --version  # Python 3.8.19
python -m pip install -r requirements.txt
```

Open `notebooks/01_mpdta_did.ipynb` in VS Code and select the `base (Python 3.8.19)` kernel. The core data inspection, TWFE, and event-study cells have saved outputs.

## Core results

The county- and year-fixed-effects TWFE estimate is **-0.0365** (state-clustered SE **0.0253**, 95% CI **[-0.0862, 0.0131]**, p = **0.149**), an estimated decrease of about 3.6% in log teen employment; the interval includes zero.

In the TWFE event study, pre-treatment estimates are small and their pointwise 95% confidence intervals include zero. Post-treatment estimates are negative; intervals include zero at event times 0 and 1, and fall below zero at event times 2 and 3. These patterns are descriptive and do not establish a causal effect.

## Data and interpretation

The checked-in CSV makes the analysis input available without requiring R or a download at notebook runtime. See the [`mpdta` dataset documentation](https://bcallaway11.github.io/did/reference/mpdta.html) and Callaway and Sant'Anna (2021), [*Difference-in-Differences with Multiple Time Periods*](https://doi.org/10.1016/j.jeconom.2020.12.001).

Results are illustrative, not definitive policy estimates. The short panel limits pre-trend diagnostics, and conventional TWFE estimates and event-study coefficients can be misleading under staggered adoption and heterogeneous effects. Policy is assigned at the state level while outcomes are observed by county; standard errors are clustered by state. The event-study intervals are pointwise.
