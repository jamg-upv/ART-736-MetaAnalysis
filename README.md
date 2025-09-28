
codigo para metanalisis usado en art-736 (pendiente de ocnverger a un modelo junto con art-639

# Videos de Soporte
https://media.upv.es/#/portal/channel/5ab9fa10-22b4-11ef-8f10-ab3091b330f3

# Description

# Meta-Analysis Project: ART 736-Canet

## Overview
This R Markdown document contains a comprehensive meta-analysis workflow for processing and analyzing effect sizes from multiple studies. The project follows a systematic approach through several stages, from data preprocessing to final analysis and visualization.

## Project Structure

### Stage 0: Data Description
- **Purpose**: Initial exploration and description of the input Excel file
- **Input**: `BRANHAM_V2.xlsx` (Excel file with multiple sheets)
- **Output**: Basic data structure information (column names, data types, sheet structure)

### Stage 1: Effect Size Collapsing
- **Purpose**: Aggregate multiple effect sizes from the same study using Borenstein et al. (2009) formula 24.5
- **Key Features**:
  - Handles studies with multiple outcomes by calculating weighted averages
  - Assumes correlation of 1.0 between outcomes (conservative approach)
  - Processes data sheet by sheet, identifying study groups separated by blank rows
  - Combines multiple effect sizes into single aggregated values
- **Output**: Collapsed effect sizes saved as Excel file with timestamp

### Stage 2: Individual Meta-Analyses
- **Purpose**: Perform separate meta-analyses for each analysis group
- **Method**: Random effects model using Hedges' g
- **Calculations Include**:
  - Combined effect size and confidence intervals
  - Prediction intervals
  - Credibility intervals
  - Heterogeneity statistics (Q, I², τ²)
  - Z-tests for significance
- **Output**: Comprehensive results table with all meta-analytic statistics

### Stage 3: Visualization
- **Forest Plots**: Visual representation of individual study effects and overall estimates
- **Funnel Plots**: Assessment of publication bias using trim-and-fill method
- **Features**:
  - Automatic detection of missing studies
  - Visual distinction between original and imputed studies
  - Export capabilities to PDF format
  - Text summaries of trim-and-fill results

### Stage 4: Between-Group Comparisons
- **Purpose**: Statistical comparison between different analysis groups
- **Method**: Mixed-effects meta-regression
- **Statistics Calculated**:
  - Q-between: Heterogeneity between groups
  - Q-within: Heterogeneity within groups
  - Associated p-values and degrees of freedom
- **Output**: Comprehensive comparison table for all group pairs

## Key Dependencies
```r
library(readxl)      # Excel file reading
library(metafor)     # Meta-analysis calculations
library(writexl)     # Excel file writing
library(dplyr)       # Data manipulation
```

## Input Data Requirements
- Excel file with multiple sheets containing study data
- Required columns:
  - `ID`: Study identifier
  - `ID único de muestra`: Unique sample identifier
  - `Hedges' g (effect size)`: Effect size values
  - `g variance (std error ^2)`: Effect size variances
  - `Authors`: Author information
  - `Año`: Publication year
  - `Outcomes`: Outcome measures

## Output Files
1. **Collapsed Effect Sizes**: `ART-736canetMeta-EScolapsados_[timestamp].xlsx`
2. **Meta-Analysis Results**: `ART-736canetMeta-analisis-[timestamp].xlsx`
3. **Group Comparisons**: `ART-736canetMeta-analisis-grupos-[timestamp].xlsx`
4. **Visualizations**: PDF files for forest plots and funnel plots
5. **Trim-and-Fill Results**: Text files with publication bias analysis

## Methodological Notes

### Effect Size Aggregation
- Uses Borenstein et al. (2009) formula 24.5 for combining correlated effect sizes
- Conservative approach assumes perfect correlation (r = 1.0) between outcomes
- Increases variance estimates to account for dependency

### Publication Bias Assessment
- Trim-and-fill method identifies potentially missing studies
- Visual inspection through funnel plots
- Quantitative assessment of bias impact on overall estimates

### Heterogeneity Analysis
- I² statistics for quantifying heterogeneity
- τ² estimates for between-study variance
- Q-statistics for testing homogeneity assumptions

## Usage Instructions
1. Ensure input Excel file is in the working directory
2. Update the `archivo` variable with your file name
3. Run stages sequentially (0 → 1 → 2 → 3 → 4)
4. Check output files for results and visualizations

## References
- Borenstein, M., Hedges, L. V., Higgins, J. P., & Rothstein, H. R. (2009). Introduction to meta-analysis. John Wiley & Sons.
- Meta-Essentials FAQ: https://www.erim.eur.nl/research-support/meta-essentials/frequently-asked-questions/

## Notes
- The script includes extensive error handling and progress reporting
- Visualization functions support both screen display and PDF export
- All calculations follow established meta-analytic best practices
- Code is modular and can be adapted for different datasets
