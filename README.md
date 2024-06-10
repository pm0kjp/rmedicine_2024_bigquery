# getting_started_r_bigquery

A repository holding educational materials related to the R/Medicine 2024 workshop on R and BigQuery.

## Topics

In this workshop, we'll cover the following topics:

### Cloud: Getting Started With GCP

* What is "the Cloud"?
* Getting started with Google Cloud Platform (for free!)
* Services we'll use
  * BigQuery: GCP's data warehousing solution 
  * Vertex AI Workbench: Jupyter notebooks on a Server
  * Our own RStudio... Posit.cloud or on our computers
* Services we won't use (but might be useful later!)
  * RStudio Server
  * GCS

## Slides

Slide shows: 

* <https://pm0kjp.github.io/rmedicine_2024_bigquery/quarto_slides/deck1.html>
* <https://pm0kjp.github.io/rmedicine_2024_bigquery/quarto_slides/deck2.html>
* <https://pm0kjp.github.io/rmedicine_2024_bigquery/quarto_slides/deck3.html>


## BigQuery 

* BigQuery public data: We'll be using two public datasets for this workshop:
  - [Births Data Summary from the Centers for Disease Control](https://console.cloud.google.com/marketplace/product/center-disease-control/wonder-births?project=principal-rhino-422713-m3)
  - [Area Deprivation Index (ADI), provided by BroadStreet](https://console.cloud.google.com/marketplace/product/broadstreet-public-data/adi?project=principal-rhino-422713-m3)
* We'll use BigQuery to do some data selection and grooming before moving to R 


## Queries we issue

```
SELECT
  cdc.Ave_Birth_Weight_gms,
  adi.area_deprivation_index_percent
FROM
  `bigquery-public-data.sdoh_cdc_wonder_natality.county_natality` AS cdc 
  INNER JOIN `bigquery-public-data.broadstreet_adi.area_deprivation_index_by_county` AS adi
ON cdc.County_of_Residence_FIPS = adi.county_fips_code AND 
   EXTRACT(YEAR FROM cdc.Year) = adi.year
```

```
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
```

## Command line 

To build an R kernel in Vertex AI Workbench:

```
conda create -n r
conda config --add channels conda-forge
conda install -c conda-forge r-base
conda install -c conda-forge r-essentials
conda install -c conda-forge r-tidyverse
conda install -c conda-forge r-stringr
conda install -c conda-forge r-gargle
conda install -c conda-forge r-bigrquery
conda activate r
```
   
# Additional Materials

Lots of great info including in-depth SQL training at [https://arcus.github.io/education_modules/example_pathways](https://arcus.github.io/education_modules/example_pathways#:~:text=Big%20data%2C%20big-,questions,-%3A%20Modules)!