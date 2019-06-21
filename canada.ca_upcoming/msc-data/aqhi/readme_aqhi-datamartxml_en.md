[En Français](readme_aqhi-datamartxml_en.md)

![ECCC logo](../../img_eccc-logo.png)

[TOC](../../readme_en.md) > [MSC Open Public Data](../readme_en.md) > AQHI

# Air Quality Health Index (AQHI) observation and forecast data in XML format

This page describes the the observation and forecast data available in XML format for the [Air Quality Health Index AQHI](readme_aqhi_en.md) that are also available on the [Environment and Climate Change Canada website](https://meteo.gc.ca/airquality/pages/index_e.html). 

## Data location

MSC Datamart data can be [automatically retrieved with the Advanced Message Queuing Protocol (AMQP)](.../../msc-datamart/amqp_en.md) as soon as they become available. An [overview and examples to access and use the Meteorological Service of Canada's open data](.../../usage-overview/readme_en.md) is also available.

The data is available via the HTTP protocol. It is possible to access it with a standard browser. In this case, we obtain a list of links giving access to a XML file.

The data can be accessed at the following address:

* Observations:
   https://dd.meteo.gc.ca/air_quality/aqhi/[atl|ont|pnr|pyr|que]/observation/realtime/xml
  
* Public forecasts:
  https://dd.meteo.gc.ca/air_quality/aqhi/[atl|ont|pnr|pyr|que]/forecast/realtime/xml
  
A file that makes it easier for automated systems to access [real-time updated data](https://dd.meteo.gc.ca/air_quality/doc/AQHI_XML_File_List.xml) is available. 

A [complete list of cities](aqhi.geosjson), with the codes of [CGNDB](http://www4.rncan.gc.ca/search-place-names/unique), Canada's toponymic data maintained by Natural Resources Canada, is available in GeoJSON format. 

## File name nomenclature 

NOTE: ALL HOURS ARE IN UTC.

* **Observations** (Note: monthly summary XML files are not yet available)

  * Hourly file: AQ_OBS_CGNDBcode_YYYYMMDDhhmm.xml
  * Copy of the most recent real-time observation file: AQ_OBS_CGNDBcode_CURRENT.xml

where:

* 'AQ_OBS': Filename prefix. Constant string.
* CGNDBcode: 5-letter [CGNDB](http://www4.rncan.gc.ca/search-place-names/unique) code which identifies each AQHI community. 
* YYYY: Year of the observation, 4 digits;
* MM: Month of the observation, 2 digits (January = 01);
* DD: Day of the observation, 2 digits;
* hh: Hour of the observation, 2 digits;
* mm: Minute of the observation, 2 digits.

* **Public forecasts** (Note: monthly summary XML files are not yet available):
  * Regular issue:     AQ_FCST_CGNDBcode_YYYYMMDDhhmm.xml
  * Amended forecasts: AQ_FCST_CGNDBcode_YYYYMMDDhhmm_AMD.xml
  * Copy of the most recent real-time forecast file: AQ_FCST_CGNDBcode_CURRENT.xml
   
where:

* 'AQ_FCST':  Filename prefix. Constant string.
* CGNDBcode: 5-letter [CGNDB](http://www4.rncan.gc.ca/search-place-names/unique) code which identifies each AQHI communitiy. 
* YYYY: Year of the forecast issue time, 4 digits;
* MM: Month of the forecast issue time, 2 digits (January = 01);
* DD: Day of the forecast issue time, 2 digits;
* hh: Hour of the forecast issue time, 2 digits;
* mm: Minute of the forecast issue time, 2 digits;
* 'AMD': the suffix appended to the filename to indicate that the file is
an amendment.

## Notes

* The XML observation files are produced hourly, at approximately 40 minutes past the hour,
and are available on Datamart for a period of 48 hours. The XML public forecast files are issued
twice per day at approximately 6am and 5pm local time and are available on Datamart for a
period of 48 hours.

* Air quality observations are provided by provinces and municipalities. Provincial jurisdictions also control how observations are communicated to the public. Quebec did not agree to the publication of current air quality in the form of an air quality health index (AQHI). This explains why no observation are available at the address: http://dd.meteo.gc.ca/air_quality/aqhi/que/observation/. However, the Ministère du Développement durable, Environnement et Lutte contre les changements climatiques (MDDELCC) and Ville de Montreal also redistribute some of their data on the American AirNow portal:
https://www.airnowtech.org/index.cfm?page=login 

## Support

If you have any questions about these data, please contact us at: ec.dps-client.ec@canada.ca

## Announcements from the dd_info mailing list 

Announcements related to this dataset are available in the [dd_info list](https://lists.ec.gc.ca/cgi-bin/mailman/listinfo/dd_info).
