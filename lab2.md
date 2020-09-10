# Google Cloud Fundamentals: Getting Started with BigQuery

## Overview
In this lab, you load a web server log into a BigQuery table. After loading the data, you query it using the BigQuery web user interface and the BigQuery CLI.

## Objectives
In this lab, you learn how to perform the following tasks:

- Load data from Cloud Storage into BigQuery.

- Perform a query on the data in BigQuery.


## Task 1: Sign in to the Google Cloud Platform (GCP) Console

### Before you begin
use your Qwicklabs credentials to sign in to Google Cloud Platform Console.

### Activate Google Cloud Shell
Google Cloud Shell is a virtual machine that is loaded with development tools. It offers a persistent 5GB home directory and runs on the Google Cloud. Google Cloud Shell provides command-line access to your GCP resources.

1. In GCP console, on the top right toolbar, click the Open Cloud Shell button.

2. Click `Continue`.
> It takes a few moments to provision and connect to the environment. When you are connected, you are already authenticated, and the project is set to your PROJECT_ID.


### bq command-line tool
The bq command-line tool is a Python-based command-line tool for BigQuery. It comes pre-installed on Cloud Shell.
> Full documentation of bq is available on [Using the bq command-line tool](https://cloud.google.com/bigquery/docs/bq-command-line-tool) .


## Task 2: Load data from Cloud Storage into BigQuery
1. Create a new dataset called logdata
`bq --location=us-central1 mk \
--dataset \
project_id:logdata`

2. Load data from Cloud Storage into a new table called accesslog
`bq load \
--source_format=CSV \
logdata.accesslog \
gs://cloud-training/gcpfci/access_log.csv \
--autodetect`

## Task 3-4: Perform a query on the data using the bq command
query the accesslog table
`bq query "select string_field_10 as request, count(*) as requestcount from logdata.accesslog group by request order by requestcount desc"`

## End your lab
When you have completed your lab, click End Lab. Qwiklabs removes the resources you've used and cleans the account for you.