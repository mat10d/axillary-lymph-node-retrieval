# Lymph Node Retrieval Analysis for Breast Cancer Surgery in Nigeria

## Project Overview

This repository contains the data analysis code for a published research study examining the impact of immediate lymph node extraction protocols on lymph node retrieval rates following axillary lymph node dissection in breast cancer surgery.

**Title:** Immediate lymph node extraction improves retrieval rate following axillary lymph node dissection: an effective approach to improving guideline concordant breast cancer care in Nigeria

**Principal Investigator:** Lekan Olasehinde

**Institution:** Obafemi Awolowo University Teaching Hospital, Nigeria

**Publication:** ecancermedicalscience

**DOI/URL:** https://ecancer.org/en/journal/article/1609-immediate-lymph-node-extraction-improves-retrieval-rate-following-axillary-lymph-node-dissection-an-effective-approach-to-improving-guideline-concordant-breast-cancer-care-in-nigeria

## Citation

If you use this code or data, please cite the original publication:

```
Olasehinde O, et al. Immediate lymph node extraction improves retrieval rate following
axillary lymph node dissection: an effective approach to improving guideline concordant
breast cancer care in Nigeria. ecancermedicalscience. 2023.
```

## Research Background

### Objective

To evaluate whether immediate lymph node extraction from surgical specimens improves lymph node retrieval rates and guideline concordance in breast cancer surgery.

### Study Design

This is a quality improvement intervention study conducted at a single tertiary hospital in Nigeria. The study compares lymph node retrieval rates across multiple time periods:

- **Window 1:** Retrospective baseline (no intervention)
- **Window 2:** Intervention phase I (initial implementation)
- **Window 3:** Intervention phase II (continued implementation)
- **Window 4:** Extended follow-up period

### Guideline Concordance

The study uses the standard pathology guideline requiring **≥10 lymph nodes** to be harvested and examined for adequate nodal staging in breast cancer.

### Key Findings

The intervention of immediate lymph node extraction significantly improved:
- Mean number of lymph nodes harvested
- Proportion of cases meeting guideline concordance threshold
- Quality of pathological staging

## Repository Contents

```
.
├── README.md           # This file
├── analysis.R          # Main analysis script
├── data.csv           # De-identified patient data
├── .gitignore         # Git ignore rules
└── results/           # Output directory (created by analysis.R)
    ├── tables/        # Summary tables (CSV format)
    ├── figures/       # Publication figures (PDF format)
    ├── window_1/      # Window 1 specific outputs
    ├── window_2/      # Window 2 specific outputs
    ├── window_3/      # Window 3 specific outputs
    └── window_4/      # Window 4 specific outputs
```

## Data Description

### Data File

`data.csv` - Contains de-identified patient records with the following key variables:

**Patient Demographics:**
- `age` - Patient age at surgery
- `initials` - Patient initials (de-identified)

**Clinical Variables:**
- `cancer_type` - Type of cancer (Breast/Colorectal)
- `type_of_operation` - Surgical procedure performed
- `neoadjuvant_chemo` - Whether neoadjuvant chemotherapy was administered
- `date_window` - Study period (1, 2, 3, or 4)

**Pathology Variables:**
- `n_ln_harv` - Number of lymph nodes harvested (primary outcome)
- `n_ln_pos` - Number of lymph nodes positive for malignancy
- `t_stage_assigned` - Assigned tumor stage
- `n_stage_assigned` - Assigned nodal stage
- `histopath_diagnosis` - Histopathological diagnosis
- `tumour_grade` - Tumor grade (1-3)
- `margin_status` - Surgical margin status

**Intervention Variables:**
- `intervention_applied` - Whether intervention was applied
- `firm_of_surgeon` - Operating unit (A or B)
- `cadre_of_surgeon` - Surgeon training level

**Quality Control:**
- `specimen_tagged` - Whether specimen was properly tagged
- `proforma_complete` - Data completeness status

### Missing Data Codes

The dataset uses standardized missing data codes:
- `-666` - Patient does not know
- `-777` - Patient refused to answer
- `-888` - Missing in case notes
- `-999` - Other missing (see comments)

## Analysis Overview

The analysis script (`analysis.R`) performs the following:

1. **Data Preprocessing**
   - Loads and cleans raw data
   - Converts coded variables to meaningful factor labels
   - Identifies and handles duplicate records
   - Applies variable labels

2. **Descriptive Statistics**
   - Overall cohort characteristics
   - Distribution of key variables by study window
   - Cross-tabulations by firm and intervention status

3. **Regression Analyses**
   - Relationship between harvested and positive lymph nodes
   - Association with tumor stage
   - Association with patient age
   - Effect of intervention on harvest rates

4. **Comparative Analyses**
   - Between-firm comparisons (Operating Unit A vs B)
   - Pre/post intervention comparisons
   - Statistical tests (t-tests, proportion tests)

5. **Visualization**
   - Boxplots comparing lymph node harvest rates
   - Bar plots showing guideline concordance proportions
   - Combined publication-ready figures

6. **Output Generation**
   - Summary tables (CSV format)
   - Statistical plots (PDF format)
   - Session information for reproducibility

## Requirements

### R Version

The analysis was developed using R version 4.0 or higher.

### Required R Packages

Install all required packages using:

```r
# Core data manipulation
install.packages("dplyr")
install.packages("tidyr")
install.packages("tidyverse")
install.packages("plyr")
install.packages("stringr")

# Date/time handling
install.packages("lubridate")

# Statistical analysis
install.packages("Hmisc")
install.packages("scales")

# Visualization
install.packages("ggplot2")      # Included in tidyverse
install.packages("ggpubr")
install.packages("ggBrackets")
install.packages("cowplot")
install.packages("gridExtra")
install.packages("grid")
install.packages("lattice")

# Document generation
install.packages("officer")
```

Or install all at once:

```r
required_packages <- c(
  "officer", "dplyr", "tidyr", "tidyverse", "stringr", "plyr",
  "ggBrackets", "ggpubr", "scales", "lubridate", "Hmisc",
  "gridExtra", "grid", "lattice", "cowplot"
)

install.packages(required_packages)
```

### Package Descriptions

- **officer** - Work with Microsoft Office documents
- **dplyr** - Data manipulation grammar
- **tidyr** - Tidy data formatting
- **tidyverse** - Collection of data science packages
- **stringr** - String manipulation
- **plyr** - Data splitting, applying, and combining
- **ggBrackets** - Add statistical brackets to ggplot2
- **ggpubr** - Publication-ready plots
- **scales** - Scale functions for visualization
- **lubridate** - Date/time manipulation
- **Hmisc** - Harrell Miscellaneous (variable labels)
- **gridExtra** - Arrange multiple grid-based plots
- **grid** - Low-level graphics functions
- **lattice** - Trellis graphics system
- **cowplot** - Streamlined plot themes and arrangements

## Usage

### Running the Analysis

1. Clone this repository or download the files
2. Set your working directory to the repository folder
3. Ensure all required packages are installed
4. Run the analysis script:

```r
source("analysis.R")
```

### Output

The script will create a `results/` directory containing:

- **Summary Tables:** `results/window_*/firm_summary.csv`
  - Number of surgeries per firm
  - Number and percentage meeting guideline concordance
  - Mean lymph nodes harvested and positive

- **Statistical Plots:**
  - `results/window_*/boxplot_firm.pdf` - Lymph node harvest comparisons
  - `results/window_*/barplot_firm.pdf` - Concordance proportion comparisons
  - `results/figures/Figure1_window1.pdf` - Combined publication figure

### Modifying the Analysis

The script is organized into clearly marked sections:

1. Load packages
2. Setup and data loading
3. Data preprocessing
4. Define analysis functions
5. Filter to breast cancer cases
6. Descriptive statistics
7. Overall analysis
8. Window 1 analysis (baseline)
9. Window 2 analysis (intervention)
10. Session information

To add new analyses or modify existing ones, navigate to the appropriate section.

## Data Privacy

All patient data has been de-identified in accordance with institutional review board (IRB) requirements and HIPAA guidelines. No protected health information (PHI) is included in this repository.

## Study Limitations

- Single-center study (limited generalizability)
- Retrospective component (Window 1) may have selection bias
- Small sample sizes in some subgroups
- Potential confounding by temporal trends

For detailed discussion of limitations, see the published manuscript.

## Contributing

This is a published research project. For questions or comments about the analysis, please contact the principal investigator or open an issue in this repository.

## License

This code is released under the MIT License. The data is provided for research and educational purposes only.

## Acknowledgments

- Study team at Obafemi Awolowo University Teaching Hospital
- Participating patients who consented to data collection
- ecancermedicalscience for publication

## Contact

For questions regarding this analysis or the study:

**Principal Investigator:** Lekan Olasehinde
**Institution:** Obafemi Awolowo University Teaching Hospital, Nigeria

## Version History

- **v1.0** (2023) - Initial analysis for publication
- **v1.1** (Current) - Cleaned and documented code for reproducibility

---

**Last Updated:** December 2025
