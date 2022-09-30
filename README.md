# Brazil cprcm CMORise
Converting the output from the Met Office CSSP Brazil convecting-permitting model (CPRCM) output into a single-variable
netCDF files consistent with CMOR 3.7, CF-1.7 CMIP-6.2 and CF standards.    

## Climate forcing and Lateral Boundary Conditions (LBCs):
The Brazil CPRCM experiment includes three simulations performed with the Met Office regional environment model
(MOHC-REM3), using the regional atmosphere-land tropical configuration at 4.5 km grid spacing (MOHC-HadREM3-RAL1T-4.5km).  

The **Hindcast simulation** (hindcast) is ran for 1998-2008. The boundary conditions are provided by the ERA-interim
dataset, dynamically downscaled to the CPRCM 4.5km resolution using two-step nesting. ERA-Interim
data is first downscaled to 25 km with MOHC-HadREM3-GA705-25km and then into 4.5km with HadREM3-RAL1T-4.5km. 

The **present-day control simulation** (pdControl) covers the same period and the boundary conditions are provided
by the HadGEM3 atmosphere-land model at 25km (MOHC-HadGEM3-GC31-N512). Sea surface temperatures (SSTs) and sea ice are
from the present-day daily 0.25 deg. dataset (Reynolds et al., 2007).

The **Future simulation** (future2100) simulates 10 years under 2100 RCP8.5 forcing driven by the MOHC-HadGEM3-GC31-N512
model. The future forcing includes GHG concentrations for the year 2100 from the RCP8.5 scenario (Moss et al., 2010)
and sea surface temperatures (SST) anomalies between the 1975-2005 and 2085-2115 from the MOHC-HadGEM2-ES CMIP5 RCP8.5
simulation, added to the present-days (Reynolds) SSTs.  

## Data conversion
We have used a Python-based tool for converting the UM output into CMOR standards. This tool has been developed by the 
Climate Data Dissemination System (CDDS) team at the Met Office (https://github.com/MetOffice/CDDS) and was extensively
used to convert the Met Office UM data for CMIP6. 

## Brazil CPRCM experiment: Simulations segments, calendar and spinup
Each of the three simulations was split into two segments of 5 years (+1 year spinup), which were run in parallel
to save computing time. The spinup yr for segment one is 2007 and the simulation period is 1998-2002. 
The spinup yr for segment two is 2002 and the simulation period is 2003-2008.

| Experiment | Calendar | UM model                 | suite ID (Segment I)  | suite ID: Segment II  | Driving model      | Driving suite  |
|------------|----------|--------------------------|-----------------------|-----------------------|--------------------|----------------|
| hindcast   | Gregorian| MOHC-HadREM3-RAL1T-4.5km | mi-ba751              | mi-bb055              | MOHC-HadREM3-GA705-25km | mi-ba898       |
| pcControl  | 360-day  | MOHC-HadREM3-RAL1T-4.5km | mi-ba488              | mi-bb069              | MOHC-HadGEM3-GC31-N512  | u-ab261        |
| future2100 | 360-day  | MOHC-HadREM3-RAL1T-4.5km | mi-ba489              | mi-bb070              | MOHC-HadGEM3-GC31-N512  | u-ab268        |


## Initialisation Details:
Hindcast Simulations:
   * MO rose suites mi-ba751 was initialised at 1998-01-01 from a dump file from its spinup suite (mi-ba451). This  
was initialised from the RCM (MOHC-HadREM3-GA705-25km) dump at 1997-01-01. The RCM was initialised at 1992-01-01 from
reconfiguration, which uses offline JULES run to create estimate of the soil moisture state. 
   * MO rose suites mi-bb055 was initialised at 2003-01-01 from a spinup dump of suite mi-ba451.

pcControl Simulations:
   * MO rose suite mi-ba488 was initialised at 1997-01-01 from a PD GCM dump (MOHC-HadGEM3-GC31-N512, MO rose suite
u-ab261). The first year of mi-ba488 is regarded as spinup and the simulation begins at 1998-01-01.
   * MO rose suite mi-bb069 was initialised at 2002-01-01 from a u-ab261 dump. The first year of mi-bb069 is
its spinup and the simulation begins at 2003-01-01.

Future2100 Simulations: 
   * MO rose suite mi-ba489 was initialised at 1998-01-01 from a Future GCM dump (MOHC-HadGEM3-GC31-N512, MO rose suite
u-ab268). The first year of mi-ba489 is regarded as spinup and the simulation begins at 1998-01-01.
   * MO rose suite mi-bb070 was initialised at 2002-01-01 from a u-ab268 dump. The first year of mi-bb070 is
its spinup and the simulation begins at 2003-01-01.

### File names convention, variant ID and metadata:
We have generated single-variable netCDF files consistent with CMOR 3.7, CF-1.7 CMIP-6.2 and CF standards. The filename
is given in the CMIP6 format, as following:

{variable}_{frequency}_{model_id}_{experiment_id}_{variant_id}_{grid_type}_{start_date}-{end_date}.nc

For example: 
**‘pr_day_HadREM3-RAL1T_hindcast_r1i1p1f1_gn_19980101-19981231.nc’**

Files from the future2100 also have dates from 1998-01-01 to 2008-01-01, even though their forcing are for 2100.
This is to reflect the dates of the base SSTs that are used. For this reason, time series plots will have 1998-2008
dates for both the pdControl and the future2100 simulations.

The CMIP6 netCDF file names contain information on variant-id, with the format e.g.: r1i1p1f1. The letters express the
following: r - realisation (i.e. ensemble member), I - initialisation method, p- physics,  f- forcing. We have decided
not to use the variant ID to distinguish between the different CSSP Brazil simulations (because of subtly different
meaning of r, i, p and f in the CMIP experiments) and therefore filenames from all simulations are defined as r1i1p1f1. 

The netCDF files metadata includes information about the timestep (60s or 1/1440 of a day), diagnostic name and units,
the experiment name and suite id and a link to this url.   

### Licensing and data use:
TBC