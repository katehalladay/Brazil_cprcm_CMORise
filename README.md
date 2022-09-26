# Brazil cprcm CMORise
Using mip_convert to process CSSP Brazil CPRCM output pp files to CMOR-compliant netCDF 

## Background
The Brazil CPRCM experiment includes three simulations: the **Hindcast simulation** for 1998-2008 is driven by 
ERA-interim dataset, dynamically downscaled to the CPRCM 4.5km resolution using two-step nesting.The **present-day
control simulation** (pdControl) covers the same period and is driven by the HadGEM3 atmosphere/land model at 25km
(HG3 N512). Sea surface temperatures (SSTs) and sea ice are from the present-day daily 0.25 deg. dataset 
(Reynolds et al., 2007). The **Future simulation** simulates 10 years under 2100 RCP8.5 forcing driven by a similar
future simulation of the HG3 N512. The future forcing includes GHG concentrations for the year 2100 taken from the 
RCP8.5 scenario (Moss et al., 2010) and sea surface temperatures (SST) anomalies between the 1975-2005 and 2085-2115
from the HadGEM2-ES CMIP5 RCP8.5 simulation, added to the present-days SSTs. 

## Brazil CPRCM experiment: Simulations segments, calendar and spinup
Each of the three simulations was split into two segments of 5 years (+1 year spinup), which were run in parallell
to save computing time. 

|   Experiment   | Calendar  |  Segment I  | Segment II | Driving model
|:--------------:|:---------:|:-----------:|:----------:|:---------: |
|    hindcast    | Gregorian |  mi-ba751   |  mi-bb055  | mi-ba898
|   pcControl    |  360-day  |  mi-ba488   |  mi-bb069  | u-ab261
| future |  360-day  | mi-ba489 |  mi-bb070  | u-ab268

The spinup yr for segment one is 2007 and simulation period is 1998-2002.
The spinup yr for segment tweo is 2002 and simulation period is 2003-2008.
## Lateral Boundary Conditions:
   * The lateral boundary conditions for the hindcast simulations (MO rose suites mi-ba751 and mi-bb055) are provided
by Era-Interim (1998-2007) data at 75km, dynamically downscaled to convection permitting scale (4.5 km grid spacing)
using two step nesting. The CPRCM simulation at 4.5km is nested in 25 km HadREM3-GC3.1-N512, which in turn is nested in
ERA-Interim. 
   * The lateral boundary conditions for the PD simulations (MO rose suites mi-ba488, mi-bb069) are provided by the
HadGEM3 atmosphere/land model at 25km resolution HadGEM3-GC3.1-N512, (MO rose suite: u-ab261), dynamically downscaled
to convection permitting scale (resolution ~ 4.5 km) using one-step nesting. 
   * The lateral boundary conditions for the future, 2100AD climate simulations (mi-ba489, mi-bb070) are provided by
the HadGEM3 atmosphere/land model at 25km resolution HadGEM3-GC3.1-N512, (MO rose suite: u-ab268), dynamically
downscaled to convection permitting scale (resolution ~ 4.5 km) using one-step nesting. 

## Initialisation Details:
Hindcast Simulations:
   * MO rose suites mi-ba751: initialised at 1998-01-01 from a spinup dump. Spinup (mi-ba451) initialised from RCM dump
at 1997-01-01. RCM initialised at 1992-1-1 from reconfiguration, which uses offline JULES run to create estimate of
soil moisture state. 
   * MO rose suites mi-bb055: initialised at 2003-01-01 from a spinup dump. Spinup (mi-ba451) initialised from RCM dump
at 1997-01-01. RCM initialised at 1992-1-1 from reconfiguration, which uses offline JULES run to create estimate of
soil moisture state. 

pcControl Simulations:
   * MO rose suite mi-ba488: initialised at 1998-01-01 from a spinup dump. Spinup initialised from PD GCM dump
(MO rose suite u-ab261) at 1997-01-01. 
   * MO rose suite mi-bb069: initialised at 2003-01-01 from a spinup dump. Spinup initialised from PD GCM dump
(MO rose suite u-ab261) at 2002-01-01. 

Future Simulations: 
   * MO rose suite mi-ba489:  initialised at 1998-01-01 from a spinup dump. Spinup initialised from future GCM dump
(MO rose suite u-ab268) at 1997-01-01.
   * MO rose suite mi-bb070:  initialised at 2003-01-01 from a spinup dump. Spinup initialised from future GCM dump
(MO rose suite u-ab268) at 2002-01-01.

## VARIANT-ID IN CSSP BRAZIL CPRCM METADATA
CSSP Brazil follows a similar variant-id to CMIP6 netCDF files, with the format r1i1p1f1, where the letters and numbers
express the following:

r: realisation (i.e. ensemble member)

i: initialisation method

p: physics

f: forcing

### Realisation:
1: First ensemble member 

2: Not used

### Initialisation:
1: Initial conditions and boundary conditions taken from a prior simulation: HadGEM3-GC3.1-N512. 

2: Initial conditions and boundary conditions taken from a prior simulation: HadREM3-GC3.1-N512. 

i1 is used by pdControl and Future CPRCM simulations. The lateral boundary condition source is the HadGEM3-GC3.1-N512 
GCM, dynamically downscaled to convection permitting scale (resolution ~ 4.5 km) using one-step nesting. 
i2 is used by the Hindcast CPRCM simulation. The lateral boundary condition source is the ERA Interim dataset,
dynamically downscaled to convection permitting scale (~ 4.5 km grid spacing) using two step nesting. The CPRCM
simulation at 4.5km is nested in 25 km HadREM3-GC3.1-N512, which in turn is nested in ERA-Interim. 

### Physics:
1: tbc 

### Forcing:
1: tbc pdControl /hindcast forcing
2: tbc future forcing

## A note about file names and dates
We have generated single-variable netCDF files consistent with CMOR 3.7, CF-1.7 CMIP-6.2 and CF standards.
The filename is given in the CMIP6 format, as following:

{variable}_{frequency}_{model_id}_{experiment_id}_{variant_id}_{grid_type}_{start_date}-{end_date}.nc

For example: "pr_day_HadREM3-RAL1T_hindcast_r1i1p1f1_gn_19980101-19981231.nc"

Files from all three experiments have dates from 1998-01-01 to 2008-01-01. 
For this reason, the time series plots in
this paper are using the 1998-2008 period for both the PD and the AD 2100 simulations.
