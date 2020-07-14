
This script summarizes key QC metrics from the automated `eddy QC` tools, i.e., the eddy quad PDFs (Bastiani et al., _NeuroImage_, 2019), and `MRTrix` for the n=`r nrow(df)` participants who are eligible for inclusion.

In script 1, preform correlations, and then PCA. PC scores (typically first, or first and second) can be used as 'quality' regressors in other analyses.

In script 2, we perform automated QC, on the basis of 6 variables. Our DWI working group suggested thresholds for key QC metrics, on the basis of analysis of subsets of the SPINS, POND, and HCP datasets. These thresholds were found to reliably predict a number of different visual QC ratings from different raters. The suggested thresholds were as follows:

Assumes you have run `eddy` and `mrtrix`. `eddy` is currently run by staff piplines, and `mrtrix` is run by trainees, as desired.
