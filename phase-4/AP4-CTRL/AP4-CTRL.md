# AeroCom phase 4 control experiment (AP4-CTRL)

## Organizers
- Kostas Tsigaridis, ([kostas.tsigaridis@columbia.edu](mailto:kostas.tsigaridis@columbia.edu))
- Michael Schulz, ([michael.schulz@met.no](mailto:michael.schulz@met.no))
- Huisheng Bian ([huisheng.bian-1@nasa.gov](mailto:huisheng.bian-1@nasa.gov))

## Submission deadlines
- **Present-day free-running:** July 2025
- **Present-day nudged:** July 2025
- **Preindustrial free-running:** July 2025
- **Preindustrial nudged:** July 2025

## Motivation
The model versions used for the different experiments are often not easily comparable. New model versions should be documented regularly to establish a state of the art comparison yearly. For this purpose AeroCom offers a semi-automatic platform with visualization via the AeroCom web interface. Evaluation with surface observations and AERONET observations will complete the documentation of emissions, removal, burden, lifetime of the major aerosol species.

In 2025 additional motivation we try to revisit the AeroCom evaluation done over the years, focusing on not only whether and by how much models differ, but primarily on the why. Further, several AP4 experiments have been launched which should use this control experiment as their baseline, to the extent possible, including multi-model PPE analyses. Also  models prepare for CMIP7 and might be interested in quick feedback.

Additional analysis not listed here which can happen using this output is particularly welcome. 

## Objectives
- Document models and how they have changed since the last time.
- Benchmark individual model performance against measurements and identify problems.
- Evaluate models against each other, by quantitatively identifying model similarities and differences.
- Explain model differences.
- Help improve models.

## Proposed Model Experiments

### General Simulation Requirements
- **Simulation Period:** Preindustrial (1850; Full: 10-year mean; Lite: 5-year mean) and present-day (Full: 2000-2023; Lite: 2010-2023).
- **Spinup:** 2 years or more. Year 1850 for preindustrial, transient years before initial year for present-day (i.e. Full: 1988-1999; Lite: 2008-2009). 
- **Nudging:** Both. For preindustrial nudged runs use 2010. Models can use their nudging source and method. CTMs will be considered as nudged, and don't have to submit free-running simulations.
- **Emissions:** CEDS for CMIP7 for anthropogenic. Climatological for preindustrial, transient for present-day. GFED4s (daily) for present-day, per CMIP7 (monthly) for preindustrial. Natural emissions (Natural VOCs, DMS, dust, sea salt, etc.) calculated online, or whatever each model uses. 
- **SST and sea ice:** AMIP simulations, per CMIP7. Climatological mean for preindustrial, transient for present-day.
- **Configuration:** Include both gas-phase chemistry and aerosols. CH4 concentrations prescribed at surface. Do not use prescribed volcanoes in the stratosphere, rather inject SO2 from Carn et al. All other boundary conditions and forcings (e.g. GHGs, solar, land use and land cover, orbital) should match those of CMIP7 to the extent possible.
- **Passive tracers:** Strongly recommended to be included, but not required. These include CO50, Rn222, Pb210, e90, st8025, aoa, aoanh, nh50. 

### Lite simulations
Nudged and free-running (for GCMs only) simulations. Preindustrial: 5-year mean with at least 2 years of spinup. Present-day: 2010-2023 with at least 2 years of spinup. **Total simulation years:** 23 for CTMs, 46 for GCMs. 

### Full simulations
Nudged and free-running (for GCMs only) simulations. Preindustrial: 10-year mean with at least 2 years of spinup. Present-day: 2000-2023 with at least 2 years of spinup. **Total simulation years:** 38 for CTMs, 76 for GCMs. 

### Simulations

| Simulation   | Period        | Nudged | Years                               |
|--------------|---------------|--------|-------------------------------------|
| AP4-CTRL-PIf | Preindustrial | No     | 1850. Lite: 5 years; Full: 10 years |
| AP4-CTRL-PIn | Preindustrial | Yes    | 1850. Lite: 5 years; Full: 10 years |
| AP4-CTRL-PDf | Present day   | No     | Lite: 2010-2023; Full: 2000-2023    |
| AP4-CTRL-PDn | Present day   | Yes    | Lite: 2010-2023; Full: 2000-2023    |

## Model Output Variables

**TBD; not yet current**

Either a table or a link to somewhere else. 

**E.g.:** 

| **Variable**                         | **Variable Name** | **Variable Unit** | **Temporal Frequency** |
|--------------------------------------|-------------------|-------------------|------------------------|
| **Basics:**                          |                   |                   |                        |
| Surface altitude (relative to sea level) | orog              | m                 | Unchanging              |
| Area of each grid box                | areacella         | m²                | Unchanging              |
| Land area fraction                   | sftlf             | 1                 | Unchanging              |
| Variables to interpolate from model levels to pressure levels |                   |                   |                        |
| **Met. fields:**                     | **VerticalCoordinateType: Surface** |                   |                        |
| Surface air pressure                 | ps                | Pa                | Monthly-mean            |
| Sea surface temperature              | tos               | K                 | Monthly-mean            |
| Near-surface air temperature         | tas               | K                 | Monthly-mean            |

## Model Output Submission
Submit your model output via the AeroCom website: [Submit Data](https://aerocom.met.no/FAQ/data_access/submit_data).

### Model Output Naming Convention
The format for the AeroCom file name (one variable per file) should be:
`aerocom4_<ModelName>_<YOUR_EXPERIMENT_NAME>-<SimulationName>_<VariableName>_<VerticalCoordinateType>_<Year>_monthly.nc`

#### Example Filenames
- **2-D:** `aerocom4_GEOS-i33p2_AP4-CTRL-PDn_ps_Surface_2008_monthly.nc`
- **3-D:** `aerocom4_GEOS-i33p2_AP4-CTRL-PDn-oa_ModelLevel_2009_monthly.nc`

## References
List here control-like papers from past AeroCom phases. Also list papers for the emissions, the CMIP7 configuration (if/when available) and the passive tracers.
