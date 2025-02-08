# Risks, Rates, and Rays: The Financial Realities of Brazil's Solar Revolution
This repository contains the datasets and code used in the study, 
*Risks, Rates, and Rays: The Financial Realities of Brazil's Solar Revolution*. 
The study explores how macroeconomic factors, such as interest rates, 
influence the Levelised Cost of Energy (LCOE) for solar photovoltaic (PV) projects in Brazil. 
The materials include calculations for Weighted Average Cost of Capital (WACC), 
LCOE estimates for auction-awarded projects from 2014 to 2022, 
and scenario projections for financing conditions through 2029.

## Contents
This repository contains the following files and directories:

### Jupyter Notebooks
1. `cost-of-capital.ipynb`: Calculates the Weighted Average Cost of Capital (WACC) for solar PV projects using multiple datasets and produces the final WACC dataset for further analysis. Steps include:
   - Estimation of the BNDES rate.
   - Calculation of global risk-free rates, country default spreads, technology premiums, and cost of debt/equity.
   - Application of IRENA criteria to determine debt share and final WACC calculation.
   
2. `lcoe.ipynb`: Calculates the Levelised Cost of Energy (LCOE) for solar PV projects using energy auction data and WACC estimates. Key steps include:
   - Cleaning and structuring energy auction data for analysis.
   - Estimation of OPEX and CAPEX baselines, adjusted for inflation.
   - Integration of WACC data from the first notebook to calculate LCOE with financing costs.
   - Analysis of changes in financing costs between 2014 and 2022.
   - Visualization of key metrics, including LCOE trends and auction dynamics.
   
3. `scenario-projection.ipynb`: Scenario projections 2024-2029, WACC calculations, LCOE projections, financing cost analysis. Steps include:
   - Generate Flat, Upward, and Downward scenarios for yields and inflation using regression results and historical trends.
   - Project monthly NTN-B bond yields and calculate corresponding BNDES rates.
   - Combine BNDES rate, technology premium, equity premium, and leverage to calculate WACC for each scenario.
   - Build CAPEX and OPEX baselines, incorporating learning curves (15% for CAPEX, 5% for OPEX).
   - Calculate LCOE for each scenario and assess financing costs.
   - Compare financing contributions across scenarios and calculate changes in financing costs from 2024 to 2029.
   - Plot LCOE trends, financing cost breakdowns, and percentage contributions (CAPEX, OPEX, and financing) under each scenario.


### Input Data for `cost-of-capital.ipynb`
1. `bndes-rates.csv`: 
   - **Monthly data (January 2014 to June 2024)**:
     - Subsidised TJLP BNDES rate (`bndes_tjlp`).
     - Observed TLP BNDES rate (`obs_bndes_tlp`).
     - NTNB bond yield (`ntnb_5yr_yield`).
     - Inflation data (`cpi_ipca`).
   - **Purpose**: Used to estimate the BNDES rate, compare with observed TLP rates, and create a unified `bndes_rate` variable.

2. `us-treasury-yield.csv`: 
   - **Monthly data (January 2014 to June 2024)**:
     - U.S. Treasury bond yields.
   - **Purpose**: Used to calculate the country default spread (`cds_brazil`) by subtracting U.S. Treasury yields from BNDES rates.

3. `solar-installed-capacity.csv`: 
   - **Data on Brazil's solar PV capacity (January 2014 to June 2024)**:
     - Cumulative installed capacity as a percentage of total electricity capacity.
   - **Purpose**: Used to estimate technology premiums and assign debt share based on IRENA’s market maturity criteria.

4. `erp-mature-market-sp500.csv`: 
   - **Equity risk premium data (January 2014 to June 2024)**:
     - Monthly S&P 500 equity risk premium values from Damodaran (2024).
   - **Purpose**: Used to calculate the cost of equity.
   
### Output Data for `cost-of-capital.ipynb`
1. `bndes_wacc_calculations.csv`: 
   - **Final output**:
     - Contains calculated WACC values for Brazil's solar PV projects, alongside variables such as cost of debt, cost of equity, and market maturity classifications.

 
### Input Data for `lcoe.ipynb`
1. `solar-auctions.csv`:
   - **Dataset on solar PV projects awarded in auctions (195 projects)**:
     - Key variables: `date`, `invest_auction`, `nominal_capacity_mw`, `sale_price_auction`, `supply_start_date`, `auction_ipca`.
   - **Purpose**: Provides auction data for estimating CAPEX, OPEX, and LCOE.

2. `bndes_wacc_calculations.csv`:
   - **Output from the first notebook**:
     - Contains WACC estimates by auction date for integration with project data.
   - **Purpose**: Links financing conditions to auction projects for LCOE calculation.

3. `currency-brl-usd.csv`:
   - **Exchange rate data**:
     - Monthly BRL/USD exchange rates.
   - **Purpose**: Enables conversion of LCOE to USD.

4. `us-cpi.csv`:
   - **US Consumer Price Index (CPI)**:
     - Monthly CPI data used to adjust USD values for inflation.
   - **Purpose**: Converts nominal USD values to 2022 constant dollars.

   
### Output Data for `lcoe.ipynb`
1. `lcoe_solar_analysis.csv`:
   - **Final output**:
     - Contains calculated LCOE values for each project, both with and without WACC.
     - Includes variables such as CAPEX, OPEX, and discounted energy production.

### Input Data for `scenario-projection.ipynb`
1. `yield-correlation.csv`:
   - **Content**:
     - Monthly data (October 2017 to June 2024) on:
       - `ntnb_5yr_yield`: NTNB bond yield (5 years).
       - `cpi_ipca`: Inflation (IPCA).
       - `yr10_gov_bond_yield`: 10-year government bond yield (BR10YT).
   - **Purpose**:
     - Analyse correlations and run regressions between yields and inflation.
     - Generate Flat, Upward, and Downward scenarios for yields and inflation rates.
     - Project monthly changes for the NTNB bond yield based on BR10YT and inflation scenarios.
	 
### Output Data for `scenario-projection.ipynb`
1. `projected_ntnb_yields.csv`:
   - **Content**:
     - Projections for monthly NTN-B bond yields under Flat, Upward, and Downward scenarios from July 2024 to December 2029.
     - Key variables include:
       - `Date`: Date for each projection.
       - `NTNB_Change_Flat`, `NTNB_Change_Upward`, `NTNB_Change_Downward`: Monthly changes for NTN-B bond yields in each scenario.

2. `scenarios-solar.csv`:
   - **Content**:
     - Comprehensive dataset including yearly yield and inflation scenarios, NTN-B bond yield projections, and financing cost contributions.
     - Key variables include:
       - Yield projections: `Flat_10YR_Yield`, `Upward_10YR_Yield`, `Downward_10YR_Yield`.
       - Inflation scenarios: `Flat_Inflation`, `Upward_Inflation`, `Downward_Inflation`.
       - NTN-B bond yield projections: `NTNB_Flat_Scenario`, `NTNB_Upward_Scenario`, `NTNB_Downward_Scenario`.
       - BNDES rate calculations for each scenario.
       - Cost of debt and equity, WACC, and LCOE projections under all three scenarios.