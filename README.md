![DOI badge](https://zenodo.org/badge/DOI/10.5281/zenodo.3939310.svg)
# Neural activity score
A novel index for analyzing microelectrode array data.

I hope you find this measurement and approach useful for analyzing neural activity. If you use or modify neural activity score (NAS), please cite the original publication.

Code information/instructions are included below. Descriptions of included data files are included in the 'DataDescriptions.md' file in the /Data/ folder.

# Setup and usage instructions
Note: This code is written for data generated from the StatCompiler function in AxIS Software (Axion Biosystems, Atlanta, GA). If using MEA data from other software/systems, the code will need to be edited or data reformatted to a similar format (see customization suggestions below). Alternatively, NAS can be calculated manually using the provided formula in Passaro et al. (to be linked upon publication), though note that results may vary if parameters are calculated differently or omitted.

## Setup
The code hosted here is written in Python and presented in a Jupyter notebook for ease of use and modularity.

### Install Python 3
To install Python 3, follow the instructions here: https://www.python.org/downloads/ or install a Python distribution such as Anaconda: https://docs.anaconda.com/anaconda/install/

Anaconda is recommended as necessary packages/dependencies, including Jupyter, are included.

### Install Jupyter
To install Jupyter notebook or JupyterLab, refer to the following instructions: https://jupyter.org/install

### Install dependencies
The following dependencies will be needed, and are recommended to install/update prior to beginning:
Note: versions used and tested are noted in parentheses. If compatibility issues with other versions arise, try installing the following versions.  
- tkinter (8.6)  
- pandas (1.0.0)  
- openpyxl (3.0.3)  
- numpy (1.18.1)  
- scipy (1.4.1)  
- tqdm (4.42.0) (optional)

These packages can be installed with pip or conda.

## Usage
### Run the notebook
Download the .ipynb file(s) from this repository.
NeuralActivityScore.ipynb is suitable for most typical experiments.
NeuralActivityScore_Tox.ipynb is used to analyze toxicity data and is customized to incorporate additional dose, compound, and plate metadata.

Refer to the following instructions for launching the desired notebook: https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/execute.html

### Run the following cells/modules as necessary
Note: Function cells are split. Run the first cell to define the function, then the second to execute the function. This is done to facilitate editing/debugging, as well as quick usage for multiple data sets once all functions are defined. If using JupyterLab, definition cells can be collapsed after running.

#### Import
Run this to import necessary packages.

#### tqdm
Run if tqdm progress bars are to be used. Tested primarily using JupyterLab.

Note: If tqdm is not used, remove tqdm() containers in individual cells (typically found at large for loops).

#### Parent/Destination specification
Run to specify experiment folder and destination folder. Follow these file structure guidelines for parent folder:

If inputting individual StatCompiler .csv files:
Experiment folder > Plate subfolder(s) > DIV subfolder(s) > StatCompiler.csv file(s)
Example file tree:
C:/
    MEAExperiment/
        Plate1/
        Plate2/
        Plate3/
            DIV1/
            DIV2/
            ...
            DIV21/
                DIV21_StatCompiler.csv

If inputting compiled .xlsx file(s) (with individual recordings as sheets):
Experiment folder > Plate subfolder(s) > Compiled .xlsx file(s)
C:/
	MEAExperiment/
		Plate1/
			Compiled.xlsx

If using the 'NeuralActivityScore_Tox.ipynb' code, there is one extra parent folder level containing compound names (named with example compounds from corresponding plates).

#### Compile and merge
If inputting individual .csv files (with the above file structure), this function will copy them (useful for copying from external drive and/or separating from large raw files) and compile them into one .xlsx file to be used in the next step.

If inputting compiled .xlsx file, can skip this cell.

#### Analyze StatCompiler files
This function will take compiled .xlsx files with all individual recording data (as individual sheets, generated from previous cell) and perform the following:
- Determine groups, replicates, time points (days, assuming 1 recording/day)
**Note: Groups must be defined on first sheet of compiled .xlsx file (in the 'Treatment' row) prior to running. If groups have not been defined, an error will be raised with instructions to define groups before proceeding.**
- Generate .xlsx file with all parameter averages for each plate, rep (well), day, and group.
This .xlsx file can be used for individual parameter analysis if desired.

#### Merge plate output files
If multiple plates were recorded with identical layouts, this function can be used to fix replicate numbers and concatenate results for downstream analysis.

For example, if three 48-well plates were recorded with 6 groups of 8 reps on each plate, the previous cell would output three separate files (one per plate) and reps would be labeled 1-8 in each. This function would output one file with all data, with the first plate having rep labels 1-8, the second plate 9-16, and the third plate 17-24 so the data can be analyzed together.

#### Normalization
This function will normalize all values to standard scores (z-scores). This is an important step prior to NAS calculation to ensure parameters are weighted equally prior to NAS calculation.

#### NAS calculation (also referred to in code as index score)
This function takes the normalized values and calculates NAS using factor loading coefficients, as described in Passaro et al.

NAS values are added as a separate 'NAS' column and on a new sheet. On the new sheet, NAS values are also normalized to remove outliers (-3 > z > 3), scaled to 0-1, and formatted for easy copy/paste to GraphPad Prism for graphing and statistical analysis.

#### AUC calculation
This function calculates the area under the curve over time for each group and parameter. This can be used for quick comparison between groups (though two-way RM ANOVA (NAS x time) is recommended for statistical analysis).

This function is particularly useful for generating AUC values that can be used for concentration-response curve generation and EC50 calculation in toxicity studies (see Passaro et al.).

## Customization
The modular organization of the Jupyter notebook allows for easy customization of individual functions, testing/debugging, and re-running analysis from various points.

This code was written to analyze data recorded with the Maestro system and AxIS Software (Axion Biosystems). If other systems/platforms/software are used, the data can be reorganized to fit similar organization/layout or the code can be modified to work with other data formats.

The code is commented to describe steps and array/data structures, and it is written to frequently export files after each major function/step to provide flexibility with customization, whichever steps are needed to add to an existing analysis pipeline. Example files are provided for each of these steps both for testing and to provide templates to assist with customization.

Finally, the neural activity score (NAS) formula has been developed to include 25 common neural activity parameters. If these parameters are calculated differently or some are omitted, results may differ. However, similar calculations, substitutions with similar parameters, or omissions may be necessary due to platform/pipeline differences and may still result in a useful index (especially if the changed/omitted parameters have relatively low weights).

If changes to the NAS formula are made, regression analysis (NAS vs. time, control conditions) and experimental validation are recommended to ensure neural network ontogeny is still accurately being measured before interpreting results applied to future experiments.

## FAQ/Troubleshooting
To be updated when questions arise.

## Contact
Please contact Austin Passaro at passaroa@uga.edu with comments, questions, or concerns.
