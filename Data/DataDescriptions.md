# Data Descriptions

This folder contains several data sets from Passaro et al. These data sets can be used to test the accompanying neural activity score code. Figure references refer to Passaro et al.

Descriptions and details for the files can be found below.

Folders contain files for individual plates, as well as compiled files.

File descriptions:
1. '1_AllDaysCompiled_PlateX.xlsx' - all .csv files generated from AxIS for each plate. Data has not been analyzed yet, simply processed from .raw signal files. These files were compiled via compileAndMerge() or manually.
2. '2_AnalyzedAllParameters_PlateX.xlsx' - all MEA parameters (that AxIS calculates) have been averaged by group and organized for downstream analysis. These files can be used for individual parameter analysis. Generated via analyzeStatCompilerFiles().
3. '3_Zscore_PlateX.xlsx' - similar to the previous file, but all parameters have been normalized to standard (z) scores. These files are useful for PCA, NAS calculation, or other analyses requiring normalized data.
4. '4_NAS_PlateX.xlsx' - include column with calculated NAS values, a sheet with additional NAS values (normalized, outliers removed, and scaled to 0-1), and a sheet with scaled NAS values in GraphPad Prism (XY) format for graphing and statistical analysis.

## Ontogeny
These files were generated from raw MEA recordings in typical mouse ESC-derived neural culture conditions. Figs 1 and 2 were generated from this data. Coefficient of variation values used to generate S1 Fig also provided in the /Ontogeny/Compiled/ folder.


## Neural enhancement experiments
These files were generated from raw MEA recordings in two experiments:
1. Comparison between DMEM/Neurobasal-based media and BrainPhys-based media (Fig 3A)
2. Analysis of the effects of C2C12-conditioned media on neural network ontogeny (Fig 3B)

## Neural network disruption
These files were generated from raw MEA recordings in two experiments:
1. Microglia (BV2 cells)-mediated disruption of neural activity (Fig 4A)
2. BV2-conditoned media-mediated disruption of neural activity (Fig 4B)
	- Note: n=6 for Control and 7 for other groups, so '2_Analyzed...' files had "Rep 7" values for Control (7 and 14 in Compiled file) deleted manually prior to further analysis, and NAS values were entered into GraphPad manually.

## Neurotoxicity screening
Additional file descriptions
1. ExperimentLog files - files containing metadata for toxicity screening data
2. '5_NAS_AUC_PlateX.xlsx' - AUC values for all parameters including NAS - used to fit curves for EC50 extrapolation in GraphPad
3. '6_AllCompounds_AllAUC.xlsx' - GraphPad formats from '5_NAS_AUC_PlateX.xlsx' compiled for all parameters and all compounds
This data was used to generate Fig 5.

/All Compounds/ - These files were generated from raw MEA recordings analyzing potential neurotoxic compounds from EPA libraries (ToxCast and DNT). Compound folders are named by one compound from the plate, but each plate contains many compounds.

The data in these files was used to produce Fig 5, with a subset of compounds (aspirin, tamoxifen, picoxystrobin) used in Fig 5A-F and all compounds (with detected toxicity) used for Fig 5G.

/All Parameter EC50s/ - These are the EC50/IC50 values extrapolated from GraphPad for each parameter, as well as a summary file with comparisons used to generate S2 Table.