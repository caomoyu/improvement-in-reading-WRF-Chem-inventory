# improvement-in-reading-WRF-Chem-inventory
I modified the wrfchemi* file reading, making continuously running WRF-Chem and dynamically update monthly inventory possible 

Since most of emission inventories used in WRF-Chem is monthly updated, so if users want to run a case that last more than
a month, the wrfchemi_00z and wrfchemi_12z file still remain last month, and won't update.

Even through there is an option 'io_style_emissions' in namelist.input, when it is set to 1, WRF-Chem will use wrfchemi_00z and wrfchemi_12z file to 
represent the emission in a month. When it is set to 2,  it can use daily form with 'wrfchemi_00z_year_month_day'. However, every single file within
a month is identical, which is storage costly.

In this program, I modified the wrfchemi file reading preocess in 'WRF/share/mediation_integrate.F', it can use new wrfchemi_in file named 
wrfchemi_year_month which still use io_style_emissions=1, and it allows users to run WRF-Chem case without restarting or run WRF-Chem every 
sigle month.
