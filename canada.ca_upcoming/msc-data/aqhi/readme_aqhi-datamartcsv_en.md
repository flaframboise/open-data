[En Français](readme_aqhi-datamartcsv_en.md)

![ECCC logo](../../img_eccc-logo.png)

[TOC](../../readme_en.md) > [MSC Open Public Data](../readme_en.md) > AQHI

# Observation and forecast data generated in CSV format for the Air Quality Health Index (AQHI) program

This page describes the observation and forecast data available in CSV format for the [Air Quality Health Index AQHI](readme_aqhi_en.md) that are also available on the [Environment and Climate Change Canada website](https://meteo.gc.ca/airquality/pages/index_e.html). 

## Data location

MSC Datamart data can be [automatically retrieved with the Advanced Message Queuing Protocol (AMQP)](.../../msc-datamart/amqp_en.md) as soon as they become available. An [overview and examples for accessing and using the Meteorological Service of Canada's open data](../../usage-overview/readme_en.md) is also available.

The data is available via the HTTP protocol. It is possible to access it with a standard browser. In this case, we obtain a list of links giving access to a CSV file.

The data can be accessed at the following address:

* **Observations**: 

  * Files in real time: 
    https://dd.meteo.gc.ca/air_quality/aqhi/[atl|ont|ont|pnr|pyr|que]/observation/realtime/csv
  
  * Monthly files:  
    https://dd.meteo.gc.ca/air_quality/aqhi/[atl|ont|ont|pnr|pyr|que]/observation/monthly/csv

* **Public forecasts**:

  * Monthly files:
    https://dd.meteo.gc.ca/air_quality/aqhi/[atl|ont|ont|pnr|pyr|que]/forecast/monthly/csv
    
* **Data from numerical models**:

   * https://dd.weather.gc.ca/air_quality/aqhi/[atl|ont|ont|pnr|pyr|que]/forecast/model/csv

Note: Real-time CSV files are produced on an hourly basis and contain the data for the last 7 days. They are available on the MSC Datamart for a period of 8 days. MONTHLY" CSV files are produced at the end of each month. They are available on the MSC Datamart for a period of 12 months.
    
## File name nomenclature 

NOTE: ALL HOURS ARE IN UTC.

* **Observations**: 
  
  * Real-time files: YYYYYMMDDhh_AQHI_REGION_OBSTYPE.csv
  * Monthly files: AAAAMM_MONTHLY_AQHI_REGION_OBSTYPE.csv
  * Monthly files with backfilled data:  AAAAMM_MONTHLY_AQHI_REGION_OBSTYPE_BACKFILLED.csv
  
where: 

* YYYYY: year of observation, 4 digits;
* MM: month of observation, 2 digits (January = 01);
* JJ: day of observation, 2 digits;
* hh: hour of observation, 2 digits;
* mm: minute of observation, 2 digits;
* MONTHLY': symbol that is present when the file contains data for the month;
* REGION: Name of Environment and Climate Change Canada region where the observations are located. The values
possible are as follows:
    * ATL' = Atlantic Region,
    *'ON' = Ontario Region,
    * NRP' = Prairie and Northern Region,
    * PYR' = Pacific and Yukon Region,
    *'QC' = Quebec Region;
* OBSTYPE: type of observation in the file. The possible options are as follows:
    * SiteObs' = the file contains AQHI observations for communities,
    * StationObs' = the file contains AQHI observations for the associated observation stations
    to communities (not available in January 2012).
* BACKFILLED': symbol that is present when the file contains AQHI observations that
    are not calculated in real time, but are calculated from the backfilled data or corrected (received within 48 hours of the validity time).

* **Public forecasts**: 

  * AAAAMM_MONTHLY_AQHI_CGNDBcode_SiteFcst.csv

where: 

* YYYYY: year of forecast, 4 digits;
* MM: month of forecast, 2 digits (January = 01);
* MONTHLY': symbol that is present when the file contains data for the month;
* CGNDB_code: a [5-character code](http://www4.rncan.gc.ca/search-place-names/unique) that identifies each community in the AQHI. 
* SiteFcst': symbol that is present to indicate that the file contains AQHI forecasts for a community.

A [complete list of cities](aqhi.geojson), with the codes of [CGNDB](http://www4.rncan.gc.ca/search-place-names/unique), Canadian toponymic data maintained by Natural Resources Canada, is available in GeoJSON format.

* **Data from numerical models**:

  * AAAAMMDDhh_SPECIES_REGION_MODELTYPE.csv
    
where:

* YYYYY: year for which data were generated, 4 digits;
* MM: month for which data were generated, 2 digits (January = 01);
* DD: day for which the data was generated, 2 digits;
* hh: hour for which the data was generated, 2 digits (00 or 12 UTC);
* SPECIES': name of the chemical species in the file. The possible options are as follows:
    * 'O3' = ozone
    * 'NO2' = nitrogen dioxide
    * PM2.5' = particles with a diameter of less than 2.5 um,
    * 'PM10' = particles with a diameter of less than 10 um,
    * 'AQHI' =Air Quality Health Index,
* REGION: Name of the Environment and Climate Change Canada region for which the data are valid. The values
possible are as follows:
    * 'ATL' = Atlantic Region,
    * 'ON' = Ontario Region,
    * 'PNR'' = Prairie and Northern Region,
    * 'PYR' = Pacific and Yukon Region,
    * 'QC' = Quebec Region;
* MODELTYPE: Indicates the system used to generate the data. The possible options are as follows:
    * 'AQFM' = air quality prediction model,
    * 'UMOSAQ' = the "Updateable Model Output Statistics" post-processing system applied to the raw outputs of the AQFM,
    * 'UMOSAQMIST' = the combined data of the AQFM and UMOSAQ systems; generated to provide additional information
    to meteorologists because UMOSAQ data are not always directly available at observation points.

## File content

* **CSV files with AQHI observations calculated from pollutant data received in real-time** (for files in "real-time" and "MONTHLY" format):

  * **Header**
  
   The header is given on the first line and contains the following information:
   
   Date,Hour,CGNDB_Site1,CGNDB_Site2,...,CGNDB_SiteN
   
    where:
    
      * 'Date': fixed string
      * 'Hour': fixed string
      * CGNDB_Site#: a 5-letter CGNDB code that identifies each AQHI community. 

  * **Data block**
  
   Observations are provided with an accuracy of two decimal.
   
   Each line of a data block contains the following information:

    YYYYY-MM-DD,hh,AQHI_Site1,AQHI_Site2,...,AQHI_SiteN

    where:
    
      * YYYYY: the year of observation.
      * MM: the month of observation.
      * DD: the day of observation.
      * hhh: hour for observation.
      * AQHI_Site#: AQHI observations for all communities in the region.

    Note: For real-time files, AQHI observations cover the latest seven days with the most recent observation on the first line. They are available on the MSC Datamart for a period of 48 hours. For "MONTHLY" files, the AQHI observations cover the period from month end (first line) to beginning of the month (in the last line). They are available on the MSC Datamart for a period of time of 12 months.

* **CSV files with AQHI observations calculated from backfilled or corrected data** (only files in "MONTHLY" format):

  These products have the same description as for the "MONTHLY" files provided in 2.1.1. However, the
content is different in that the AQHI values are calculated 48 hours after the validity time for
allow the arrival of missing data and corrections for pollutants. 

* **CSV files with public AQHI forecasts** (only "MONTHLY" files):

  * **Header**
  
   The header is given on the first line and contains the following information:

   cgndb code,community name,issue date,issue time,period,period,value,amended

   where the values are all the symbols that describe the content of the following lines.

  * **Data block**
  
   Public forecasts are provided in whole numbers.
   
   CGNDBcode,CommunityName,IssueDate,IssueTime,ForecastPeriod,Value,AmendmentFlag

   where:
   
      * CGNDBcode: a 5-character code that identifies each AQHI community. 
      * CommunityName: the name used to identify the community associated with the CGNDB code, for which the forecast is valid,
      * IssueDate: the day for which the forecast was issued (YYYY-MM-DD),
      * IssueTime: the exact time the forecast was issued (hh:mm:ss),
      * ForecastPeriod: integer with a value of 1, 2, or 3, which represents the forecast period ("Today", "Tonight and Night", or "Tomorrow", respectively),
        - for forecasts issued at 06:00 (local time): 1=Today, 2=Today and tonight, 3=Tomorrow
        - for forecasts issued at 17:00 (local time): 2=This evening and tonight, 3=Tomorrow
      * Value: value of the AQHI forecast for the forecast period in question,
      * AmendmentFlag: integer with a value of 0 for the first emission of the forecast and which is incremented by +1 for each subsequent amendment.

    Note: In these "MONTHLY" files, AQHI public forecasts are written with the most recent issue
(at the end of the month) in the first line and they proceed to move back in time to the first issue (at the beginning
of the month) in the last line. They are available on the MSC Datamart for a period of 12 months.

* **CSV files that contain model data**:
 
  * **Header**
  
   The header is given on the first line and contains the following information:

    1) For files that contain pollutant data (O3, NO2, PM2.5, PM10):
    stationId, forecast date (time 0), forecast date (time 1),... forecast date (time48)

    2) For files that contain AQHI data:
    cgndb,forecast date (hour0),forecast date (hour1), ... , forecast date (hour47),forecast date (hour48)

    where:
    
      * "stationId" is a symbol that states that the values in the first column identify stations in the region of interest;
      * "cgndb" is a symbol that states that the values in the first column identify the communities in the region of interest;
      * The 49 values following stationId are the dates (format=YYYYYMMDDhh) that define the forecast time (H+000 to H+048) of the model and are applicable to all stations.
  
  * **Data block**
 
   Model data for all species are provided to 2 decimal.
   
   Each line of a data block contains the following information:

   1) For files that contain pollutant data (O3, NO2, PM2.5, PM10):
StationID, Value (H+000), Value (H+001), ... Value (H+047), Value (H+048)

   2) For files that contain AQHI data:
StationID, Value (H+000), Value (H+001), ... Value (H+047), Value (H+048)

   where:
   
       * StationID: NAPS ID that identifies the observation station to which the model data is provided.
       * CGNDBcode: a 5-character code that identifies each AQHI community. A list of CGNDB codes is given at the end of this file.
       * Value (H+000 to H+048): model value derived at the observation station (for UMOSAQ) or interpolated at the observation station (for AQFM, UMOSAQMIST). 
  
## Notes

* Real-time CSV files are produced on an hourly basis and contain the data for the last 7 days. They are available on the MSC Datamart for a period of 8 days. "MONTHLY" CSV files are produced at the end of each month. They are available on the MSC Datamart for a period of 12 months.

* In the CSV files for the AQHI, the value of the first hour is always missing because the AQHI formula
requires a minimum of two hours in the last 3 hours to calculate moving averages.

* In CSV files for UMOSAQ, it is possible that some values are missing since UMOS guidance may not be available
for all hours. The availability of UMOS guidance for a specfic hour is dependent upon having sufficient historical
data to be able to generate reliable predictive statistical equations.

* Air quality observations are distributed by provinces and municipalities. Provincial jurisdictions control how comments are communicated to the public. Quebec has not authorized the publication of air quality data in the form of an Air Quality Health Index (AQHI). This explains why there are no observations under the directory: http://dd.meteo.gc.ca/air_quality/aqhi/que/observation/ . However, the Ministry of Sustainable Development, Environment and Climate Change and the City of Montreal also distribute some of their data on the American portal AirNow: https://www.airnowtech.org/index.cfm?page=login.

## Support

If you have any questions about these data, please contact us at: ec.dps-client.ec@canada.ca

## Announcements from the dd_info mailing list 

Announcements related to this dataset are available via the [dd_info](https://lists.ec.gc.ca/cgi-bin/mailman/listinfo/dd_info) list

  