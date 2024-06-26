
Ingesting Observation Data on MetService Data Systems
====

This document aims to demonstrate how Observation data can be ingested into MetService data systems, often with the goal to be visualized on MetService Insights Platform (MIP) and provide validation reference to Forecast models.

Ingestion Methods
====

We currently support a few methods for ingesting Observation Data in MIP. Here, it's described from the most preferable to the least preferable way of doing

1. **FTP Pull**: The client provides an FTP/SFTP/FTPS server account from which we can download the data as CSV.

2. **FTPS Push**: We provide an FTPS server account in which the client uploads the data in CVS format.

3. **API Access**: The client provides a web API (HTTP/HTTPS) endpoint and access credentials, which we can use to download the data, usually in a JSON format.

4. **SSH/SCP Ingest**: Clients connect to our SSH servers and upload the data using an SSH Identity Key known by our servers.

5. **Web Scrapping**: The client publishes the data on a website, and we scrape the contents of the page to mine the data


# Station Metadata (buoy, ship, AWS, etc)

 **Station name**: It is usually the client's hardware name. It is not *not mandatory*. e.g. *Esp_BC2 Water Height*.

 **Description**: It is usually the client's description of the hardware. e.g. *Beacon 2 AWAC and E2M Beacon 2 Meteorology*.

 **Coordinates**: The station coordinates (latitude/longitude) in decimal degrees format.

 **Vertical position:** The vertical position of a measurement must be referred to MSL on WGS84. If not, the appropriate correction scheme must be mentioned at set-up time.


> The **Level** is usually the altitude relative to the Mean Sea Level (MSL) where the measurement was taken.
For atmospheric stations, the information provided is assumed to be the sum of “ground_level” and the sensor’s height. Sometimes, the station's measurements may already be normalized to 10m height, particularly for AWS.
For oceanic observations, the level is considered the same as “negative depth” from the water surface.

Data format
====

The most common way to provide data to be ingested it's as [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) files where each row represents one measurement. One file can contain one or more instrument sets of records.

The measured variables should preferably be registered as SI units. Here are some examples:

 - Significant Wave Height: meters
 - Peak period: seconds
 - Current speed: meters/second
 - Current direction (to): degree
 - Wind speed: meters/seconds
 - Wind direction (from): degree
 - Date and Time (UTC): [ISO-8601](https://en.wikipedia.org/wiki/ISO_8601)
 - Latitude and Longitude (WGS84): decimal degrees

Although SI units are preferable, some common units are also accepted, but those need to be specifically communicated within the CSV file or at set-up time, for example:

  - Wind Speed: Knots
  - Date and Time (NZT): 2000/12/22 12:44:00

**Time Zone:** Different Time Zones are also supported but **UTC** is preferable.

**Directional Variables:** such as Wind Direction or Current Direction is assumed to use True North [Magnetic Corrected](https://en.wikipedia.org/wiki/Magnetic_declination) instead of Magnetic North. Regarding the latter, it can be corrected on our side. Often, instruments provide the angle related to the True North instead of the Magnetic North, but that's not always the case.


**Latitude and Longitude:** It's assumed that all coordinates are in the WGS84 datum, thus assuming that the coordinates are in [SRID 4326](http://spatialreference.org/ref/epsg/wgs-84/).

**Missing Values:** Sometimes an instrument will not have all variables available for all the records, so missing values should be defined either as *blank space* in CSV or *-999*. The first would be preferable, for example:

With values:
```
Buoy1, 2000-12-22T00:00:00,3,4,10
```
With missing values:
```
Buoy1, 2000-12-22T00:00:00,,,10 (the sequence of comma represent missing values for those columns)
```
**File names:** The file name often should contain a reference to the initial date and time the file relates to:
```
wave_buoy_200012221244.csv
```
**Columns:** The columns in the CSV file are usually composed by:
```
Instrument ID, Date and Time (UTC), Latitude, Longitude, Variable1, Variable2,...

Buoy1, 2000-12-22T00:00:00,-33.4423, 156.0455,3.33,5.55,...
```
Ideally, the data file should contain one or more header lines. The data columns should be informed at the set-up time if they do not contain a header.

Data and Service documentation
====

In cases where the client wants to provide the data through an API service, it should come with the documentation about how to use/access this service: the Auth method, Query parameters, update frequency, etc.
It is also important to have a data documentation explaining the data structure, the variables, etc.

See the [Wiki](https://metservice.atlassian.net/wiki/spaces/METOCEAN/pages/105318490/Client+s+API+documentation) for examples
