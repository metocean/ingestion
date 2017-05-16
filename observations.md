
Ingesting Observation Data on MSL
====

This document is aimed to demonstrate how Observation data can be ingested into MSL data systems, often with the end goal to be visualized on MOV and provide validation reference to Forecast models.

Data format
=====

The most common way to provide data to be ingested it's trough [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) files where each row represents one measurement. One file can contain one or more instruments set of records. 

The measured variables should preferebly be registered as SI units. Here some examples:

 - Significant Wave Heigth: meters
 - Peak period: seconds
 - Current speed: meters/second
 - Current direction (to): degree 
 - Wind speed: meters/seconds
 - Wind direction (from): degree
 - Date and Time (UTC): (ISO-8601)(https://en.wikipedia.org/wiki/ISO_8601)

Altought SI units are preferable, some common units are also accepted, but those needs to be specifically comunicated within the CSV file or other means, for example:

 - Wind Speed: Knots
 - Date and Time (NZT): 2000/12/22 12:44:00
  
The file-name often should contain a reference for the initial date and time the file relates to:

wave_buoy_200012221244.csv

The columns in the CSV are usually composed by:

Instrumend ID, Date and Time (UTC), Variable1, Variable2... 

Exemple...




Ingestion methods
====

FTP Pull: The client provides a FTP server account which we can download the data from.

FTP Push: We provide a FTP server account which the client upload the data.

API Access: Client provide a API web (http) endpoint which we can download the data from.

Email Ingest: Client sends a email to incoming@metoceanview.com with a specific Subject and the data either as a attached file or in the email body.

SSH/SCP Ingest: Clients connect to our SSH servers and upload the data using a SSH Identity Key known by our servers.

Web Scrapping: Client publishes the data in a website and we scrape the contents of the page in order to mine the data
