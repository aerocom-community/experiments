# AeroCom phase 4 control experiment (AP4-CTRL)

## Organizers
- Kostas Tsigaridis, ([kostas.tsigaridis@columbia.edu](mailto:kostas.tsigaridis@columbia.edu))
- Michael Schulz, ([michael.schulz@met.no](mailto:michael.schulz@met.no))
- Huisheng Bian ([huisheng.bian-1@nasa.gov](mailto:huisheng.bian-1@nasa.gov))

## Submission deadlines
- **Preindustrial AMIP:** TBD
- **Preindustrial transient nudged:** TBD
- **Preindustrial climatological nudged:** TBD
- **Present-day AMIP:** TBD
- **Present-day transient nudged:** TBD
- **Present-day climatological nudged:** TBD

A note on submission deadlines: AP4-CTRL should be performed with the models that participate in CMIP7, where applicable. This means that the submission deadline depends on 1) the availability of model input data from CMIP7, and 2) the model code freezing from the different modeling centers. However, early submissions are highly encouraged, with the caveat that you will need to repeat the runs when the CMIP7 version of the model is ready. 

Who should submit results early: 
- CTMs and GCMs not participating in CMIP7.
- GCMs that have their CMIP7 version of the code frozen.
- GCMs that are not ready for CMIP7, but are willing to repeat the early simulations.

The [ACI experiment](/phase-4/aci-baseline/aci-baseline.md) is welcoming early submissions of results, given that it only requests a small amount of simulation years. These include the climatological nudged simulations only; see below for details. 

## Motivation
The model versions used for the different experiments are often not easily comparable. New model versions should be documented regularly to establish a state of the art comparison yearly. For this purpose AeroCom offers a semi-automatic platform with visualization via the AeroCom web interface. Evaluation with surface observations and AERONET observations will complete the documentation of emissions, removal, burden, lifetime of the major aerosol species.

In 2025 additional motivation we try to revisit the AeroCom evaluation done over the years, focusing on not only whether and by how much models differ, but primarily on the why. Further, several AP4 experiments have been launched which should use this control experiment as their baseline, to the extent possible, including multi-model PPE analyses. Also  models prepare for CMIP7 and might be interested in quick feedback.

Three types of simulation pairs are planned, each of which has a preindustrial and a present day simulation:
- **AMIP:** For all GCMs; aiming to capture the full atmospheric transient model response to aerosol changes. 
- **Transient nudged:** For all models; focusing on aerosol forcing.
- **Climatological nudged:** Only for models participating in the [ACI experiment](/phase-4/aci-baseline/aci-baseline.md); trying to reduce the weather noise as much as possible.

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
- **Nudging:** For preindustrial climatological nudged runs use year 2010. For preindustrial transient  nudged runs use the same years used in the present day simulation. Models can use their nudging source and method. CTMs will be considered as nudged, and don't have to submit AMIP simulations.
- **Emissions:** CEDS for CMIP7 for anthropogenic. Year 1850 preindustrial, transient for present day. GFED4s (daily) for present day, per CMIP7 (monthly) for preindustrial. Natural emissions (natural VOCs, DMS, dust, sea salt, lightning, etc.) calculated online, or whatever each model uses. 
- **SST and sea ice:** Climatological decadal mean for all preindustrial experiments, as close to 1850 as possible for AMIP, a decade around 2010 (e.g. 2005-2015) for both of the nudged ones. Transient for present day AMIP and transient nudged, climatological decadal mean (the same as the preindustrial climatological nudged) for climatological present day nudged.
- **Configuration:** Include both gas-phase chemistry and aerosols. CH4 concentrations prescribed at surface. Do not use prescribed volcanoes in the stratosphere, rather inject SO2 from Carn (2022). All other boundary conditions and forcings (e.g. GHGs, solar, land use and land cover, orbital) should match those of CMIP7 to the extent possible.
- **Passive tracers:** Strongly recommended to be included, but not required. These include CO50, Rn222, Pb210, e90, st8025, aoa, aoanh, nh50. See e.g. Orbe et al. (2022) for details. Also see [here](https://wiki.met.no/_media/aerocom/a3_tracer_requirements_v2019-10-10c.pdf).

### Lite simulations
Nudged (climatological and transient) and AMIP (for GCMs only) simulations. Preindustrial: 5-year mean with at least 2 years of spinup. Present-day: 2010-2023 with at least 2 years of spinup. **Total simulation years:** 30 for CTMs, 53 for GCMs; 23 and and 46, respectively, if not participating in the ACI experiment. 

### Full simulations
Nudged (climatological and transient) and AMIP (for GCMs only) simulations. Preindustrial: 10-year mean with at least 2 years of spinup. Present-day: 2000-2023 with at least 2 years of spinup. **Total simulation years:** 45 for CTMs, 83 for GCMs; 38 and and 75, respectively, if not participating in the ACI experiment. 

### Simulations
In the table below, replace the year 2000 with 2010 if only running the lite simulations. For spinup, use the same years as described for individual years, or the years prior for transient ones (e.g. 2010 for a 2010 climatology, and 1998-1999 for a 2000-2023 simulation).

| Simulation          | Emissions | Nudging   | SST and sea ice     |
|---------------------|-----------|-----------|---------------------|
| AP4-CTRL-PI-AMIP    | 1850      | None      | ~1850 decadal mean  |
| AP4-CTRL-PI-NudTran | 1850      | 2010-2019 | 2010-2019 transient |
| AP4-CTRL-PI-NudClim | 1850      | 2010      | 2005-2015 mean      |
| AP4-CTRL-PD-AMIP    | 2000-2023 | None      | ~1850 decadal mean  |
| AP4-CTRL-PD-NudTran | 2000-2023 | 2000-2023 | 2000-2023 transient |
| AP4-CTRL-PD-NudClim | 2010      | 2010      | 2005-2015 mean      |

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
- **2-D:** `aerocom4_GEOS-i33p2_AP4-CTRL-PD-NudTran_ps_Surface_2010_monthly.nc`
- **3-D:** `aerocom4_GEOS-i33p2_AP4-CTRL-PD-NudTran-oa_ModelLevel_2010_monthly.nc`

## References
Carn, S. (2022), Multi-Satellite Volcanic Sulfur Dioxide L4 Long-Term Global Database V4, Greenbelt, MD, USA, Goddard Earth Science Data and Information Services Center (GES DISC), doi:[10.5067/MEASURES/SO2/DATA405](https://dx.doi.org/10.5067/MEASURES/SO2/DATA405).

Orbe, C., D. Rind, J. Jonas, L. Nazarenko, G. Faluvegi, L.T. Murray, D.T. Shindell, K. Tsigaridis, T. Zhou, M. Kelley, and G. Schmidt, 2020: GISS Model E2.2: A climate model optimized for the middle atmosphere. Part 2: Validation of large-scale transport and evaluation of climate response. J. Geophys. Res. Atmos., 125, no. 24, e2020JD033151, doi:[10.1029/2020JD033151](http://dx.doi.org/10.1029/2020JD033151).
