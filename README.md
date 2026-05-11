# Lymph Node Retrieval Analysis for Breast Cancer Surgery in Nigeria

## Citation

If you use this code or data, please cite the original publication:

> Olasehinde O, Di Bernardo M, Komolafe AO, Omoyiola OZ, Wuraola FO, Betiku O,
> Ogunrinde O, Aderounmu A, Olaofe OO, Adefidipe A, Ewoye E, Mohammed TO,
> Oyeneye F, Adisa AO, Alatise OI, Omoniyi-Esan G. Immediate lymph node
> extraction improves retrieval rate following axillary lymph node dissection:
> an effective approach to improving guideline concordant breast cancer care in
> Nigeria. *ecancermedicalscience*. 2023;17:1609.
> doi: [10.3332/ecancer.2023.1609](https://doi.org/10.3332/ecancer.2023.1609)

**Full text:** <https://ecancer.org/en/journal/article/1609>

## Study Overview

This repository contains the analysis code and de-identified data for a quality
improvement study conducted at Obafemi Awolowo University Teaching Hospital,
Ile-Ife, Nigeria. The study evaluated whether **immediate lymph node extraction**
from surgical specimens improves lymph node retrieval rates and guideline
concordance (<e2><89><a5>10 lymph nodes harvested) following axillary lymph node dissection
in breast cancer surgery.

### Study Design

Data were collected across four time windows:

| Window | Period | Design | Intervention |
|--------|--------|--------|-------------|
| 1 | Retrospective baseline | Historical control | None |
| 2 | Intervention Phase I | Prospective | Immediate LN extraction |
| 3 | Intervention Phase II | Prospective | Immediate LN extraction |
| 4 | Extended follow-up | Prospective | Immediate LN extraction |

### Key Results

Guideline concordance (<e2><89><a5>10 lymph nodes harvested) improved dramatically after
implementing the intervention:

| Window | Concordant / Total | Concordance Rate |
|--------|--------------------|-----------------|
| 1 (Baseline) | 11 / 105 | **10.5%** |
| 2 (Intervention I) | 26 / 39 | **66.7%** |
| 3 (Intervention II) | 20 / 25 | **80.0%** |
| 4 (Follow-up) | 26 / 35 | **74.3%** |

## Repository Contents

```
.
<e2><94><9c><e2><94><80><e2><94><80> README.md          # This file
<e2><94><9c><e2><94><80><e2><94><80> analysis.R         # Main analysis script (R)
<e2><94><9c><e2><94><80><e2><94><80> data.csv           # De-identified patient data (272 records)
<e2><94><9c><e2><94><80><e2><94><80> .gitignore         # Git ignore rules
<e2><94><94><e2><94><80><e2><94><80> results/           # Output directory (created by analysis.R)
    <e2><94><9c><e2><94><80><e2><94><80> tables/        # Summary tables (CSV)
    <e2><94><9c><e2><94><80><e2><94><80> figures/       # Combined publication figures (PDF)
    <e2><94><9c><e2><94><80><e2><94><80> window_1/      # Window 1 outputs (summary CSV, boxplot, barplot)
    <e2><94><9c><e2><94><80><e2><94><80> window_2/      # Window 2 outputs
    <e2><94><9c><e2><94><80><e2><94><80> window_3/      # Window 3 outputs
    <e2><94><94><e2><94><80><e2><94><80> window_4/      # Window 4 outputs
```

## Output Mapping to Paper

The table below maps each section of `analysis.R` to the corresponding
table or figure in the published paper.

| Code Section | Description | Paper Output |
|-------------|-------------|-------------|
| Section 3 | Factor coding and variable labels | Methods <e2><80><94> Variable definitions |
| Section 5 | Filter to breast cancer; duplicate checks | Methods <e2><80><94> Cohort selection |
| Section 6 | Descriptive statistics (all windows) | **Table 1** <e2><80><94> Patient demographics |
| Section 7 | Regression: LN harvested vs. positive, T-stage, age | Results text <e2><80><94> Regression analyses |
| Section 8 | Window 1 summary by firm; boxplot + barplot | **Table 2 / Figure 1** <e2><80><94> Baseline concordance |
| Section 9 | Window 2 summary by firm (intervention) | **Table 3 / Figure 2** <e2><80><94> Intervention concordance |

## Data Description

### File: `data.csv`

272 patient records with 32 variables. Key columns:

| Variable | Description |
|----------|-------------|
| `record_id` | Unique patient identifier |
| `age` | Patient age at surgery |
| `cancer_type` | Cancer type (1 = Breast, 2 = Colorectal) |
| `type_of_operation` | Surgical procedure performed |
| `date_window` | Study period (1<e2><80><93>4) |
| `intervention_applied` | Whether intervention was applied |
| `firm_of_surgeon` | Operating unit (1 = A, 2 = B) |
| `cadre_of_surgeon` | Surgeon level (1 = Consultant, 2 = Resident) |
| `neoadjuvant_chemo` | Neoadjuvant chemotherapy (1 = Yes, 0 = No) |
| `n_ln_harv` | Number of lymph nodes harvested (primary outcome) |
| `n_ln_pos` | Number of lymph nodes positive for malignancy |
| `t_stage_assigned` | Assigned tumor stage |
| `n_stage_assigned` | Assigned nodal stage |
| `histopath_diagnosis` | Histopathological diagnosis |
| `tumour_grade` | Tumor grade (1<e2><80><93>3) |
| `margin_status` | Surgical margin status |
| `specimen_tagged` | Whether specimen was properly tagged |

### Missing Data Codes

- `-666` <e2><80><94> Patient does not know
- `-777` <e2><80><94> Patient refused to answer
- `-888` <e2><80><94> Missing in case notes
- `-999` <e2><80><94> Other missing

## Requirements

### R Version

R <e2><89><a5> 4.0 (tested with R 4.5.0)

### Required R Packages

All packages are available from CRAN:

```r
install.packages(c(
  "tidyverse",   # Core data science (includes dplyr, tidyr, ggplot2, stringr, etc.)
  "ggpubr",      # Publication-ready plots and compare_means()
  "scales",      # Label formatting (label_percent)
  "Hmisc",       # Variable labels
  "gridExtra",   # Arrange multiple grid-based plots
  "cowplot"       # Plot themes and arrangements
))
```

`grid` and `lattice` ship with base R and do not need installation.

> **Note:** The original code used the `ggBrackets` package (GitHub-only,
> not on CRAN), which is incompatible with R <e2><89><a5> 4.5. The current version
> replaces `ggBrackets` with equivalent helper functions using base
> `ggplot2::annotate()`. The original code also loaded `plyr`, `officer`,
> `stringr`, and `lubridate` <e2><80><94> these were unused and have been removed.
> `stringr` and `lubridate` are still available via `tidyverse`.

## Usage

1. Clone this repository:
   ```bash
   git clone https://github.com/mat10d/axillary-lymph-node-retrieval.git
   cd axillary-lymph-node-retrieval
   ```

2. Install required packages (see above).

3. Run the analysis:
   ```r
   source("analysis.R")
   ```

4. Outputs will be written to the `results/` directory.

## Authors

Olalekan Olasehinde, Matteo Di Bernardo, Akinwumi Oluwole Komolafe,
Oluwatosin Zainab Omoyiola, Funmilola Olanike Wuraola, Omolade Betiku,
Opeyemi Ogunrinde, Adewale Aderounmu, Olaejirinde Olaniyi Olaofe,
Adeyemi Adefidipe, Ese Ewoye, Tajudeen Olakunle Mohammed, Fisayo Oyeneye,
Adewale Oluseye Adisa, Olusegun Isaac Alatise, Ganiyat Omoniyi-Esan

## License

This code is released under the MIT License. The data is provided for
research and educational purposes only.

