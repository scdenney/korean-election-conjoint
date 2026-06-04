# Korean Election Conjoint Data

[![DOI: Paper](https://img.shields.io/badge/DOI-10.1177%2F13540688251339976-blue?style=flat-square)](https://doi.org/10.1177/13540688251339976) [![Open Science](https://img.shields.io/badge/Open_Science-Replication_Materials-brightgreen?style=flat-square&logo=opensourceinitiative&logoColor=white)](https://github.com/scdenney/korean-election-conjoint) [![Harvard Dataverse](https://img.shields.io/badge/Harvard-Dataverse-orange?style=flat-square)](https://doi.org/10.7910/DVN/3N4UFF)

Replication data for the 2024 South Korea conjoint experiment on presidential candidate preferences.

> Denney, Steven, and Peter Ward. 2025. "Partisan Voters in Party Systems with Ephemeral Parties: Evidence from South Korea." *Party Politics*. DOI: [10.1177/13540688251339976](https://doi.org/10.1177/13540688251339976)

## Changelog

**v2 (2026-06-04):** Added three columns to `final_df_conjoint.csv` that were missing from the initial deposit:
- `question_profile` — task × profile identifier (e.g., "1.1" = task 1, profile 1)
- `chosen` — the forced-choice CBC outcome (1 = selected, 0 = not selected); essential for conjoint analysis
- `open_text_reason` — open-text explanation for task 6 choice (Q40 in the Qualtrics survey)

Coverage note: `chosen` is populated for 39,660 of 40,100 rows (98.9%; 1,983 of 2,005 respondents). The 22 respondents with missing values (440 rows, `chosen` = empty string) could not be matched across available Qualtrics exports. Exclude rows where `chosen` is empty for conjoint analysis.

## Files

- `final_df_direct.csv`: Cleaned data with respondent-level direct responses (n = 2,005 respondents).
- `final_df_conjoint.csv`: Cleaned long-format conjoint data (n = 40,100 rows; 20 rows per respondent = 10 tasks × 2 profiles). Includes `chosen`, `question_profile`, and `open_text_reason` as of v2.
- `data_dictionary_direct.csv`: Variable definitions for `final_df_direct`.
- `data_dictionary_conjoint.csv`: Variable definitions for `final_df_conjoint`.
- `README.md`: This file.

## Quick-start (R)

```r
library(tidyverse); library(cregg)

df <- read_csv("final_df_conjoint.csv") |>
  filter(chosen != "")   # drop 22 respondents with unresolved raw data

mm <- cj(df,
         chosen ~ age_attribute + origin + gender_attribute + career +
                  scandal + labor_policy + housing_policy +
                  social_policy + foreign_policy + nuclear_policy,
         id = ~respondent_id, estimate = "mm")
plot(mm)
```

## DOI

Denney, Steven. 2025. "Replication Data for: Partisan Voters in Party Systems with Ephemeral Parties: Evidence from South Korea." Harvard Dataverse. https://doi.org/10.7910/DVN/3N4UFF.

## Contact

Steven Denney, Leiden University
stevencdenney@gmail.com
