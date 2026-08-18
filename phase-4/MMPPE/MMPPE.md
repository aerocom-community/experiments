# Multi-Model PPE Experiment

## Organizers
- Hailing Jia ([h.jia@sron.nl](mailto:h.jia@sron.nl))

## Deadlines for Submission of Model Data
- **[One-At-a-Time Test](#one-at-a-time-test):** 31 July 2026
- **[PPE Experiments](#ppe-simulations):** 30 September 2026


## Motivation
To understand and constrain the uncertainty in aerosol radiative forcing (ACI+ARI) in different model systems, a Multi-Model Perturbed Parameter Ensemble (MMPPE) involving different aerosol- and cloud-related parameters is needed. With this, we will be able to jointly tackle two dominant sources of model uncertainty: structural uncertainty and parametric uncertainty. The AeroCom MMPPE experiment is also linked to the CMIP7 Aerosol-Cloud Interactions Perturbed Parameter Ensemble Model Intercomparison Project ([ACI-PPEMIP](https://wcrp-cmip.org/mips/)).


## Objectives
- Quantify parametric uncertainty across different models and assess the relative contributions of parametric versus structural uncertainties.
- Constrain parametric uncertainty using new observations from 2025, (e.g., EarthCARE and PACE).
- Identify structural deficiencies in models and guide improvements to parameterizations.


## Proposed Model Experiments

### General Simulation Requirements
- **Simulation Period:** 1850 for Preindustrial (PI) and 2025 for present-day (PD).
- **Spin-up:** 3-month CTL run (spin-up; starting 1 July 2024 )  + 3-month CTL+PPE runs (spin-up; starting 1 Oct 2024) + 1-year CTL+PPE production runs (2025). CTL denotes the control simulation using the model's default parameter settings.

- **Nudging:** Both PI and PD winds (not temperature or relative humidity) are nudged towards reanalysis data. Nudging to ERA5 with a relaxation timescale of ~6 hours above the boundary layer (~2 km) is recommended. Other reanalyses or nudging configurations (e.g.,throughout the atmospheric column or difference relaxation time) are also acceptable.

- **CFMIP COSP:** Optional, but highly desirable for models with COSP

- **Ensemble size:** The number of simulations should be at least 6 times the number of [perturbed parameters](#perturbed-parameters), with a target ratio of 8 where possible. For example, a PPE with 29 (mandatory + recommended) parameters, plus 1 CTL run, requires a minimum of (29 × 6 + 1) × 2 = 350 simulations (PI+PD).

- **Input/Forcing datasets** (kept as consistent as possible with CMIP7):

    - **Anthropogenic emission:** CEDS v2025-04-18 (available for 1850-2023; 2022-2023 repeated for 2024-2025)
    - **Biomass burning emission:** GFED5.1 (daily) for PD; CMIP7 biomass burning (monthly) for PI
    - **GHGs and ozone:** CMIP7 ScenarioMIP `m` for GHGs, `vl` for ozone (only `vl` and `h` are currently available)
    - **SST/SIC:** Prescribed from ERA5 monthly data for the year 2025 for both PI and PD runs


    >**Note**: All above inputs are available at https://public.spider.surfsara.nl/project/polder/hjia/MMPPE_input. Most datasets are provided at fine spatial resolution (e.g., 0.25° × 0.25°) to be regridded to match your model resolution.

### PPE Experiments

| Experiment | Emissions | Nudging | SST & SIC | Other forcing |
|------------|-----------|---------|---------|---------------|
| PI         | 1850      | 2025    | 2025     |2025| 
| PD         | 2025      | 2025    | 2025     |2025     |      

### One-At-a-Time Test

To ensure that all parameters are wired properly, **a five-day One-At-a-Time (OAT) test for PD (1–5 Aug 2025) is strongly recommended before the PPE runs.** In each OAT simulation, one parameter is set to its lower or upper bound while all others remain at their default values.

**Spin-up**: first perform a 3-month spin-up of the default CTL run, then initialize all OAT runs from the same CTL state at 1 Aug 2025.

**Variables to test:**
| Variable               | Dedcription                                      |
|------------------------|--------------------------------------------------|
| od550aer               | Aerosol Optical thickness @550nm                 |  
| abs550aer              | Absorption optical thickness @550nm              |  
| angstrm550_865         | Angstroem parameter 550nm-865nm                  | 
| ssa550                 | Single scattering albedo @550nm                  |
| ccns.3                 | Surface CCN number concentration at S=0.3%       |
| ccncol.3               | Column-integrated number concentration at S=0.3% |  
| cdnc_incl_ct           | Cloud-top in-cloud cloud droplet number conc.    |
| clt                    | Total cloud cover                                |
| cllvi                  | Vertically integrated cloud water                |       
| clivi                  | Vertically integrated cloud ice                  |   
| pr                     | Surface recipitation flux                        |
| scre                   | Shortwave cloud radiative effect at TOA          |
| lcre                   | Longwave cloud radiative effect at TOA           |
| fnet                   | Net radiation flux at TOA                        |

Submit the following:

- a CSV file following the format of [ICON-HAM_5d_OAT.csv](ICON-HAM_5d_OAT.csv), containing 5-day global-mean values for the base, `parameter_L`, and `parameter_H` experiments
- plots of the relative (%) change with respect to the base run (see example for ICON-HAM `od550aer` below). You may use [plot_OAT.py](./plot_OAT.py) to generate plots in the example style.

![OAT_AOD](./ICON-HAM_5d_OAT_od550aer.png)

See **[Model Output submission](#model-output-submission)** for submission instructions.


### Perturbed Parameters
We focus on multiple aerosol- and cloud-related processes. For aerosols, they are aerosol emissions, optical and hygroscopic properties, wet and dry depositions, nucleation,  aging and chemistry, with a special focus on emissions from biomass burning and natural sources. For clouds, the targeted processes/schemes include activation, cloud microphysics, cloud cover, convection, optical processes, and turbulence. See [Jia et al. (2026)](https://doi.org/10.5194/egusphere-2026-3275) for more detials.

**Latin hypercube sampling** strategy is used to generate parameter values for each ensemble member. An example Python script can be found at: https://github.com/hljia/LHS_example

Parameters labeled "Rel" are scaling factors relative to the control values, whereas those labeled "Abs" are absolute values. 

>**Note**: If the default parameter value in your model differs substantially from the protocol value (e.g., lies close to or outside the prescribed range), please scale the parameter range proportionally to preserve the same min/default and max/default ratios.

#### Mandatory (21)
These parameters are not model-dependent, so all models should be able to perturb them. 

| Variable   | Default | Range  | Description | Process | Remark | 
|------------|---------|--------|-------------|---------|--------|
| emi_ant_so2<br>(Rel)| 1       |[0.6, 2]| Scale factor for anthropogenic so2 emissions | Emission | |
| emi_ant_bc<br>(Rel)| 1 |[0.6, 2] | Scale factor for anthropogenic bc emission | Emission | |
| emi_ant_oc<br>(Rel)| 1 | [0.6, 2] | Scale factor for anthropogenic oc emission | Emission | |
| emi_bb_so2<br>(Rel)| 1 |[0.25, 4] | Scale factor for biomass burning so2 emission | Emission | |
| emi_bb_bc<br>(Rel)| 1 | [0.25, 4] | Scale factor for biomass burning bc emission | Emission |
| emi_bb_oc<br>(Rel)| 1 | [0.25, 4] | Scale factor for biomass burning oc emission | Emission | | 
| emi_dms<br>(Rel)| 1 | [0.2, 3] | Scale factor for DMS emission | Emission | |
| emi_ss_acc<br>(Rel)| 1 | [0.1, 3] | Scale factor for accumulation mode sea salt emission | Emission | | 
| emi_ss_coa<br>(Rel)| 1 | [0.1, 3] | Scale factor for coarse mode sea salt emission | Emission | |
| emi_du<br>(Rel)| 1 | [0.5, 2] | Scale factor for dust emission | Emission | |
| emi_cmr_ff<br>(Abs)| 30nm | [15, 45] | Emitted particle size for fossil fuel emissions (unit: nm) | Emission | not in NorESM |
| emi_cmr_bb<br>(Abs)| 75nm | [25, 250] | Emitted particle size for biomass burning emissions | Emission | not in NorESM |
| rad_bc_ni<br>(Abs)| 0.71 | [0.2, 0.9] | BC imaginary refractive index at 550nm|Aerosol Optics | if BC imaginary refractive index is wavelength-dependent in your model, scale all SW wavelengths by the same factor (`scale_bc_rad_ni`) derived from 550nm, to preserve the original spectral dependence (see [wavelength-dependent perturbation](#example-for-wavelength-dependent-perturbation) for example code)|
| rad_oc_ni<br>(Abs)|0.0055 | [0.0001,0.05] | OC imaginary refractive index at 550nm| Aerosol Optics | same as `rad_bc_ni`|
| wetdep_ic<br>(Rel)| 1 | [0.75, 1.25] | Scale factor for in-cloud wet deposition rate | Deposition | |
| activ_aero<br>(Rel)| 1 | [0.75, 1.25] | Scale factor for activated aerosols | Activation | reflects the uncertainty of activation scheme; [0.75, 1.25] from [Ghosh et al. (2025)](https://doi.org/10.5194/gmd-18-4899-2025) |
| activ_cwturb<br>(Rel)| 1 | [0.3,3] | Scale factor for vertical velocity for activation | Activation | Very uncertain according to [Virtanen et al. (2025)](https://www.nature.com/articles/s41561-025-01662-y)|
| micro_ccraut<br>(Rel)| 2.8 | [0.9,15] | Scale factor for autoconversion rate from cloud droplets to rain in stratiform clouds | Microphysics | | 
| micro_ccsaut<br>(Rel)| 1200 | [100, 2000] | Scale factor for autoconversion rate from cloud ice to snow | Microphysics | |
| conv_cprcon<br>(Abs)| 1e-4 s-1| [5e-5,8e-4] | Conversion rate from cloud water to rain in convective clouds | Convection | |
| conv_entrpen<br>(Abs)| 3e-4 m-1| [2e-5,4e-4] | Entrainment rate for deep convection | Convection | |

##### Example for wavelength-dependent perturbation
```fortran
!Compute the scaling factor using the 550 nm value (index: Nwv_sw+1)
scale_bc_rad_ni = rad_bc_ni / cni(Nwv_sw+1,iradbc)
!Apply the same scaling factor to all SW wavelengths
cni(1:Nwv_sw_tot,iradbc) = cni(1:Nwv_sw_tot,iradbc) * scale_bc_rad_ni
```
#### Recommended (8)
These parameters are either less critical than mandatory parameters or important but absent in some models.

| Variable   | Default | Range  | Description | Process | Remark | 
|------------|---------|--------|-------------|---------|--------|
| micro_ccraut_cdnc_expo<br>(Abs) | -1.79 | [-0.8,-2] | CDNC exponent in autoconversion scheme | Microphysics | **highly recommanded** if Khairoutdinov and Kogan (2010) scheme is used| 
| micro_ccraut_lwp_expo<br>(Abs) | 2.47 | [2.1,3.3] | LWP exponent in autoconversion scheme| Microphysics | **highly recommanded** if Khairoutdinov and Kogan (2010) scheme is used| 
| drydep_acc<br>(Rel)| 1 | [0.1,10] | Scale factor for dry deposition rate of accumulation-mode aerosols | Deposition | | 
| chem_so2<br>(Rel) | 1 | [0.5, 2] | Scale factor for so2 chemistry reaction rates | Chemistry | so2 –> so4 |
| kappa_so4 <br>(Abs)| 0.6 | [0.3,0.8] | Hygroscopic parameter for sulfate aerosols | Hygroscopicity | |
| coating_so4<br>(Abs)| 1 | [0.3,5] | Layer thickness of sulfate to transfer an insoluble particle to a soluble mode | Aging | It is  given in units of layers of monomolecular sulfate, NOT ‘nm’ |
| emi_ss_expo<br>(Rel)| 1 | [0.9,1.1] | Scale factor for wind exponent in the parameterization  of sea salt emission | Emission | |
| conv_cmfctop<br>(Abs)| 0.1 | [0.01,0.35] | fractional convective mass flux across the top of cloud | Convection | |


#### Optional (14)

| Variable   | Default | Range  | Description | Process | Remark | 
|------------|---------|--------|-------------|---------|--------|
| rad_du_ni<br>(Abs)| 1e-3 | [2e-4,1e-2] | Dust imaginary refractive index at 550nm| Aerosol Optics | same as `rad_bc_ni` |
| wetdep_bc<br>(Rel)| 1 | [0.3,3] | Scale factor for below-cloud wet deposition rate | Deposition | |
| kappa_oc<br>(Abs)| 0.06 | [0.02,0.4] | Hygroscopic parameter for oc aerosols | Hygroscopicity | |
| nucl_bl_ft<br>(Rel)| 1 | [0.01,10] | Scale factor for nucleation rate in BL and FT | Nucleation | |
| chem_dms<br>(Rel)| 1 | [0.5,2] | Scale factor for dms chemistry reaction rates | Chemistry | dms –> so2 |
| micro_icefall<br>(Rel)| 1| [0.4,2] | Scale factor for terminal fall velocity of cloud ice crystals| Microphysics | |
| cld_cov_crs<br>(Abs)| 0.968 | [0.9,0.98] | critical relative humidity at surface | Cloud cover | |
| cld_cov_crt<br>(Abs)| 0.8 | [0.7,0.85] | critical relative humidity aloft | Cloud cover | |
| conv_entrscv<br>(Abs)| 3e-3 m-1| [2e-4,4e-3] | entrainment rate for shallow convection | Convection | |
| conv_entrmid<br>(Abs)| 2e-4 m-1| [2e-5,4e-4] | entrainment rate for mid-level convection | Convection | |
| cld_opt_cinhomi<br>(Abs) | 0.7 | [0.6,1] | Inhomogeneity factor for ice clouds | Cloud Optocs | |
| cld_opt_cinhoml1<br>(Abs)| 0.8 | [0.6,1] | Inhomogeneity factor for stratiform clouds | Cloud Optics | |
| cld_opt_cinhoml3<br>(Abs) | 0.8 | [0.6,1] | Inhomogeneity factor for deep/mid-level convection | Cloud Optics | |
| turb_prandtl<br>(Abs) | 1 | [0.6,1] | Neutral limit Prandtl number | Turbulence | |

## Model Output Variables
> Note: "+" denotes variables to be added to the AeroCom AP4 CTRL variable spreadsheet..
 
`6H`: 6-hourly **instantaneous** output

`M`: monthly **mean** output

**PD PPE**: all listed `M` and `6H` outputs are required. 

**PI PPE**:  all listed `M` outputs are required;  `6H` output is required only for the follwing variables:

- `od550aer`, `angstrm550_865`, `od550aer_fine`, 
- `ccn01vi`, `ccn03vi`, `ccn01sf`, `ccn03sf`, `ccn01bl`, `ccn03bl`, `loadso4`, `so4sf`, `so4bl`
- `clt`, `lcc`, `icc`, `cdnctop`, `reffclwtop`, `reffclitop`, `ttop`, `n_liq_layer`, `lwp`, `clivi`, `clivi`, `wb`, `lts`, `pr`
- `rsdt`, `rsut`, `rsutcs`, `rlut`, `rlutcs`, `rsutaf`, `rsutcsaf`, `rlutaf`, `rlutcsaf`
- optional: `cltmodis`, `lccmodis`, `iccmodis`, `codmodis`, `codclwmodis`, `codclimodis`, `reffclwmodis`, `reffclimodis`, `lwpmodis`, `clivimodis`


### 3D outputs (lev, lat, lon)
- **output levels**: all model levels for monthly outputs; 8 height levels for 6-hourly `ec355aer` (see *Remarks*).


| **AeroCom name**         | **Description**                     | **Units** | **Freq**             |**Remark**             |
|---------------------------|---------------------------------------|----------|------------------------|------------------------|
| ec355aer +     | aerosol extinction coefficient @355nm     | m-1 | 6H,M |6H: 8 height levels [20, 200, 500, 1000, 2000, 3500, 6000, 10000] m above ground level (a.g.l.)| 
| zfull  +       | geometric height at model full levels above sea level (a.s.l.) | m | M | |
| zhalf  +       | geometric height at model interfaces (half levels) a.s.l.  | m | M |  |
| ccn01 +        | ccn number concentration at SS=0.1% | m-3 | M| |
| ccn03          | ccn number concentration at SS=0.3%  | m-3 | M| |
| ccn05 +        | ccn number concentration at SS=0.5%  | m-3 | M| |
| mmrdms +       | mass mixing ratio of dms | kg kg-1 | M | |
| mmrso2 +       | mass mixing ratio of so2| kg kg-1 | M | |
| mmrso4         | mass mixing ratio of sulfate| kg kg-1 | M | |
| mmrbc          | mass mixing ratio black carbon | kg kg-1 | M | |
| mmroa          | mass mixing ratio of organic matter | kg kg-1 | M | |
| mmrdust        | mass mixing ratio of dust | kg kg-1 | M | |
| mmrss          | mass mixing ratio of seasalt | kg kg-1 | M | |
| mmraerh2o      | mass mixing ratio of aerosol water | kg kg-1 | M | |
| nmrcdnc +      | cloud droplet number mixing ratio | kg-1 | M | grid cell mean, not in-cloud |
| nmricnc  +     | ice crystal number mixing ratio | kg-1 | M | grid cell mean, not in-cloud|
| hur            | relative humidity | % | M | | 
| hus            | specific humidity | kg kg-1 | M | |
| cl             | cloud area fraction | 1 | M | |
| cli            | specific cloud ice content | kg kg-1 | M | |
| clw            | specific cloud water content | kg kg-1 | M | |
| wa             | upward air velocity | m s-1 | M |   |
| ta             | air temperature | K | M | |
| rho            | atmospheric air density | kg m-3 | M | |
| pfull          | air pressure | Pa | M | |

### 2D outputs (lat, lon)
| **AeroCom name**         | **Description**                     | **Units** | **Freq**             |**Remark**             |
|---------------------------|---------------------------------------|----------|------------------------|------------------------|
| od550aer          | aerosol optical depth @550nm      | 1 | 6H,M |                        |
| abs550aer         | absorption aerosol optical depth @550nm   | 1 | 6H,M |                        |
| ssa440aer +       | single scattering albedo @440nm       | 1 | 6H,M |                        |
| angstrm440_670 +  | angstrom exponent 440nm-670nm       | 1 | 6H,M |                        |
| angstrm550_865 +  | angstrom exponent 550nm-865nm       | 1 | 6H,M |                        |
| od550aer_fine +   | fine-mode aerosol optical thickness @550nm    | 1 | 6H,M | nucleation + Aitken + accumulation modes         |
| od550aer_cs +     | coarse soluble aerosol optical thickness @550nm    | 1 | 6H,M |                  |
| od550aer_ci +     | coarse insoluble aerosol optical thickness @550nm    | 1 | 6H,M |                  |
| conccn30_50sf +     | aerosol number concentration (30<D<50nm) at the lowest model level    | m-2 | 6H,M |Aitken mode (aerosol growth / NPF) |  
| conccn50_100sf +    | aerosol number concentration (50<D<100nm) at the lowest model level   | m-2 | 6H,M |Aitken mode (CCN in pristine environments) |  
| conccn100_500sf +   | aerosol number concentration (100<D<500nm) at the lowest model level  | m-2 | 6H,M |Accumulation mode (dominant CCN size range) |  
| conccn250_500sf +   | aerosol number concentration (250<D<500nm) at the lowest model level  | m-2 | 6H,M |Upper accumulation range (CCN in polluted environments) | 
| conccn500_800sf +   | aerosol number concentration (500<D<800nm) at the lowest model level  | m-2 | 6H,M | | 
| conccn150vi +     | vertically integrated aerosol number concentration (D>150nm)     | m-2      | 6H,M |  | 
| loadbc            | atmospheric burden of black carbon | kg m-2   | 6H,M |                        |
| loaddu            | atmospheric burden of dust | kg m-2   | 6H,M |                        |
| loadoa +          | atmospheric burden of organic matter | kg m-2   | 6H,M |                        |
| loadso4           | atmospheric burden of sulfate | kg m-2   | 6H,M |                        |
| loadss            | atmospheric burden of seasalt | kg m-2   | 6H,M |                        |
| loadaerh2o +      | atmospheric burden of aerosol water| kg m-2   | 6H,M |                        |
| ccn01vi +         | vertically integrated CCN number concentration at S=0.1% | m-2   | 6H,M |                        |
| ccn03vi +         | vertically integrated CCN number concentration at S=0.3% | m-2   | 6H,M |                        |
| ccn01sf +         | CCN number concentration at SS=0.1% st the lowerst model level| m-3 | 6H,M| |
| ccn03sf +         | CCN number concentration at SS=0.3% st the lowerst model level| m-3 | 6H,M| |
| ccn05sf +         | CCN number concentration at SS=0.5% st the lowerst model level| m-3 | 6H,M| |
| ccn01bl +         | CCN number concentration at S=0.1% at 1 km above the surface | m-3 | 6H,M |                        |
| ccn03bl +         | CCN number concentration at S=0.3% at 1 km above the surface | m-3 | 6H,M |                        |
| so4sf   +         | mass concentration of sulfate at surface | kg m-3  | 6H,M |                        |
| so4bl   +         | mass concentration of sulfate at 1 km above surface | kg m-3  | 6H,M |                        |
| bcsf    +         | mass concentration of black carbon at surface | kg m-3  | 6H,M |                        |
| pm1sf   +         | mass concentration of pm1 at surface | kg m-3  | 6H,M |                        |
| pm2p5sf +         | mass concentration of pm2.5 at surface | kg m-3  | 6H,M |                        |
| pm10sf  +         | mass concentration of pm10 at surface | kg m-3  | 6H,M |                        |
| **< cloud-top diag seen from TOA** |||| for the Fortran code for the seven cloud-top diagnostics below, see the *"Cloud-top calculation"* in the [aci-baseline](../aci-baseline/aci-baseline.md) experiment |
| clt               | total cloud cover                | 1 | 6H,M |                        |
| lcc     +         | liquid cloud cover               | 1 | 6H,M |                        |
| icc     +         | ice cloud cover                  | 1 | 6H,M |                        |
| cdnctop +         | cloud droplet number concentration at cloud top | m-3 | 6H,M | grid cell mean, not in-cloud   |
| reffclwtop        | effective radius of cloud droplet at cloud top  | m       | 6H,M | grid cell mean, not in-cloud   |
| reffclitop        | effective radius of ice crystal at cloud top    | m       | 6H,M | grid cell mean, not in-cloud   |
| ttop              | air temperature at cloud top | K | 6H,M | grid cell mean, weighted by cloud cover |
| **cloud-top diag seen from TOA >**
| n_liq_layer       | number of liquid cloud layers    | 1 | 6H,M |                        |
| icncvi +?         | vertically integrated ice crystal number concentration | m-2   | 6H,M | grid cell mean, not in-cloud |
| cdncvi +?         | vertically integrated cloud droplet number concentration | m-2   | 6H,M | grid cell mean, not in-cloud |
| lwp               | vertically integrated cloud water  | kg m-2 | 6H,M | grid cell mean, not in-cloud  |
| clivi             | vertically integrated cloud ice    | kg m-2 | 6H,M | grid cell mean, not in-cloud  |
| cod               | cloud optical depth      | 1 | 6H,M | grid cell mean, not in-cloud |
| codclw  +         | cloud optical depth due to liquid     | 1 | 6H,M | grid cell mean, not in-cloud |
| codcli  +         | cloud optical depth due to ice              | 1 | 6H,M | grid cell mean, not in-cloud |
| cbh +        | liquid cloud base height (a.g.l. ) | m | 6H | only 6H|
| wb +         | updraft velocity at cloud base for activation | m s-1 | 6H,M | |
| bldep        | atmosphere_boundary_layer_thickness | m | 6H,M | |
| lts +        | lower tropospheric stability | K | 6H,M | potential temperature difference (theta at 700hPa – theta at 1000hPa)|
| pr           | precipitation flux                 | kg m-2 s-1 | 6H,M |                        |
| rsdt         | toa incoming shortwave flux | W m-2 | 6H,M | |
| rsut         | toa outgoing shortwave flux | W m-2 | 6H,M | |
| rsutcs       | toa outgoing shortwave flux (clear-sky) | W m-2 | 6H,M | |
| rlut         | toa outgoing longwave flux | W m-2 | 6H,M | |
| rlutcs       | toa outgoing longwave flux (clear-sky) | W m-2 | 6H,M | |
| rsutaf       | toa outgoing shortwave flux (aerosol-free)  | W m-2 | 6H,M | |
| rsutcsaf     | toa outgoing shortwave flux (clear-sky and aerosol-free)  | W m-2 | 6H,M | |
| rlutaf       | toa outgoing longwave flux (aerosol-free)  | W m-2 | 6H,M | |
| rlutcsaf     | toa outgoing longwave flux (clear-sky and aerosol-free)  | W m-2 | 6H,M | |
| sftlf        | land area fraction | % | M | |
| albsrfc  +   | surface albedo | 1 | M | |
| ua10m        | eastward_wind at 10m | m s-1 | M | |
| va10m        | northward_wind at 10m | m s-1 | M | |
| hfls         | surface_upward_latent_heat_flux | W m-2 | M | |
| hfss         | surface_upward_sensible_heat_flux | W m-2 | M | |
| prw          | atmosphere_mass_content_of_water_vapor | kg m-2 | M | |
| prcr   +     | convective liquid precipitation flux (rain) | kg m-2 s-1 | M |  | 
| prcs   +     | convective solid precipitation flux (snow) | kg m-2 s-1 | M |  | 
| prlr   +     | stratiform liquid precipitation flux (rain) | kg m-2 s-1 | M |  large scale precipitation | 
| prls   +     | stratiform solid precipitation flux (snow) | kg m-2 s-1 | M |  large scale precipitation | 
| loaddms      | atmosphere_mass_content_of_ambient_dimethyl_sulfide | kg m-2 | M |  |
| loadso2      | atmosphere_mass_content_of_ambient_sulfur_dioxide | kg m-2 | M |  |
| emidms       | emission mass flux of of DMS | kg m-2 s-1 | M |  |
| emiso2       | emission mass flux of sulfur dioxide | kg m-2 s-1 | M |  |
| emiso4       | emission mass flux of sulfate | kg m-2 s-1 | M  | |
| emibc        | emission mass flux of blac carbon | kg m-2 s-1 | M |  |
| emioa        | emission mass flux of organic matter | kg m-2 s-1 | M |  |
| emidust      | emission mass flux of dust | kg m-2 s-1 | M |  |
| emiss        | emission mass flux of seasalt | kg m-2 s-1 | M |  |
| abs550bc     | absorption aerosol optical depth due to black carbon | 1 | M |  |
| abs550oa     | absorption aerosol optical depth due to organic matter | 1 | M |  |
| abs550dust   | absorption aerosol optical depth due to dust | 1 | M |  |
| od550bc      | aerosol optical depth due to black carbon | 1 | M |  |
| od550oa      | aerosol optical depth due to organic matter | 1 | M |  |
| od550so4     | aerosol optical depth due to sulfate | 1 | M |  |
| od550dust    | aerosol optical depth due to dust | 1 | M |  |
| od550ss      | aerosol optical depth due to seasalt | 1 | M |  |
| od550aerh2o  | aerosol optical depth due to aerosol water  | 1 | M |  |

### Optional 2D outputs

| **AeroCom name**         | **Description**                     | **Units** | **Freq**             |**Remark**             |
|---------------------------|---------------------------------------|----------|------------------------|------------------------|
| cltmodis | modis_cloud_area_fraction | 1 | 6H | **highly recommanded** |
| lccmodis | modis_liquid_topped_cloud_area_fraction | 1 | 6H | **highly recommanded** |
| iccmodis | modis_ice_topped_cloud_area_fraction | 1 | 6H | **highly recommanded** |
| codmodis     | modis optical thickness total | 1 | 6H | **highly recommanded** |
| codclwmodis  | modis optical thickness water | 1 | 6H | **highly recommanded** |
| codclimodis  | modis optical thickness ice | 1 | 6H | **highly recommanded** |
| reffclwmodis | modis_Cloud_Particle_Size_Water | m | 6H | **highly recommanded** |
| reffclimodis | modis_Cloud_Particle_Size_Ice | m | 6H | **highly recommanded** |
| lwpmodis     | modis liquid water path | kg m-2 | 6H | **highly recommanded** |
| clivimodis   | modis ice water path | kg m-2 | 6H | **highly recommanded** |
| od550aer_ks + | aerosol optical depth (soluble Aitken mode) | 1 | M |  |
| od550aer_as + | aerosol optical depth (soluble accumulation mode) | 1 | M |  |
| od550aer_cs + | aerosol optical depth (soluble coarse mode) | 1 | M |  |
| od550aer_ki + | aerosol optical depth (insoluble Aitken mode) | 1 | M |  |
| od550aer_ai + | aerosol optical depth (insoluble accumulation mode) | 1 | M |  |
| od550aer_ci + | aerosol optical depth (insoluble coarse mode) | 1 | M |  |


### Output size estimate

For a 1-year simulation:

- M/2D: ~2 MB per variable
- M/3D: ~2 × 47 (levels) = 94 MB per variable
- 6H/2D: ~2 × 4 × 30 = 240 MB per variable
- 6H/3D: ~2 × 4 × 30 × 8 (levels) = 1.9 GB per variable

PPEs with 350 ensemble members in total (PD + PI) would generate (optional variables in parentheses):

- M/2D: ~350 × 100(+6) × 2 MB = 70(+4) GB
- M/3D: ~350 × 25 × 94 MB = 823 GB
- 6H/2D: ~[175 × 62(+10) + 175 x 35(+10)]× 240 MB = 4.1(+0.8) TB
- 6H/3D: ~175 × 1 × 1.9 GB = 0.33 TB (ec355aer only for PD)

**Total: ~5.3 TB for mandatory variables + ~0.8 TB for optional variables.**

## Model Output Submission

For **One-At-a-Time Test**, please
- Upload your csv file and OAT plots to the google drive folder [ACI-PPEMIP_OAT/](https://drive.google.com/drive/folders/1V1c-4pqVWfcsTqqsZ4UamWCuBw-jrNvz?usp=drive_link) (please create a subfolder for your model)
-  Enter your parameter ranges in the spreadsheet [ACI-PPEMIP parameter ranges](https://docs.google.com/spreadsheets/d/1tHGisfeP_58EO69tO5mt5H-nEfxcTZLcGYEDKeKs-v0/edit?gid=0#gid=0).
- You will see examples for ICON-HAM PPE there

For **PPE experiments**, submit the following data via the AeroCom website ([Submit Data](https://aerocom.met.no/FAQ/data_access/submit_data)):

- A text file listing the ensemble IDs and corresponding parameter values, i.e., `PPE_values_<ModelName>.txt` generated by [Latin Hypercube Sampling (LHS) code](https://github.com/hljia/LHS_example). Ensemble ID `exp_0` represents the control run.

- Required outputs from the control run + all LHS-generated ensemble members.

>**Note**: it is recommended to use NetCDF compression (e.g., -z zip_4 in CDO) to reduce output file size.




### Model Output Naming Convention
The format for the AeroCom file name (one variable per file) should be:

`aerocom4_<ModelName>_<YOUR_EXPERIMENT_NAME>-<SimulationName>_<VariableName>_<VerticalCoordinateType>_<Year>_<Freq>.nc`

#### Example Filenames
- **2-D:** `aerocom4_ICON-HAM_<YOUR_EXPERIMENT_NAME>-PD_aod_Surface_2025_monthly.nc`
- **3-D:** `aerocom4_ICON-HAM_<YOUR_EXPERIMENT_NAME>-PD_aod_ModelLevel_2025_monthly.nc`
- **3-D (reduced levels):** `aerocom4_ICON-HAM_<YOUR_EXPERIMENT_NAME>-PD_aerext_CustomLevel_2025_monthly.nc` (only for aerosol extinction)
## References
Ghosh, P., Evans, K. J., Grosvenor, D. P. et al. Assessing modifications to the Abdul-Razzak and Ghan aerosol activation parameterization (version ARG2000) to improve simulated aerosol–cloud radiative effects in the UK Met Office Unified Model (UM version 13.0). Geosci. Model Dev. 18, 4899–4913 (2025). https://doi.org/10.5194/gmd-18-4899-2025

Virtanen, A., Joutsensaari, J., Kokkola, H. et al. High sensitivity of cloud formation to aerosol changes. Nat. Geosci. 18, 289–295 (2025). https://doi.org/10.1038/s41561-025-01662-y

Jia, H., Neubauer, D., Bhatti, Y. et al. Process-level contributions to uncertainty in aerosol effective radiative forcing: a perturbed parameter ensemble with the aerosol–climate model ICON–HAM. EGUsphere [preprint] (2026). https://doi.org/10.5194/egusphere-2026-3275 

