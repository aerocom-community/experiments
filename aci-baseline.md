ACI "Baseline" Experiment
=========================

<!-- One way to get this into other formats (e.g., docx for the google doc version) -->
<!--  pandoc --highlight-style=pygments -s -f gfm+smart -t latex -o aci.tex aci-baseline.md -->

<!-- [comment]: # Repository: -->
<!-- aerocom-users:/metno/aerocom/work/aerocom1/INDIRECT3 -->

## Preliminary remarks ##

This document is a **draft** meant to structure discussion at the Lille
workshop.  **We are actively soliciting comments.**  You can provide comments in
any of the following ways:
 
 1. Contact Johannes Mülmenstädt by email (<johannes.muelmenstaedt@pnnl.gov>)
 1. Leave a comment or edit the [google docs version of this
    document](https://docs.google.com/document/d/1TlV4SynIRs0v6d8X2GwikCh9I8D_XKCw/edit?usp=sharing&ouid=111193538246169007999&rtpof=true&sd=true) _in suggestion mode_
 1. Interact directly with the [master version of this document on
    GitHub](https://github.com/jmuelmen/AeroCom-Phase4/aci-baseline.md) (e.g., via a
    pull request containing your proposed changes)
	
Johannes Mü will collate comments and suggestions, and they will be discussed at the Lille
workshop. 

## Data submission deadline ##

**TBD at Lille workshop** 

## Simulation setup ##

* Five years nudged to winds (not temperature or humidity)
* Preferred: Nudge toward ECMWF reanalysis winds 
* Acceptable: Nudge toward winds from one baseline simulation by your model 
* Simulation start year **TBD** to weigh the trade-off between satellite
availability, recent features in the temperature and forcing time series, etc.
Will include the overall Phase 4 baseline year.
* all_2000: simulation PD (present-day): year 2000 IPCC aerosol emissions 
* all_1850: simulation PI (preindustrial): year 1850 IPCC aerosol emissions (year 2000 GHG concentration, nudged to present-day winds)
<!-- *   Forcing by AMIP2 sea surface temperature and sea-ice extent  
 *   Greenhouse gas concentrations for year 2000  -->

<!-- [comment]: # these sound like beyond-the-baseline -->
<!-- [comment]: #  *   hom_2000: present day emissions no heterogeneous nucleation of ice in cirrus clouds with T%%<%%-37 C -->
<!-- [comment]: #  *   hom_1850: as in hom_2000, but for pre-industrial emissions  -->
<!-- [comment]: #  *   fix_2000: present day emissions fixed ice nucleation for T%%<%%-37 C using a constant ice number of 383.6 /L, which is from Cooper (1986) at T=-37C  -->
<!-- [comment]: #  *   fix_1850: as in fix_2000, but for pre-industrial emissions   -->

## Motivation ##

The AeroCom Phase 4 "ACI baseline" experiment design builds on the highly
successful [Phase 2 Indirect Effect Experiment ("Indirect3")](https://wiki.met.no/aerocom/indirect), updated to address
the new science questions that have emerged since (and, in many cases, as a
result of) Indirect3.  We have aimed to retain what made Indirect3 great, moved
the technically more challenging aspects into "beyond-the-baseline" experiments
that modelers can opt into separately, and updated the output request with things we
wish had been included.

<!-- Broadly, the purpose of the experiment is to address persistent key areas of uncertainty: 1) the sensitivity of cloud liquid water path to aerosol, and 2) the competition between heterogeneous and homogeneous nucleation of ice crystals.  -->

<!-- To address issue 1), we’ve added daily and monthly diagnostics that can be compared with CloudSat and MODIS retrievals of the relationship between the aerosol optical depth and the probability of precipitation (Wang et al., 2012).  -->

<!-- To address issue 2), we’ve added experiments in which heterogeneous nucleation is neglected for T%%<%%-37C, and in which ice nucleation for T%%<%%-37C is a prescribed function of temperature (Cooper, 1986). -->

<!-- We also have added a requirement to nudge toward analyzed winds, which we’ve found greatly reduces the noise due to natural variability without significantly inhibiting the cloud response to the aerosol. (Kooperman et al., 2012). Simulations of six years duration each should be sufficient for all experiments.  -->

<!-- To facilitate analysis and comparison before the 2013 AeroCom meeting, the results should be submitted to the AeroCom repository by December 1, 2013. Please contact steve.ghan@pnnl.gov and xiaohong.liu@pnnl.gov when your results have been submitted. -->


<!-- Cooper, W. A.: Ice initiation in natural clouds. precipitation enhancement – a scientific challenge, Meteor. Mon., 43, 29–32, 1986. -->

<!-- Kooperman, G. J., M. S. Pritchard, S. J. Ghan, R. C. J. Sommerville, and L. M. Russell, 2012: Constraining the influence of natural variability to improve estimates of global aerosol indirect effects in a nudged version of the Community Atmosphere Model 5. J. Geophys. Res., 117, doi:10.1029/2012JD018588. -->

<!-- Wang, M., S. Ghan, X. Liu, T. L’Ecuyer, K. Zhang, H. Morrison, M. Ovchinnikov, R. Easter, R. Marchand, D. Chand, Y. Qian, and J. E. Penner, 2012: Strong constraints on cloud lifetime effects of aerosol using satellite observations. Geophys. Res. Lett., 39, 15, doi:10.1029/2012GL052204. -->

    
## Diagnostics ##

 *   All data is to be collected at the AeroCom server.
 *   Follow the aerocom data protocol (http://aerocom.met.no/protocol.html)
 *   Data in NetCDF format, one variable and year per file with CMOR variable names
 *   All data are 3-dimensional, e.g., ``( lon x lat x time )``; if your model
     uses other than a lon-lat coordinate system, please provide the data in
     your model's native format (no post-processing remapping)
 *   Filename format is ``aerocom_<ModelName>_<ExperimentName>_<VariableName>_<VerticalCoordinateType>_<Period>_<Frequency>.nc``,\
    where ``<ModelName>`` can be chosen such that model name, model version and possibly the institution can be identified. No underscores (``_``) are allowed in ``<ModelName>``. Use (-) instead. Max 20 characters. \
    ``<ExperimentName>`` = ``all_2000``, ``all_1850``\
    ``<VariableName>`` see list below \
    ``<VerticalCoordinateType>`` => "Surface", "TOA", "Column", "ModelLevel" \
    ``<Period>`` => "2008", "2010", ... (note at this point *period TBD*) \
    ``<Frequency>`` => "timeinvariant","hourly", ,"3hourly", "daily", "monthly" 
 *  CFMIP COSP diagnostics provided by COSP do not need to be run through cmor because the names are the same, 
      but please separate files for each variable

<!-- In addition to the diagnostics below, it is highly recommended to store the AEROCOM standard and forcing diagnostics, so that the simulations can be analysed for the direct forcing as well, and future more in-depth analyses are possible.  -->

### 5 years of 2D diagnostics (3-hourly instantaneous) ### 

For evaluation with satellite data and for ERFaci decomposition (Gryspeerdt et al. 2020)

| name | long_name (CF if possible) | units | description |
| ---- |  ---- |  ---- |  ---- |
| od550aer  | atmosphere_optical_thickness_due_to_aerosol | 1 | Aerosol optical depth (@ 550 nm) |
| aod550aer  | atmosphere_absorbinh optical_thickness_due_to_aerosol | 1 | Aerosol optical depth (@ 550 nm) |
| angstrm | AOD_Angstrom_exponent | 1 | |
| aerindex |aerosol_index  | 1  | od550aer*angstrm |
| cdr | liquid_cloud-top_droplet_effective_radius | m  | Grid cell mean droplet effective radius at top of liquid water clouds |
| cdnc | liquid_cloud_droplet_number_concentration | m-3 | Grid cell mean droplet number concentration in top layer of liquid water clouds |
| cdnum  | column_cloud_droplet_number_concentration    | m-2  | grid cell mean column total |
| icnum  | column_ice_crystal_number_concentration    | m-2  | grid cell mean column total |
| clt | cloud_area_fraction | 1 | Fractional cover by all clouds |
| lcc | liquid_cloud_area_fraction  | 1 | Fractional cover by liquid water clouds |
| lwp | atmosphere_cloud_liquid_path | kg m-2 | grid cell mean liquid water path for liquid water clouds |
| iwp | atmosphere_cloud_ice_path | kg m-2 | grid cell mean ice water path for ice clouds |
| icr | cloud-top_ice_crystal_effective_radius | m | grid cell mean effective radius of crystals at top of ice clouds |
| icc | ice_cloud_area_fraction | 1  | Fractional cover by ice clouds |
| cod | cloud_optical_depth | 1 	| Grid cell mean cloud optical depth |
| codliq | cloud_optical_depth_due_to_liquid | 1 	| Grid cell mean cloud optical depth |
| codice | cloud_optical_depth_due_to_ice | 1 	| Grid cell mean cloud optical depth |
| ccn0.1bl | cloud_condensation_nuclei_0.1_pbl | m-3 | CCN number concentration at S=0.1% at 1 km above the surface |
| ccn0.3bl | cloud_condensation_nuclei_0.3_pbl | m-3 | CCN number concentration at S=0.3% at 1 km above the surface |
| colccn.1 | column_cloud_condensation_nuclei_0.1 | m-2 | column-integrated CCN number concentration at S=0.1%  |
| colccn.3 | column_cloud_condensation_nuclei_0.3 | m-2 | column-integrated CCN number concentration at S=0.3%  |
| rsut | toa_upward_shortwave_flux | W m-2 	| TOA upward SW flux, all-sky |
| rsutcs | toa_upward_shortwave_flux_assuming_clear_sky | W m-2 | TOA upward SW flux, clear-sky |
| rsutnoa | toa_upward_shortwave_flux_no_aerosol | W m-2 | TOA upward SW flux, all-sky, aerosol removed from calculation |
| rsutcsnoa | toa_upward_shortwave_flux_clear_sky_no_aerosol |W m-2 | TOA upward SW flux, clear-sky, aerosol removed from calculation |
| rlut | toa_upward_longwave_flux | W m-2 | TOA upward LW flux, all-sky |
| rlutcs | toa_upward_longwave_flux_assuming_clear_sky | W m-2 | TOA upward LW flux, clear-sky |
| hfls 	| surface_upward_latent_heat_flux | W m-2 | Surface latent heat flux |
| hfss | surface_upward_sensible_heat_flux  | W m-2 | Surface sensible heat flux |
| rls | surface_net_downward_longwave_flux_in_air | W m-2 | Net surface LW downward flux |
| rss | surface_net_downward_shortwave_flux | W m-2 | Net surface SW downward flux |
| rsds | surface_downwelling_shortwave_flux_in_air | W m-2 | Surface SW downward flux (to estimate the model's 'true' surface albedo) |
| ttop | air_temperature_at_cloud_top | K | Temperature at top of clouds, weighted by cloud cover |
| lts | lower_tropospheric_stability | K | Difference in potential temperature between 700 hPa and 1000 hPa |
| u10  | zonal wind at 10 m height | m s-1 | provide lowest model level wind if 10 m is not diagnosed|
| v10  | meridional wind at 10 m height | m s-1 | provide lowest model level wind if 10 m is not diagnosed|
| u700  | zonal wind at 700 hPa | m s-1 | |
| v700  | meridional wind at 700 hPa | m s-1 | |
| u200  | zonal wind at 200 hPa | m s-1 | |
| v200  | meridional wind at 200 hPa | m s-1 | |
| w500  | vertical_velocity_dp/dt_at_500_hPa | hPa s-1 | |
| w700  | vertical_velocity_dp/dt_at_700_hPa | hPa s-1 | |
| lts   | potential temperature difference (theta at 700_hPa -- theta at 1000 hPa) | K | |
| sprecip | stratiform_precipitation_rate	| kg m-2 s-1	| grid cell mean at surface |
| autoconv | column_autoconversion_rate | kg m-2 s-1	| grid cell mean column total |
| accretn | column_accretion_rate	| kg m-2 s-1	| grid cell mean column total |
| wbf | Wegener--Bergeron--Findeisen rate	| kg m-2 s-1	| grid cell mean column total |

### Monthly-mean fields ###

As above, plus a land-ocean mask (0 land, 1 ocean).

### 3D monthly mean diagnostics ###

*TBD* whether these are actually needed

<!-- | name | long_name (CF if possible) | units | description | comment | notes |  -->
<!-- | ---- | ---- | ---- | ---- | ---- | ---- | -->
<!-- | t              | temperature                                      | K          | each layer                                                                                                                                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | hus            | specific_humidity                                | kg/kg      | each layer                                                                                                                                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | z              | altitude                                         | m          | each layer                                                                                                                                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | airmass        | atmosphere_mass_content_of_air                   | kg m-2     | each layer                                                                                                                                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | ccn0.1         | cloud_condensation_nuclei_0.1                    | m-3        | each layer (S=0.1%)                                                                                                                                                                                                                                          |   |      |      |      |      |   | -->
<!-- | ccn0.3         | cloud_condensation_nuclei_0.3                    | m-3        | each layer (S=0.3%)                                                                                                                                                                                                                                          |   |      |      |      |      |   | -->
<!-- | nc             | liquid_cloud_droplet_number_concentration        | m-3        | grid cell mean each layer                                                                                                                                                                                                                                    |   |      |      |      |      |   | -->
<!-- | lwc            | cloud_liquid_water_content                       | kg m-3     | grid cell mean each layer                                                                                                                                                                                                                                    |   |      |      |      |      |   | -->
<!-- | rel            | droplet_effective_radius                         | m          | grid cell mean each layer                                                                                                                                                                                                                                    |   |      |      |      |      |   | -->
<!-- | lccl           | liquid_cloud_fraction                            | 1          | Fractional cover by liquid water clouds each layer                                                                                                                                                                                                           |   |      |      |      |      |   | -->
<!-- | wsubc          | subgrid_vertical_velocity_for_stratiform         | m s-1      |                                                                                                                                                                                                                                                              |   |      |      |      |      |   | -->
<!-- | autocl         | autoconversion_rate                              | kg m-2 s-1 | layer total in grid cell                                                                                                                                                                                                                                     |   |      |      |      |      |   | -->
<!-- | accretl        | accretion_rate                                   | kg m-2 s-1 | layer total in grid cell                                                                                                                                                                                                                                     |   |      |      |      |      |   | -->
<!-- | ni             | ice_cloud_crystal_number_concentration           | m-3        | grid cell mean each layer                                                                                                                                                                                                                                    |   |      |      |      |      |   | -->
<!-- | iwc            | cloud_ice_water_content                          | kg m-3     | grid cell mean each layer                                                                                                                                                                                                                                    |   |      |      |      |      |   | -->
<!-- | rei            | Ice_effective_radius                             | m          | grid cell mean each layer                                                                                                                                                                                                                                    |   |      |      |      |      |   | -->
<!-- | iccl           | ice_cloud_fraction                               | 1          | Fractional cover by ice water clouds each layer                                                                                                                                                                                                              |   |      |      |      |      |   | -->
<!-- | sati           | ice_supersaturation                              | 1          | Supersaturation with respect to ice                                                                                                                                                                                                                          |   |      |      |      |      |   | -->
<!-- | wsubi          | subgrid_vertical_velocity_for_cirrus             | m s-1      |                                                                                                                                                                                                                                                              |   |      |      |      |      |   | -->
<!-- | mmrdu          | mass_fraction_of_dust_dry_aerosol_in_air         | kg/kg      | each layer                                                                                                                                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | mmrbc          | mass_fraction_of_black_carbon_dry_aerosol_in_air | kg/kg      | each layer                                                                                                                                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | mmrso4         | mass_fraction_of_sulfate_dry_aerosol_in_air      | kg/kg      | each layer                                                                                                                                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | cirrus_nso4    | sulfate_aerosol_number_for_homogeneous           | m-3        | grid cell mean sulfate aerosol number used for homogeneous aerosol freezing even if ice not nucleated                                                                                                                                                        |   |      |      |      |      |   | -->
<!-- | cirrus_ndust   | dust_aerosol_number_for_heterogeneous            | m-3        | grid cell mean dust aerosol number used for heterogeneous aerosol freezing even if ice not nucleated                                                                                                                                                         |   |      |      |      |      |   | -->
<!-- | cirrus_nbc     | BC_aerosol_number_for_heterogeneous              | m-3        | grid cell mean BC aerosol number used for heterogeneous aerosol freezing even if ice not nucleated                                                                                                                                                           |   |      |      |      |      |   | -->
<!-- | cirrus_nihom   | homogeneous_nucleation_number                    | m-3        | grid cell mean ice crystal number production from homogeneous aerosol freezing for T%%<%%-37C during one model time step                                                                                                                                     |   |      |      |      |      |   | -->
<!-- | cirrus_nihet   | heterogeneous_nucleation_number                  | m-3        | grid cell mean ice crystal number production from heterogeneous aerosol freezing for T%%<%%-37C during one model time step                                                                                                                                   |   |      |      |      |      |   | -->
<!-- | cirrus_freqhom | homogeneous_nucleation_frequency                 | 1          | frequency counter of homogeneous aerosol freezing for T%%<%%-37C. For each time step, freqhom = 1 if homogeneous ice nucleation happens; otherwise freqhom = 0. Monthly average of this value indicates the homogeneous nucleation frequency.                |   |      |      |      |      |   | -->
<!-- | cirrus_freqhet | heterogeneous_nucleation_frequency               | 1          | frequency counter of heterogeneous aerosol freezing for T%%<%%-37C. At each model time step, set freqhom = 1 if heterogeneous ice nucleation happens; otherwise freqhom = 0. Monthly average of this value indicates the heterogeneous nucleation frequency. |   |      |      |      |      |   | -->
<!-- | mp_hetnuc      | droplet_freezing_rate_by_heterogeneous           | m-3 s-1    | grid cell mean freezing rate of cloud droplets in mixed-phase clouds for T>-37C                                                                                                                                                                              |   |      |      |      |      |   | -->
<!-- | mp_homnuc      | droplet_freezing_rate_by_homogeneous             | m-3 s-1    | grid cell mean instantaneous freezing rate of cloud droplets for T<=-37C                                                                                                                                                                                     |   |      |      |      |      |   | -->

### CFMIP COSP 2D diagnostics (3-hourly instantaneous) ### 

Optional, but highly desirable for models with COSP

| name | long_name (CF if possible) |	units |	description | comment | notes |
| ---- | ---- | ---- | ---- | ---- | ---- |
| clwmodis | modis_liquid_cloud_fraction | 1 | Column fractional cover by liquid water clouds  | from modis simulator |
| reffclwmodis | modis_droplet_effective_radius*clwmodis  | m | grid cell mean  | from modis simulator |
| climodis  | modis_ice_cloud_fraction	|1 | Column fractional cover by ice water clouds  |from modis simulator	|  |
| reffclimodis | modis_ice_effective_radius*climodis	| m | grid cell mean  | from modis simulator |
| tauwmodis | modis_liquid_cloud_optical_thickness*clwmodis | 1 | grid cell mean | from modis simulator |
| tauimodis | modis_ice_cloud_optical_thickness*climodis | 1 | grid cell mean | from modis simulator |
| parasolRefl | toa_bidirectional_reflectance | 1 | PARASOL Reflectance | Simulated reflectance from PARASOL as seen at the top of the atmosphere for 5 solar zenith angles. Valid only over ocean and for one viewing direction (viewing zenith angle of 30 degrees and relative azimuth angle 320 degrees). | |
| cltcalipso | cloud_area_fraction | % | CALIPSO Total Cloud Fraction  | | |
| cllcalipso | cloud_area_fraction_in_atmosphere_layer | % | CALIPSO Low Level Cloud Fraction  | | |
| clmcalipso | cloud_area_fraction_in_atmosphere_layer | % | CALIPSO Middle Level Cloud Fraction  | | |
| clhcalipso | cloud_area_fraction_in_atmosphere_layer | % | CALIPSO High Level Cloud Fraction  | | |

*TBD: include Brandon Duran's/Casey Wall's monthly-mean COSP histogram ERFaci decomposition?*

<!-- (b) 3D -->

<!-- | name | long_name (CF if possible) |	units |	description | comment | notes | -->
<!-- | ---- | ---- | ---- | ---- | ---- | ---- | -->
<!-- | t | temperature	| K	| each layer |	 -->
<!-- | z | altitude          | m       | each layer |	 -->
<!-- | pressure | atmospheric_pressure          | Pa  | each layer | -->
<!-- | airmass | atmosphere_mass_content_of_air    | kg m-2   | each layer  | -->
<!-- | ccn0.1 | cloud_condensation_nuclei_0.1 | m-3	| each layer (S=0.1%) | -->
<!-- | ccn0.3 | cloud_condensation_nuclei_0.3 | m-3	| each layer (S=0.3%) | -->
<!-- | nc | liquid_cloud_droplet_number_concentration | m-3	| grid cell mean each layer | -->
<!-- | lwc| cloud_liquid_water_content | kg m-3	| grid cell mean each layer stratiform cld only|  | -->
<!-- | rel | droplet_effective_radius | m |	grid cell mean each layer stratiform cld only  |  | -->
<!-- | lccl | layer_liquid_cloud_fraction | 1 | Fractional cover by liquid water stratiform clouds each layer | -->
<!-- | ni | ice_cloud_crystal_number_concentration	| m-3	| grid cell mean each layer | -->
<!-- | iwc | cloud_ice_water_content	| kg m-3	| grid cell mean each layer stratiform cld only| -->
<!-- | rei | ice_effective_radius | m | grid cell mean each layer stratiform cld only |       	| | -->
<!-- | iccl   | layer_ice_cloud_fraction  | 1 | Fractional cover by ice water stratiform clouds each layer |	|  | -->
<!-- | dbze94  | 94GHz_radar_reflectivity_subcolumn | dBZe  | Radar reflectivity each model layer in 100 subcolumns   | -->
<!-- | fracout | fracout_cloud_flag_subcolumn | 1 | subcolumn cloud flag each model layer in 100 subcolumns 0 clear, 1 strat 2 conv | -->
<!-- | clcalipso | cloud_area_fraction_in_atmosphere_layer | % | CALIPSO Cloud Area Fraction |  | at 40 height levels | -->
<!-- | clcalipso2   | cloud_area_fraction_in_atmosphere_layer | % | CALIPSO Cloud Fraction Undetected by CloudSat | Clouds detected by CALIPSO but below the detectability threshold of CloudSat | at 40 height levels | -->
<!-- | cfadDbze94 | histogram_of_equivalent_reflectivity_factor_over_height_above_reference_ellipsoid | 1 | CloudSat Radar Reflectivity CFAD | CFADs (Cloud Frequency Altitude Diagrams) are joint height - radar reflectivity  distributions. | 40 levels x 15 bins | -->
<!-- | cfadLidarsr532 | histogram_of_backscattering_ratio_over_height_above_reference_ellipsoid | 1 | CALIPSO Scattering Ratio CFAD | CFADs (Cloud Frequency Altitude Diagrams) are joint height - lidar scattering ratio distributions. | 40 levels x 15 bins | -->

## Sampling of cloud-top quantities ## 

The idea is to use the cloud overlap assumption (maximum, random, or
maximum-random) to estimate which part of the cloud in a layer can be seen from
above.

Note: For the CCN, whether to sample it in the same way as CDNC, or use a similar approach (going from bottom up)    
to sample it at cloud base depends on your parameterization of the activation.

let $i=1,2,...,nx$ be the index for the horizontal grid-points \
let $k=1,2,...,nz$ be the index for the vertial levels, with 1 being the uppermost level, and nz the surface level 

### Naming convention for the 3D input fields: ### 

iovl is the flag to select the overlap hypothesis\
cod3d(nx,nz) cloud optical thickness\
f3d(nx,nz) cloud fraction\
t3d(nx,nz) temperature\
phase3d(nx,nz) cloud thermodynamic phase (0: entire cloud consists of ice, 
1: entire cloud consists of liquid water, between 0 and 1: mixed-phase)\
phase3d could be from fice3d/f3d where fice3d=ice+mixed phase cloud fraction\
cdr3d(nx,nz) in-cloud  droplet effective radius\
icr3d(nx,nz) in-cloud ice crystal effective radius\
cdnc3d(nx,nz) in-cloud droplet number concentration\ 

### "Cloud-top" calculation ### 
This piece of Fortran code was used to calculate the Phase 2 Indirect3 ACI diagnostics.
We suggest using it again for the Phase 4 ACI baseline experiment.  Models that
participated in Phase 2 Indirect3 probably already have an implementation of
this that can be reused. 

``` fortran
thres_cld = 0.001  
thres_cod = 0.3  
IF ( iovl = random OR iovl = maximum-random ) THEN
  clt(i) = 1.
ELSE
  clt(:) = 0
ENDIF  
icc(:) = 0  
lcc(:) = 0  
ttop(:) = 0  
cdr(:) = 0  
icr(:) = 0  
cdnc(:) = 0


DO i=1,nx
	DO k=2,nz ! assumption: uppermost layer is cloud-free (k=1)
		IF ( cod3d(i,k) > thres_cod and f3d(i,k) > thres_cld ) THEN ! visible, not-too-small cloud
			! flag_max is needed since the vertical integration for maximum overlap is different from the two others: for maximum, clt is the actual cloud cover in the level, for the two others, the actual cloud cover is 1 - clt
			! ftmp is total cloud cover seen from above down to the current level
			! clt is ftmp from the level just above
			! ftmp - clt is thus the additional cloud fraction seen from above in this level

			IF ( iovl = maximum ) THEN
				flag_max = -1.
				ftmp(i) = MAX( clt(i), f3d(i,k))  ! maximum overlap	
			ELSEIF ( iovl = random ) THEN
				flag_max = 1.
				ftmp(i) = clt(i) * ( 1 - f3d(i,k) ) ! random overlap	
			ELSEIF ( iovl = maximum-random ) THEN
				flag_max = 1.
				ftmp(i) = clt(i) * ( 1 - MAX( f3d(i,k), f3d(i,k-1) ) ) / &
   	            ( 1 - MIN( f3d(i,k-1), 1 - thres_cld ) )  ! maximum-random overlap	
			ENDIF
			ttop(i) = ttop(i) + t3d(i,k) * ( clt(i) - ftmp(i) )*flag_max 

			! ice clouds
			icr(i) = icr(i) + icr3d(i,k) * ( 1 - phase3d(i,k) ) * ( clt(i) - ftmp(i) )*flag_max 
			icc(i) = icc(i) + ( 1 - phase3d(i,k) ) * ( clt(i) - ftmp(i) )*flag_max 
	
			! liquid water clouds
			cdr(i) = cdr(i) + cdr3d(i,j) * phase3d(i,k) * ( clt(i) - ftmp(i) )*flag_max 
			cdnc(i) = cdnc(i) + cdnc3d(i,j) * phase3d(i,k) * ( clt(i) - ftmp(i) )*flag_max 
			lcc(i) = lcc(i) + phase3d(i,k) * ( clt(i) - ftmp(i) )*flag_max 
			
			clt(i) = ftmp(i)
		ENDIF ! is there a visible, not-too-small cloud?
	ENDDO ! loop over k

	IF ( iovl = random OR iovl = maximum-random ) THEN
		clt(i) = 1. - clt(i)
	ENDIF
ENDDO ! loop over I
```

<!-- naming convention for the input variables: -->

<!--     utctime current time of the day in UTC in seconds   -->
<!--     time_step_len length of model time-step   -->
<!--     lon(nx) longitude in degrees from 0 to 360    -->

 <!-- ==== Q/A ==== -->

 <!-- *    2D cloud fields (lwp, iwp, cdr, cdnc, ttop, cod): Please save them as grid-box mean values but DO NOT divide by the total (2D) cloud cover, which will be done in analysis after averaging in time and space.  -->
         
 <!-- *    The three months 1 October - 31 December 2005  are thought as spin-up, which can of course be longer. Please choose as overlap assumption the one you use in the radiation scheme.   -->
    
 <!-- *    ATTENTION: clt(i) has to be initialized to 1 for random or maximum-random overlap assumptions in the "satellite simulator"   -->

 <!-- *   CCN definition: Compute CCN using Kohler theory at 0.1 and 0.3 % supersaturation. -->
 
