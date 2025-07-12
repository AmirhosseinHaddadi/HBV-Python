# 💧HBV hydrological model in Python
HBV hydrological model in Python with a complete Unceratinty-Sensitivity analysis

⚠️ This code has been developed for only educational and demonstration purposes. All data used in this implementation is synthetic and does not represent any real-world dataset or case study. No actual hydrological records or proprietary information have been utilized in this educational material.

## 📥Requierd Data
For using the model, you need to upload the HBVinput.xlsx file.
This file contains several datasheets:

1-Precipitation and Temperature time series data (mm and °C) in order

2-Observed streamflow data (m3/s or mm/day)

3-Monthly potential evapotranspiration (mm/month) and Average monthly temperature	(°C)

4-Parameter bounds

5-Initial values and general model settings

*The excel file is availabe in Github files -->

*You can change the data with yours and also, add, remove or adopt the parameters and their range.

    Input File: HBVinputs.xlsx


## 🔷Table of contents

🔹**1- Importing the libraries**

-> numpy / pandas / scipy.stats / matplotlib.pyplot / sklearn.metrics / itertools / scipy.optimize / SALib

🔹**2- Extracting the essential data from the input excel file**

-> This part loads and prepares the input data required for running the HBV hydrological model. It reads precipitation, temperature, and month information from the InputPrecipTemp sheet, as well as observed discharge values (Qobs), and monthly potential evapotranspiration (dpem) from MonthlyTempEvap. Initial values such as snow storage, soil moisture, and model configuration parameters are extracted from the IV sheet. These include key variables like the snow/rain threshold temperature (tt), watershed area (area), and initial conditions for the model's storage components (S_1, S_2). The number of simulations is set to 100 by default, and an optimization criterion is selected from the input. Lastly, parameter bounds for model calibration are retrieved from the Bounds sheet, which define the lower and upper limits for each model parameter.


🔹**3- Sampling Methods**

  3.1. Latin Hypercube Sampling

  3.2. Random Uniform Sampling

  3.3. Grid Sampling

  3.4. Normal Distribution Sampling

   
🔹**4- Start HBV Simulating (Fast and Slow Reservoirs)**

-> This section performs the core hydrological simulation using the HBV model for a set of sampled parameter combinations. It defines two key configurations: a small coefficient for capillary flux from storage S1 to the soil (cflux_coeff), and a smoothing window size for filtering the output discharge. For each parameter set, the model is initialized with snow, soil moisture, and storage states (S1, S2), then iterates through each time step (daily). During each day, it calculates snow accumulation and melt, potential and actual evapotranspiration, infiltration into the soil, and capillary return flow from S1. Water movement through the fast, intermediate, and slow runoff reservoirs is simulated, and the resulting discharge is computed and stored. Afterward, the simulated discharge is smoothed and evaluated against observed discharge using several performance metrics: NSE, RMSE, correlation, and volumetric bias. The best-performing simulation (based on a selected criterion) is identified, and all results—including the parameter values and NSE—are saved to an Excel file for further analysis.

    Code Output: HBV_Simulation_Smoothed.xlsx


🔹**4-1- A guid to Develop HBV with three reservoirs**

🔹**5- Final simulation with best params**

-> This script runs the HBV model using the best-performing parameter set previously identified, and generates detailed time series outputs for hydrological variables. It starts by setting a small capillary flux coefficient (cflux_coeff) and initializing the model’s storage states (snow, soil, s1, s2). For each day in the simulation period, the model calculates potential evapotranspiration (ep), snow accumulation and melt, actual evapotranspiration (ea), and infiltration (dq). Capillary flux is added from storage s1 back to the soil based on soil moisture deficit. The model then routes water through three conceptual reservoirs to calculate runoff (qcms), and stores the values of all key variables in time series lists. After the loop, the simulated discharge is smoothed, and model performance is evaluated using NSE and correlation with observed discharge. Finally, three Excel sheets are created: one with the full time series of hydrological components, one summarizing the best parameter values, and one reporting the model's final performance metrics.

    Code Outputs: HBV_FinalResultStruct_Smoothed.xlsx + reporting NSE and Correlation

🔹**6- Plotting the time series (Simulated vs Observed streamflow)**

    Code Outputs: HBV_Simulation_TimeSeries.xlsx + Time series plot

🔹**7- Forward Uncertainty Propagation**

  7-1- FOSM method

    Code Outputs: HBV_FOSM_Sensitivity.xlsx + FOSM plot
  
  7-2- Monte Carlo method
  
    Code Outputs: HBV_Uncertainty_MonteCarlo.xlsx + Monte Carlo plot

🔹**8- Backward Uncertainty Propagation**

  8-1- GLUE method

    Code Outputs: HBV_GLUE_Uncertainty.xlsx + GLUE plot

🔹**9- Calibration and Validation (Soon!)**

🔹**10- One-at-a-Time (OAT) Sensitivity Analysis** 

    Code Outputs: HBV_OAT_Sensitivity.xlsx + OAT plot for each parameter 
    
🔹**11- HBV Sobol Sensitivity Analysis**

    Code Outputs: HBV_Sobol_Sensitivity.xlsx + HBV_Sobol_Interactions.xlsx + Direct and Total effect plots + Interaction plots

## 🔰Acknowledgements
I would like to express my sincere gratitude to Prof. Amir AghaKouchak, Dr. Navid Nakhjiri, and Dr. Emad Habib for providing the MATLAB source code of the modified HBV hydrologic model, which includes automatic parameter uncertainty estimation based on the Generalized Likelihood Uncertainty Estimation (GLUE) method. Their valuable educational code has been instrumental in advancing my python code, and I deeply appreciate their efforts in developing and sharing this computational tool. [(https://amir.eng.uci.edu/files/2025/05/HBV.zip)]

Also, I gratefully acknowledge Dr. Farkhondeh Khorashadizadeh for her insightful lectures on Uncertainty Analysis in Hydrological Models at Sharif University of Technology. [(https://sharif.edu/~khorashadi/index.html)]

## Contact for Support
Should you encounter any issues with the code or have questions and suggestions, please don’t hesitate to reach out. You can contact me via email or LinkedIn:

[amir6haddadi@gmial.com] | [(https://www.linkedin.com/in/amirhossein-haddadi-aa8b54282/)]

Looking forward to your feedback!
