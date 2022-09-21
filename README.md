# Brazil_cprcm_CMORise
Using mip_convert to process CSSP Brazil CPRCM output pp files to CMOR-compliant netCDF 

## Background
The Brazil CPRCM experiment includes three simulations:  the Hindcast simulation is performed for 1998-2008 with lateral boundary conditions (LBCs) provided by the ERA-Interim dataset, dynamically downscaled by a 25km RCM. The present-day control (PD CNTRL) simulation covers the same period and its LBCs are taken from the HadGEM3 atmosphere/land model at 25km resolution (HG3 N512). Sea surface temperatures (SSTs) and sea ice are from the present-day daily 0.250 dataset (Reynolds et al., 2007). The Future AD 2100 experiment simulates 10 years under AD 2100 RCP8.5 forcing with LBCs from HG3 N512. The future forcing include GHG concentrations for the year 2100 taken from the RCP 8.5 scenario ( Moss et al., 2010) (Moss et al., 2010) and sea surface temperatures (SST) anomalies between the 1975-2005 and 2085-2115 from the HadGEM2-ES CMIP5 RCP8.5 simulation, added to the present-days SSTs. For this reason, the time series plots in this paper are using the 1998-2008 period for both the PD and the AD 2100 simulations.

### Lateral Boundary Conditions:
   *	The lateral boundary conditions for the hindcast simulations (MO rose suites mi-ba751 and mi-bb055) are provided by Era-Interim (1998-2007) data at ~75km, dynamically downscaled to convection permitting scale (~ 4.5 km grid spacing) using two step nesting. The CPRCM simulation at 4.5km is nested in 25 km HadREM3-GC3.1-N512, which in turn is nested in ERA-Interim. 
   * The lateral boundary conditions for the PD simulations (MO rose suites mi-ba488, mi-bb069) are provided by the HadGEM3 atmosphere/land model at 25km resolution HadGEM3-GC3.1-N512, (MO rose suite: u-ab261), dynamically downscaled to convection permitting scale (resolution ~ 4.5 km) using one-step nesting. 
   * The lateral boundary conditions for the future, 2100AD climate simulations (mi-ba489, mi-bb070) are provided by the HadGEM3 atmosphere/land model at 25km resolution HadGEM3-GC3.1-N512, (MO rose suite: u-ab268), dynamically downscaled to convection permitting scale (resolution ~ 4.5 km) using one-step nesting. 

