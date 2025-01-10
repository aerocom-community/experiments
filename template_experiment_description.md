# Title of experiment, including its acronym

## Organizers
- Name Name ([email@email.com](mailto:email@email.com))
- Name Name ([email@email.com](mailto:email@email.com))

## Deadlines for Submission of Model Data
- **Tier 1 Experiments:** One date
- **Tier 2 Experiments:** Another date
  
(Tier 1, tier 2 or higher tiers are optional)

## Motivation
A very good reason for the experiment

## Objectives
- Objective 1
- Objective 2 

## Proposed Model Experiments

### General Simulation Requirements
- **Simulation Period:** 
- **Nudging:** Yes/no, details.
- **SST:** Details.
- **And so on...** 

## Tier 1 Simulations
Description of the Tier 1 simulations (does not need to be a table).

| Simulation Name | Emissions | .. | Purpose                                 |
|-----------------|-----------|----|-----------------------------------------|
| CTRL            | ..        | .. | Control simulation                      |
| Ex1             | ..        | .. | Reason 1                                |
| Ex2             | ..        | .. | Reason 2                                |

### Tier 2 Simulations
Description of the Tier 2 simulations (does not need to be a table).

| Simulation Name | Emissions | .. | Purpose                                 |
|-----------------|-----------|----|-----------------------------------------|
| Ex3             | ..        | .. | Reason 1                                |
| Ex4             | ..        | .. | Reason 2                                |

## Model Output Variables
Either a table or a link to somewhere else. 

**E.g.:** 

| **Variable**                         | **Variable Name** | **Variable Unit** | **Temporal Frequency** |
|--------------------------------------|-------------------|-------------------|------------------------|
| **Basics**                          |                   |                   |                        |
| Surface altitude (relative to sea level) | orog              | m                 | Unchanging              |
| Area of each grid box                | areacella         | m²                | Unchanging              |
| Land area fraction                   | sftlf             | 1                 | Unchanging              |
| Variables to interpolate from model levels to pressure levels |                   |                   |                        |
| **Met. fields**                     | **VerticalCoordinateType: Surface** |                   |                        |
| Surface air pressure                 | ps                | Pa                | Monthly-mean            |
| Sea surface temperature              | tos               | K                 | Monthly-mean            |
| Near-surface air temperature         | tas               | K                 | Monthly-mean            |

## Model Output Submission
Submit your model output via the AeroCom website: [Submit Data](https://aerocom.met.no/FAQ/data_access/submit_data).

### Model Output Naming Convention
The format for the AeroCom file name (one variable per file) should be:

`aerocom4_<ModelName>_<YOUR_EXPERIMENT_NAME>-<SimulationName>_<VariableName>_<VerticalCoordinateType>_<Year>_monthly.nc`

#### Example Filenames
- **2-D:** `aerocom4_GEOS-i33p2_<YOUR_EXPERIMENT_NAME>-histSST_ps_Surface_2008_monthly.nc`
- **3-D:** `aerocom4_GEOS-i33p2_<YOUR_EXPERIMENT_NAME>-histSST-oa_ModelLevel_2009_monthly.nc`

## References
