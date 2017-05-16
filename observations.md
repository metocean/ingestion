
Ingesting Observation Data on MSL
====

This document is aimed to demonstrate how Observation data can be ingested into MSL data systems, often with the end goal to be visualized on MOV and provide validation reference to Forecast models.

Ingestion Methods
====

There are a few methods we currently support for ingesting Observation Data in MOV. Here it's described from most preferable to the least preferable way of doing

1. **FTP Pull**: The client provides an FTP server account which we can download the data from as CSV.

2. **FTP Push**: We provide an FTP server account which the client upload the data as CVS format.

3. **API Access**: Client provides a web API (HTTP/HTTPS) endpoint and access credentials which we can use to download the data from, usually in a JSON format.

4. **Email Ingest**: Client sends an email to incoming@metoceanview.com with a specific Subject and the data either as an attached file or in the email body.

5. **SSH/SCP Ingest**: Clients connect to our SSH servers and upload the data using an SSH Identity Key known by our servers.

6. **Web Scrapping**: Client publishes the data on a website and we scrape the contents of the page in order to mine the data

Data format
====

The most common way to provide data to be ingested it's as [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) files where each row represents one measurement. One file can contain one or more instrument set of records.

The measured variables should preferably be registered as SI units. Here some examples:

 - Significant Wave Height: meters
 - Peak period: seconds
 - Current speed: meters/second
 - Current direction (to): degree
 - Wind speed: meters/seconds
 - Wind direction (from): degree
 - Date and Time (UTC): [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601)
 - Latitude and Longitude (WGS84): decimal degrees

Although SI units are preferable, some common units are also accepted, but those needs to be specifically communicated within the CSV file or at set-up time, for example:

  - Wind Speed: Knots
  - Date and Time (NZT): 2000/12/22 12:44:00

**Time Zone:** Different Time Zones are also supported but UTC is preferable.ssrth instead of the Magnetic North but that's not always the case.

**Directional Variables:** such as Wind Direction and Current Direction, it's important to be mentioned during the set-up process if the data has been [Magnetic Corrected](https://en.wikipedia.org/wiki/Magnetic_declination) or not. This correction can be done at our side if not applied by the instrument. Often instruments can provide the angle related to the True north instead of the Magnetic North but that's not always the case.

**Vertical position:** The vertical position of a measurement must be referred to MSL on WGS84. If not, the appropriate correction scheme must be mentioned at set-up time.

**Latitude and Longitude:** It's assumed that all coordinates are in WGS84 datum, thus assumed that the coordinates are in [SRID 4326](http://spatialreference.org/ref/epsg/wgs-84/).

**Missing Values:** Sometimes an instrument will not have all variables available for all the records so missing values should be defined either as blank space in CSV or -999. The first would be preferable, example:

With values:
```
Buoy1, 2000-12-22T00:00:00,3,4,10
```
With missing values:
```
Buoy1, 2000-12-22T00:00:00,,,10 (the sequence of comma represent missing values for those columns)
```
**File names:** The file-name often should contain a reference to the initial date and time the file relates to:
```
wave_buoy_200012221244.csv
```
**Columns:** The columns in the CSV file are usually composed by:
```
Instrument ID, Date and Time (UTC), Latitude, Longitude, Variable1, Variable2,...

Buoy1, 2000-12-22T00:00:00,-33.4423, 156.0455,3.33,5.55,...
```
Ideally, the data file should contain one or more header lines. If does not contain a header, the data columns should be informed at set-up time.
