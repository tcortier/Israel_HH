# Factors Associated with the Transmission of the Delta SARS-CoV-2 Variant in Households: The Israeli COVID-19 Family Study (ICoFS)

## Dependencies

- C++ compiler
- Boost C++ library
- R

## Running the Transmission Model Inference

### 1. Compile the Code

You can either use the `Makefile` in the `MCMC_HH` folder or compile the C++ code using Visual Studio Code.

### 2. Data

The original data is not included in this repository for privacy reasons, but we provide a filtered and formatted dataframe compatible with the C++ code. The data is stored in a `.txt` file with 11 unlabeled columns:

1. Individual ID  
2. Household ID  
3. Household size  
4. First positive test date (1000 if not infected)  
5. End of follow-up period  
6. Infectious status (0 = uninfected, 1 = infected)  
7. Immunization status:  
   - 1: 2 doses (more than 90 days ago) - adults  
   - 2: Unvaccinated - children  
   - 3: Vaccinated - children  
   - 4: 1 dose, not previously infected - adults  
   - 5: 2 doses (less than 90 days ago) - adults  
   - 6: Unvaccinated, not previously infected - adults  
   - 7: 3 doses - adults  
   - 8: Unvaccinated, previously infected - adults  
   - 9: 1 dose, previously infected - adults  
8. Age  
9. Isolation status (0 = not isolated, 1 = isolated)  
10. Gender (1 = female, 2 = male)  
11. Symptomaticity (0 = asymptomatic, 1 = symptomatic)

### 3. Launch the MCMC Chain

Use the `launch_mcmc_git.R` script to run the C++ code. The output is iteratively written to a `.txt` file, with each column corresponding to a specific parameter.

## Analyzing the Chains

- The `analyse_mcmc_chains.R` script allows you to assess convergence and mixing of the chains. It also enables you to compare the posterior distribution of transmission factors.
- To compare two models, use the `model_comparison.R` script. This script focuses on comparing the default model with the model that includes children’s contact rates.

## Running Model Simulations

Model simulations are executed using Rcpp code, which requires the Rcpp library and a compiler. The `household_simul_epidemy.R` script simulates epidemiological dataframes from transmission parameters. You can choose to simulate using particles from the posterior distribution or the median of posterior distributions.

## Simulation and Sensitivity Analysis

The `simulation_and_sensitivity_analysis.R` script allows you to:
- Analyze a given set of sensitivity models
- Analyze infection data from simulations
- Analyze the results of posterior distributions calibrated on simulated datasets
