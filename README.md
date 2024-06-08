# getting_started_r_bigquery
A repository holding educational materials related to the R/Medicine 2024 workshop on R and BigQuery.

## Topics

In this workshop, we'll cover the following topics:

### Cloud: Getting Started With GCP

* What is "the Cloud"?
* Getting started with Google Cloud Platform (for free!)
* Services we'll use
  * BigQuery: GCP's data warehousing solution 
  * Vertex AI Workbench: 
* Services we won't use (but might be useful later!)
  * RStudio Server
  * GCS

## BigQuery 

* BigQuery public data: We'll be using two public datasets for this workshop:
  - [Births Data Summary from the Centers for Disease Control](https://console.cloud.google.com/marketplace/product/center-disease-control/wonder-births?project=principal-rhino-422713-m3)
  - [Area Deprivation Index (ADI), provided by BroadStreet](https://console.cloud.google.com/marketplace/product/broadstreet-public-data/adi?project=principal-rhino-422713-m3)
* We'll use BigQuery to do some data selection 


## Queries we issue


SELECT
  cdc.Ave_Birth_Weight_gms,
  adi.area_deprivation_index_percent
FROM
  `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` AS cdc 
  INNER JOIN `bigquery-public-data.broadstreet_adi.area_deprivation_index_by_county` AS adi
ON cdc.County_of_Residence_FIPS = adi.county_fips_code AND 
   EXTRACT(YEAR FROM cdc.Year) = adi.year
   
SELECT
  cdc.Ave_Birth_Weight_gms,
  adi.area_deprivation_index_percent,
  cdc.County_of_Residence,
  adi.county_name,
  cdc.Year,
  adi.year
FROM
  `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` AS cdc 
  INNER JOIN `bigquery-public-data.broadstreet_adi.area_deprivation_index_by_county` AS adi
ON cdc.County_of_Residence_FIPS = adi.county_fips_code AND 
   EXTRACT(YEAR FROM cdc.Year) = adi.year
   
   