# Reddit ELT Pipeline

A data pipeline to extract Reddit data from [r/dataengineering](https://www.reddit.com/r/dataengineering/). 

Output is a Google Data Studio report, providing insight into the Data Engineering official subreddit.

## Motivation

Project was based on an interest in Data Engineering and the types of Q&A found on the official subreddit. 

It also provided a good opportunity to develop skills and experience in a range of tools. As such, project is more complex than required, utilising dbt, airflow, docker and cloud based storage.

## Architecture

<img src="https://github.com/ABZ-Aaron/Reddit-API-Pipeline/blob/master/images/workflow.png" width=70% height=70%>

1. Extract data using [Reddit API](https://www.reddit.com/dev/api/)
1. Load into [AWS S3](https://aws.amazon.com/s3/)
1. Copy into [AWS Redshift](https://aws.amazon.com/redshift/)
1. Transform using [dbt](https://www.getdbt.com)
1. Create [PowerBI](https://powerbi.microsoft.com/en-gb/) or [Google Data Studio](https://datastudio.google.com) Dashboard 
1. Orchestrate with [Airflow](https://airflow.apache.org) installed via [Docker](https://www.docker.com)
1. Create AWS resources with [Terraform](https://www.terraform.io)

## Output

[<img src="https://github.com/ABZ-Aaron/Reddit-API-Pipeline/blob/master/images/GDS-Dashboard.png" width=70% height=70%>](https://datastudio.google.com/reporting/632706a4-a7d7-46df-a28d-4a24ab0e8cc4)

* Final output from Google Data Studio. Link [here](https://datastudio.google.com/reporting/632706a4-a7d7-46df-a28d-4a24ab0e8cc4)

## Setup

Follow below steps to setup pipeline. Feel free to make improvements/changes. As AWS offer a free tier, this shouldn't cost you anything unless you amend the pipeline to extract large amounts of data, or keep infrastructure running for 2+ months.

First clone the repository into your home directory and follow the steps.

  ```bash
  git clone https://github.com/ABZ-Aaron/Reddit-API-Pipeline.git
  cd Reddit-API-Pipeline
  ```

1. [Overview](instructions/overvie.md)
1. [Reddit API Configuration](instructions/reddit.md)
1. [AWS Account](instructions/aws.md)
1. [Infrastructure with Terraform](instructions/setup_infrastructure.md)
1. [Configuration Details](instructions/config.md)
1. [Docker & Airflow](instructions/docker_airflow.md) 
1. [dbt](instructions/dbt.md)
1. [Dashboard](instructions/visualisation.md)
1. [Final Notes & Termination](instructions/terminate.md)

## Improvements

There are improvements that can be made here which I'll implement at a later point.

* Improve Airflow & Docker process

  Files used were pulled from online with very few changes made. These could be simplified and/or refactored with a real production environment in mind.

* Improve workflow

  The pipeline saves file down with naming format `YYYYMMDD`. The S3 load script finds this file and uploads to S3. The Redshift script copies file data from S3 into Redshift. It may be better to copy all existing S3 files into Redshift for each DAG run.

* Testing

  Unit and Integration tests could be implemented throughout the process to ensure data quality.

* Simplify Process

  The use of Airflow and dbt is overkill. Alternative ways to run this pipeline could be with Cron for orchestration and PostgreSQL or SQLite for storage.

* Stream over Batch Processing

  If we want our Dashboard to always be up-to-date, we could benefit from something like Kafka.







