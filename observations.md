
Ingesting Observation Data on MSL
====

This document is aimed to demonstrate how Observation data can be ingested into MSL data systems, often with the end goal to be visualized on MOV and provide validation reference to Forecast models.

Data format
=====

The most common way to provide data to be ingested it's trough (CSV)[https://en.wikipedia.org/wiki/Comma-separated_values] files where each row represents one mesurement. One file can contain one or more instrument set records. The columns are composed  dcdc


Ingestion methods
====

FTP Pull: The client provides a FTP server account which we can download the data from.

FTP Push: We provide a FTP server account which the client upload the data.

API Access: Client provide a API web (http) endpoint which we can download the data from.

Email Ingest: Client sends a email to incoming@metoceanview.com with a specific Subject and the data either as a attached file or in the email body.

SSH/SCP Ingest: Clients connect to our SSH servers and upload the data using a SSH Identity Key known by our servers.

Web Scrapping: Client publishes the data in a website and we scrape the contents of the page in order to mine the data
