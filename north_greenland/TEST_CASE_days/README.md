# North-greenland prognostic test case

test derived from the roginal SMB and BMB simulations.

- INIT.sif: initialisation step [OPTIONAL: if you don't have the data copy result_test1_0000.nc from the log. dir]
- test1.sif: restart netcdf file from the INIT step. 
- test1_0002.sif: restart from test1

XIOS: config. files:
- iodef.xml: XIOS config.
- context_elmerice.init.xml : contesxt to use foer the INIT (just disable output of all files except the result file that can be restarted)
- context_elmerice.xml: context for the transient simulations 

## pending issues

- Visualisation

- Detached/Attached mode
	- Detached mode cutrrently not working with Elmer restart file
	- But we can restart from netcdf... 
		- only one file so restart easy if partitionning change (:warning: if global numbering is preserved!)  
		- should be easy to implement serial remeshing in the workfow
		- inetrmediate steps are stored at full years while using time interval with elmer shift by one time-step
	- still keep a result file from Elmer => try to save only required variables?


- Calendar:
	- Choose a calendar - Better if time-setp is an integer .... more options with 360 days
	- units? years (calendar dependant - how to insure consistency between unit conversion in elmer and xios) - days ?

- Versionning and sharing xios config files?
	- split files with "mandatory" Elmer variables and ismip6 variables
	- some variables will depend on the forcing... e.g. distance to GL for PICO... Or friction law (effective pressure) - Implement this by default anyway?

- Xios config. file
	- units for ismip6 variables? how to insure constancy with time unit conversion in Elmer and xios and density?
	- check inheritances of long and standard names.....
	- Only use long names for Elmer variables and keep standard_names for ismip6 output in the good unit sytems?
	- add meta data about model configuration (friction law,..)? Define projection; other meta data required?
	- file naming
	- scalar values shoudl be corrected for projection distorsion... 
		- we can compute cell_area with e.g. CDO and import this in Elmer  ; could be computed in Elmer?
		- is it equivalent for fluxes at GL and front?
	- elevations (bed, zs, zb) are with respect to a datum; BedMachine is geoid I think? ISMIP6 requires ellipsoid? anyway shoudl add the ref. in the meta data...
	- compute elevation above flotation
	- Implement sub-element for grounded/floating ice fractions?
	- calving flux: how to prevent inflow?
	- GL flux; should boundaries be defined as GL (if bed below sea level)? must adpat flux computation; do not compute flux if a GL edge is shared by to floating element?
	- Variables by Egde for the fluxes? Define a Edge variable?
	- computations by bassin?



