Custom ELT Project:

This repository contains a custom Extract, Load, Transform (ELT) project that utilizes Docker and PostgreSQL to demonstrate a simple ELT process.

Repository Structure:

docker-compose.yaml: This file contains the configuration for Docker Compose, which is used to orchestrate multiple Docker containers. It defines three services:

source_postgres: The source PostgreSQL database.

destination_postgres: The destination PostgreSQL database.

elt_script: The service that runs the ELT script.

elt_script/Dockerfile: This Dockerfile sets up a Python environment and installs the PostgreSQL client. It also copies the ELT script into the container and sets it as the default command.

elt_script/elt_script.py: This Python script performs the ELT process. It waits for the source PostgreSQL database to become available, then dumps its data to a SQL file and loads this data into the destination PostgreSQL database.

source_db_init/init.sql: This SQL script initializes the source database with sample data. It creates tables for users, films, film categories, actors, and film actors, and inserts sample data into these tables.

How It Works

Docker Compose: Using the docker-compose.yaml file, three Docker containers are spun up:

A source PostgreSQL database with sample data.

A destination PostgreSQL database.

A Python environment that runs the ELT script.

ELT Process: The elt_script.py waits for the source PostgreSQL database to become available. Once it's available, the script uses pg_dump to dump the source database to a SQL file. Then, it uses psql to load this SQL file into the destination PostgreSQL database.

Database Initialization: The init.sql script initializes the source database with sample data. It creates several tables and populates them with sample data.

CRON Job Implementation

In this branch, a CRON job has been implemented to automate the ELT process. The CRON job is scheduled to run the ELT script at specified intervals, ensuring that the data in the destination PostgreSQL database is regularly updated with the latest data from the source database.

To configure the CRON job:

Currently, the CRON job is setup to run every day at 3am.

You can adjust the time as needed within the Dockerfile found in the elt_script folder.

