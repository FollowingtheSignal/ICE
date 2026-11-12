# ICE Detention Trends Analysis (2022–2026)

## Project Overview

This project examines how U.S. Immigration and Customs Enforcement (ICE) detention activity changed between October 2022 and July 2026, with particular attention to trends following January 2025.

Using publicly available detention records, I analyzed changes in facility book-ins, criminality classifications, conviction types, and the duration of detention-facility stays.

The goal is to understand what changed over time while distinguishing between the number of detention records and the number of individuals represented in those records.

## Data Source

The data comes from the [Deportation Data Project](https://deportationdata.org/), a research initiative at UC Berkeley and UCLA that makes government immigration enforcement records available to the public.

The original ICE records were obtained through Freedom of Information Act (FOIA) litigation and released publicly on August 24, 2026.

**Analysis period:** October 1, 2022 – July 31, 2026.

August 2026 was excluded because the available records covered only part of that month.

## Dataset Description

The original dataset contains detention-stint records. A *stint* is a period spent at an individual detention facility.

An individual can have multiple records if they are transferred between facilities or detained on separate occasions. Therefore, detention-stint counts should not be interpreted as counts of unique individuals or arrests.

### `monthly_all.csv`

Contains monthly aggregated ICE detention statistics.

Each row represents one calendar month. The dataset includes:

- Monthly detention-facility book-in counts and distinct identified individuals.
- Counts and percentages of three ICE criminality classifications: convicted criminals, pending criminal charges, and other immigration violators.
- Violent and nonviolent conviction classifications among records categorized as involving convicted criminals.
- Median duration of individual detention-facility stints, measured in days.

Criminality categories reflect ICE's administrative records rather than independently verified criminal court outcomes.

### `monthly_stints.csv`

Contains monthly statistics describing how frequently identified individuals appear in detention-facility records.

Each row represents one calendar month and includes:

| Column | Description |
|---|---|
| `year_month` | Calendar month of facility book-in |
| `records` | Number of detention-stint records with a nonmissing individual identifier |
| `individuals` | Number of distinct identified individuals |
| `stints_per_person` | Monthly detention-stint records divided by distinct identified individuals |

The `stints_per_person` measure may reflect facility transfers, repeated detention episodes, or both. It is **not a direct transfer rate**.

## Data Cleaning and Methodology

- Combined the original ICE detention files into a single dataset.
- Excluded records flagged as probable duplicates by the Deportation Data Project.
- Missing facility location information was filled where possible using facility codes.Missing individual identifiers and detention departure dates were not imputed. Calculations requiring those fields used only records with available values.
- Restricted the analysis to October 2022 through July 2026.
- Aggregated detention-stint records by calendar month.
- Used anonymized individual identifiers to calculate monthly distinct-person counts.
- Calculated monthly criminality counts and percentages.
- Examined violent and nonviolent conviction classifications within the convicted-criminal category.
- Calculated median facility-stint duration using records with available duration information.

The monthly distinct-person calculation excludes missing identifiers. Consequently, record counts in `monthly_stints.csv` may be slightly lower than the total detention-stint counts in `monthly_all.csv`.

## Key Findings

- ICE detention-facility book-ins increased substantially beginning in early 2025.
- The share of records classified as involving convicted criminals initially increased, then declined.
- Records involving pending criminal charges grew as a percentage of total detention activity.
- The number of records classified as "Other Immigration Violators" increased substantially, although their share remained generally below earlier levels.
- Among records classified as involving convicted criminals, the percentage associated with violent convictions declined.
- Median facility-stint duration decreased, while the number of facility-stint records per identified individual increased.

## Limitations

This analysis is descriptive and does not establish the causes of observed changes.

In particular:

- A facility book-in is not necessarily a new arrest or a new detention episode.
- One individual may generate multiple detention records.
- Criminality classifications represent information recorded by ICE and do not independently verify criminal histories or active prosecutions.
- A facility stint does not necessarily represent the full time an individual spent in ICE custody.
- Missing departure dates may affect reported median durations, particularly in recent months.
- An increase in stints per person does not establish that facility transfers increased.

## Tools Used

- **Python:** pandas and NumPy for data preparation and analysis.
- **Datawrapper:** Interactive charts and visualizations.
- **GitHub:** Dataset documentation and project sharing.

## Article and Visualizations

The accompanying analysis was written for my Substack publication, *Following the Signal*.

**Article:** https://followingthesignal.substack.com/

The article includes interactive visualizations examining detention activity, criminality classifications, conviction types, and facility-stint durations.

## References

- [Deportation Data Project](https://deportationdata.org/)
- [ICE Detention Data](https://deportationdata.org/data/processed/ice)
- [ICE Data Codebook](https://deportationdata.org/docs/ice/codebook.html)

## Author

Independent data analysis project. Findings and visualizations are based on publicly released ICE records and should not be interpreted as official conclusions of ICE or the Deportation Data Project.
