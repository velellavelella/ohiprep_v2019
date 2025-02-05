## MRF Note: 10/4/2016
## MOved from: neptune_data:model/GL-WorldBank-Statistics_v2012/data

GL-WorldBank-Statistics_v2012
===========================

6 datasets (+ 1 derived) accessed through 2011:

* GDP = Gross Domestic Product (current \$USD)
* LAB = Labor force, total (\# people)
* UEM = Unemployment, total (\% of total labor force)
	+ EMP = Employment, total (\% of total labor force), calculated from UEM
* PPP = Purchase power parity
* PPPpcGDP = GDP adjusted per capita by PPP
* POP = Total Population


Files produced
==============
FILES: 

* cntry_wb_emp_2012a.csv
* cntry_wb_emp_2013a.csv
* cntry_wb_gdp_2012a.csv
* cntry_wb_gdp_2013a.csv
* cntry_wb_lab_2012a.csv
* cntry_wb_lab_2013a.csv
* cntry_wb_ppp_2012a.csv
* cntry_wb_ppp_2013a.csv
* cntry_wb_uem_2012a.csv
* cntry_wb_uem_2013a.csv
* country_wb_gdp_2013a.csv
* country_wb_gdppcppp_2013a.csv
* country_wb_ppp_2013a.csv
* rgn_wb_gdp_2012a.csv
* rgn_wb_gdp_2013a.csv
* rgn_wb_gdppcppp_2012a.csv
* rgn_wb_gdppcppp_2013a.csv
* rgn_wb_lab_2012a.csv
* rgn_wb_lab_2013a.csv
* rgn_wb_pop_2012a.csv
* rgn_wb_pop_2013a.csv
* rgn_wb_pop_2013a_updated.csv
* rgn_wb_ppp_2012a.csv
* rgn_wb_ppp_2013a.csv
* rgn_wb_ratio_lab_pop_2012a.csv
* rgn_wb_ratio_lab_pop_2013a.csv
* rgn_wb_uem_2012a.csv
* rgn_wb_uem_2013a.csv

PATH:

* model/GL-WorldBank-Statistics_v2012/data

Description
===========

ACCESS: 
Data taken from separate .xls files
* just Sheet 1 saved
* Lines removed for aggregated regions (lines 2-33): "Arab World" through "World", so that the data begins alphabetically with Afghanistan. 

* GDP: Gross Domestic Product (current \$USD)
	+ http://data.worldbank.org/indicator/NY.GDP.MKTP.CD
	+ saved as WorldBank_GDP_USD_reformatted.csv
* UEM = Unemployment, total (\% of total labor force) 
	+ http://data.worldbank.org/indicator/SL.UEM.TOTL.ZS
	+ saved as WorldBank_UEM_reformatted.csv
* LAB = Labor force, total (\# people)
	+ http://data.worldbank.org/indicator/SL.TLF.TOTL.IN
	+ saved as WorldBank_LAB_reformatted.csv
* PPP = Purchase power parity
	+ http://data.worldbank.org/indicator/NY.GDP.MKTP.PP.CD
	+ saved as WorldBank_PPP_LCU_reformatted.csv
* PPPpcGDP = GDP adjusted per capita by PPP
	+ http://data.worldbank.org/indicator/NY.GDP.PCAP.PP.CD
	+ saved as WorldBank_GDPpcPPP_USD_reformatted.csv
* EMP = Employment, total (\% of total labor force) 
	+ calculated from UEM in clean_WBstats.r 


R scripts involved
==================
SCRIPT:

* clean_WBstats.r 
* (clean_WBstatsOLD.r for record purposes only)


DETAILS: cleaning

loads data from *.csv files and calls add_rgn_id.r to save as GL-WorldBank-Statistics_v2012-cleaned.csv

* POP: POP was removed from the GL-WorldBank-Statistics_v2012-cleaned.csv file and missing countries that couldn't be gapfilled were identified (GL-WorldBank-Statistics_POPtofill.csv) . BH looked them up on wikipedia and saved the file as missing_total_pop_data.csv. JS concatenated this to (GL-WorldBank-Statistics_cleanedOnlyPOP.csv) and saved as rgn_totpop.csv [saved with only 3 columns: rgn_id_2013,count,year]

* EMP calculated: ((100 - UEM) \* LAB)\/ 100;


* these will all be translated from rgn_id (2013) to cntry_id (2013), and some also to country_id (2012) (for LE calculations)
 

Gapfilling 
==========
CATEGORY: SG, XSI, XA

EXCEPTIONS: 

* POP gapfilled by hand with Wikipedia
* All others: Southern Islands set to NA, some will later be over-rided, depending on dataset and island

DETAILS:


2014 Resolutions
================
Add to add_gapfill: 

* catch if data too old/sparse
* combine to _singleyear

Methods
=======

5.5. Artisanal fishing: need
Update: additional year(s) data.
Description: This parameter is estimated by the per capita purchasing power parity (PPP) adjusted gross domestic product (GDP), i.e. GDPpcPPP, as described previously (Halpern et al. 2012; the model treats need as 1- GDPpcPPP). Index Mundi (www.indexmundi.com describes GDP and PPP as:
“GDP is the value of all final goods and services produced within a nation in a given year. A nation's GDP at purchasing power parity (PPP) exchange rates is the sum value of all goods and services produced in the country valued at prices prevailing in the United States in the year noted. This is the measure most economists prefer when looking at per-capita welfare and when comparing living conditions or use of resources across countries. The measure is difficult to compute, as a US dollar value has to be assigned to all goods and services in the country regardless of whether these goods and services have a direct equivalent in the United States (for example, the value of an ox-cart or non-US military equipment); as a result, PPP estimates for some countries are based on a small and sometimes different set of goods and services. In addition, many countries do not formally participate in the World Bank's PPP project that calculates these measures, so the resulting GDP estimates for these countries may lack precision. For many developing countries, PPP-based GDP measures are multiples of the official exchange rate (OER) measure. The differences between the OER- and PPP-denominated GDP values for most of the wealthy industrialized countries are generally much smaller.” 
Updated GDPpcPPP calculations were available through 2012 from the World Bank (http://data.worldbank.org/indicator/NY.GDP.PCAP.PP.CD) and are reported in 2012 US dollars for all years. 

5.24. Gross Domestic Product (GDP) 
Update: additional year(s) available
Description: These data are used in the economies sub-goal of the coastal livelihoods and economies goal to adjust revenue data. Updated GDP data through 2012 (reported in 2012 US dollars) were accessed from the World Bank (data.worldbank.org/indicator/NY.GDP.MKTP.CD). For the three EEZs that fall within the China region (China, Macau, and Hong Kong), we combined the values using a population-weighted average.

5.31. Labor force
Update: new layer introduced in 2013
Description: Data for total labor force (number of people) was obtained from 1980-2012 from World Bank assessments (data.worldbank.org/indicator/SL.TLF.TOTL.IN). The World Bank defines total labor force based on the International Labour Organisation (ILO)’s definition of an economically active population – those 15years old and older who can supply labor for the production of goods and services – and includes those employed and unemployed, as well as those in the armed forces, and generally excludes homemakers and other unpaid caregivers and workers in the informal sector. For the three EEZs that fall within the China region (China, Macau, and Hong Kong), we combined the values by summing across these EEZs.

5.50. National percent unemployment
Update: additional year(s) available
Description: Updated unemployment data through 2012 were available from the World Bank (http://data.worldbank.org/indicator/SL.UEM.TOTL.ZS). These data are reported as the percent of the total labor force that is available to work and seeking employment but is without work. Because other data layers used for the tourism and recreation goal ended in 2011, we used 2011 values for current status calculations. Gap-filling procedures (see section 6 below) were required for >100 regions per year; in 5-20 cases year this produced negative values and in 8-10 cases gap-filling procedures did not have sufficient data to produce a value. For each of these cases we set unemployment to the average per-year value from the regions with reported values (2011 = 8.78%, 2010 = 8.96%, 2009 = 9.34%, 2008 = 8.9%, 2007 = 8.3%, and 2006 8.7%). For the three EEZs that fall within the China region (China, Macau, and Hong Kong), we combined the values using a population-weighted average. 

5.71. Total population
Update: additional year(s) available
Description: Updated population data were available through 2012 from the World Bank (data.worldbank.org/indicator/SP.POP.TOTL). For the three EEZs that fall within the China region (China, Macau, and Hong Kong), we combined the values by summing across these EEZs. For 59 regions, data were not reported and so we searched Wikipedia for population estimates.  Those estimates were for a single year, so to fill missing years we calculated the average per-year change in population across all regions in the World Bank data, and then applied those percent changes to the single year data from Wikipedia.

Note:::use World Bank unemployment data, not CIAfactbook. Updated unemployment data (% of total labor force) were accessed from the 2012 World Bank assessments: http://data.worldbank.org/indicator/SL.UEM.TOTL.ZS, also, don't use World Bank sanitation data; use UNICEF


Metadata
========

GDP:

GDP at purchaser's prices is the sum of gross value added by all resident producers in the economy plus any product taxes and minus any subsidies not included in the value of the products. It is calculated without making deductions for depreciation of fabricated assets or for depletion and degradation of natural resources. Data are in current U.S. dollars. Dollar figures for GDP are converted from domestic currencies using single year official exchange rates. For a few countries where the official exchange rate does not reflect the rate effectively applied to actual foreign exchange transactions, an alternative conversion factor is used.

UEM: 

Unemployment refers to the share of the labor force that is without work but available for and seeking employment. Definitions of labor force and unemployment differ by country.

Sanitation:

Access to improved sanitation facilities refers to the percentage of the population with at least adequate access to excreta disposal facilities that can effectively prevent human, animal, and insect contact with excreta. Improved facilities range from simple but protected pit latrines to flush toilets with a sewerage connection. To be effective, facilities must be correctly constructed and properly maintained.

Labor Force: 

Total labor force comprises people ages 15 and older who meet the International Labour Organization definition of the economically active population: all people who supply labor for the production of goods and services during a specified period. It includes both the employed and the unemployed. While national practices vary in the treatment of such groups as the armed forces and seasonal or part-time workers, in general the labor force includes the armed forces, the unemployed, and first-time job-seekers, but excludes homemakers and other unpaid caregivers and workers in the informal sector.

( also accessed but not used in OHI:)_
* STA = Improved sanitation facilities (% of population with access)
* PPP = Purchase power parity
* PPPpcGDP = GDP adjusted per capita by PPP
* POP = Total population count
