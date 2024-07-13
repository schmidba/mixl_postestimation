# mixl_postestimation
Estimation and postestimation framework for R package mixl

INTRODUCTION GUIDE FOR USING MIXL

This is a quick guide how to get started with this code framework for estimating choice models with the R-package mixl (available on CRAN):

Molloy, J., F. Becker, B. Schmid and K. W. Axhausen (2021) mixl: An open-source R package for estimating complex choice models on large datasets, Working Paper, 1408, Institute for Transport Planning and Systems (IVT), ETH Zurich, Zurich.


————————————————————————————————

IMPORTANT: An up-to-date documentation/user guide on how to install and run mixl can be found here:

https://github.com/joemolloy/fast-mixed-mnl/blob/master/vignettes/user-guide.md

It is recommended that you install the most recent versions of R and Rstudio.

————————————————————————————————


0. This framework for efficiently using mixl is at the same time highly flexible but also extremely organised. The code in the scripts is commented whenever appropriate.


1. Store your dataset in the 0_data folder. One row has to correspond to one choice situation. In cases where the availabilities of alternatives vary, all the attribute values of the non-available alternatives should be set to a numeric value, -99, -97 or 9999, to ensure that the postestimation functions work properly. 

Note: PCW_original_data_codebook.pdf includes a description of the attributes used in the provided modelling examples. The original data can be downloaded from www.doi.org/10.5905/ethz-1009-40


2. Open Zz_source_code.R and choose your path settings. You can add paths for multiple machines easily, so R automatically recognises where you are working from. Define the number of cores on these machines (note that mixl has linear speedups with increasing number of cores). There are different subfolder options that can be joined to the main path.


3. Create your utility script and place it in the 1_estimation folder. Note: For the sake of good organisation, you have to add _utilities at the end of the R filename for automatic file detection. Use the guide provided in the working paper Molloy et al. (2020) to create your utility script, or just use one of the examples provided in the 1_estimation folder to get familiar with the notation. 

Note: The examples are modified versions of the models presented in Chapter 4 of 4.3_schmid_2019_dissertation.pdf

Schmid (2019) Connecting Time-Use, Travel and Shopping Behavior: Results of a Multistage Household Survey, PhD Dissertation, Institute for Transport Planning and Systems (IVT), ETH Zurich, Zurich.


4. Open 0_RUN_MODEL.R and choose your settings at the top. Note: You can either use zero starting values, manually defined starting values (Zz_start_values_manual.R), or estimates from a previous model. Also define columns containing the availabilities of each alternative (they have to be specified as dummy variables), and do some final data processing if needed. More information is provided in the script.


5. Execute 0_RUN_MODEL.R. Output files are stored in the corresponding folders as defined in Zz_source_code.R. This includes:

- __model.txt output table with estimation results

- __est.Rdata file with estimates (can be subsequently used as starting values)

- __texreg.Rdata file for later use with LATEX. In the folder 1_estimation/Xx_multitable/, multi_tex.R allows you to combine different models into one LATEX table

- __mod.Rdata file which includes all model information (required for post-estimation)

- __posteriors.csv file with the posteriors (includes all parameters that were specified as …_RND in the model file/utility script)


5. Open 0_POSTESTIMATION_ANALYSIS.R in the 2_postestimation folder. Load the model file, define the names of alternatives (no special characters allowed, ONLY letters and numbers), define the availabilities of each alternative, if you are working with a test dataset, etc. Run the run_analysis(…) function, which automatically generates the most relevant figures and numbers, including:

- hitrate and confusion matrix (optimiser and economist method): 

- outlier detection (worst mean probabilities per ID)

- elasticities and marginal probability effects (to be defined), separately stored for discrete and continuous variables

- list of OLS coefficients of each attribute on the choice probability to detect cases where the model has problems to predict

- means of attributes in case of low (to be defined) choice probabilities

- list with the means of all attributes for partworth analysis

- list of insignificant parameters

- plot with relative choice frequencies


6. More specific (i.e. application-dependent) postestimation examples are included in 0_POSTESTIMATION_ANALYSIS.R. This includes:

- calculation of standard errors for a function of estimated coefficients (a wide range of functions are included in Zz_source_code.R)

- posterior and willingness-to-pay (WTP) analysis

- partworth analysis
