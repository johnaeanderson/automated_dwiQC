
 
<p align=center> <b>AUTOMATED QC OF DWI DATA </b></p>

<br>

In 2019, the Kimel lab formed a DWI working group. One of its tasks was to create a method of automatically performing QC on large DWI datasets, as a complement to visual review. Ultimately, we found very high agreement between trained human raters and 6 quality metrics derived from `eddy` and `MRTrix`. The method was tested on 3 large datasets (SPINS, POND, and a subset of HCP) and compared to ratings of 5 independent human raters. 

The metrics, and their suggested thresholds, were as follows:

| Metric | Absolute motion | Relative motion | Percent outliers | Average SNR | Average CNR | Residual noise |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| <b>Suggested threshold</b> | >= 2 (mm) | >= .5 (mm) | >= 2 (%) | <= 20 | <= 1.5 | >= 6 | 

-----

<p align=center><b>Repo Contents</p></b>

This repo contains code to format and review the 6 requiste metrics, produce a score for each participant that can be used as a quality regressor in future analyses, and indicate which participants should likely be removed from further analyses. Specifically:

`code`
- `01_qualityScore.Rmd`. This script performs two tasks. First, it examines the correlations between the 6 QC metrics. The intent is to ensure that, on a global level, there are no unexpected associations between quality metrics.  Second, it performs PCA. The intent to to generate a 'quality regressor' that can be used in subsequent analyses, assuming the first one or two PCs capture a large proportion of variance. 
- `02_excludeParticipants.Rmd`. This script visualizes participant scores on the 6 QC metrics, and summarizes which participants should be excluded on the basis of the groups' established thresholds. 

`/data`
- `/input`  
   - `eddyMetrics.tsv`.  This .tsv is generated by lab pipelines for data found in the `/archive`. Specifically, it can be found in `bids/pipelines/dwiprep/`.
   - `mrtrixResidualNoise.txt`. This output should be generated by the user (it does not, at present, exist in the `/archive`. A script to do so can be found at [here (currently private)](https://github.com/navonacalarco/thesis-2.0/blob/master/scripts/02_mrtrix.sh).

- `/output`.   
   - `df_dwiQC_PC.csv` is generated by `01_qualityScore.Rmd`. It is a dataframe containing the 6 variables of interest, as well as the first PC score. 
   - `excludeParticipants.txt`is generated by `02_excludeParticipants.Rmd`. It contains the IDs of those participants exceeding exclusion thresholds.

__Examples__.  
When knitted in RStudio, `01_qualityScore.Rmd` should generate a report similar to the one [here](https://rpubs.com/navona/SPINS_DWI_QCeddyMRTrix), and `02_excludeParticipants.Rmd` as [here](https://rpubs.com/navona/SPINS_DWI_QCautomated). For more context, notes from the DWI working group meetings [here](https://drive.google.com/drive/folders/1Qkd7NsJboGCjJw2KzBlai3sx9bpPn__q?usp=sharing)
