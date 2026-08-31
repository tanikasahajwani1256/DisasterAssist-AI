# DisasterAssist AI
## Intelligent Disaster Response & Resource Management Platform

![Python](https://img.shields.io/badge/Python-3.10-blue)
![Machine Learning](https://img.shields.io/badge/Machine-Learning-green)
![GeoPandas](https://img.shields.io/badge/GeoPandas-GIS-success)
![OpenStreetMap](https://img.shields.io/badge/OpenStreetMap-Infrastructure-orange)
![WorldPop](https://img.shields.io/badge/WorldPop-Population-purple)
![USGS](https://img.shields.io/badge/USGS-Earthquake-red)
![GDACS](https://img.shields.io/badge/GDACS-MultiHazard-yellow)
![OpenMeteo](https://img.shields.io/badge/OpenMeteo-Weather-blueviolet)

---

# Project Overview

Natural disasters such as earthquakes, floods, cyclones, droughts, and wildfires cause significant damage to human life, infrastructure, and the economy. During such events, emergency response agencies often face two major challenges:

- Estimating the expected severity and impact of a disaster in real time.
- Allocating limited rescue and relief resources efficiently.

Traditional disaster response systems rely heavily on manual assessment, delayed reports, and fragmented information from multiple agencies. This often results in delayed decision-making, inefficient resource utilization, and increased human and economic losses.

This project addresses these challenges by developing an **DisasterAssist-AI** that integrates multiple real-world geospatial datasets, weather information, population exposure, and infrastructure availability into a unified machine learning pipeline capable of estimating disaster impact and supporting future intelligent resource allocation.

Unlike traditional machine learning projects that rely on a single dataset, this project constructs its own disaster intelligence dataset by integrating multiple heterogeneous data sources through a carefully designed data engineering pipeline.

The final objective is to build a scalable disaster intelligence framework that can assist disaster management authorities by providing reliable impact predictions and, in future phases, optimize the allocation of emergency resources.

---

# Problem Statement

Effective disaster response depends on accurate situational awareness immediately after a disaster occurs. However, disaster information is typically distributed across multiple independent sources:

- Earthquake information from geological agencies
- Multi-hazard disaster alerts
- Population distribution
- Historical weather conditions
- Nearby critical infrastructure

Since these datasets exist independently, it becomes difficult to estimate the actual impact of a disaster using only one source.

# Project Objectives

The primary objectives of this project are:

- Collect historical disaster events from multiple reliable sources.
- Integrate heterogeneous disaster datasets into a unified schema.
- Estimate population exposure around disaster locations.
- Retrieve historical weather conditions during each disaster event.
- Extract nearby critical infrastructure using OpenStreetMap.
- Engineer meaningful spatial and environmental features.
- Build a regression model capable of predicting disaster impact.
- Generate a high-quality machine learning dataset for disaster intelligence.
- Establish a foundation for future AI-driven resource allocation and relief coordination.

---

# Key Contributions

This project introduces several important contributions beyond a standard machine learning workflow.

### Multi-Source Disaster Data Integration

The project integrates multiple independent real-world datasets including:

- USGS Earthquake Catalog
- GDACS Multi-Hazard Disaster Feed
- OpenMeteo Historical Weather API
- WorldPop Population Dataset
- OpenStreetMap Infrastructure Data

into a single machine learning dataset.

---

### Geospatial Feature Engineering

Unlike conventional tabular machine learning projects, this system performs extensive geospatial processing including:

- Geographic coordinate transformations
- Spatial joins
- Population raster analysis
- Infrastructure proximity analysis
- Nearest-neighbor spatial search
- Geographic feature extraction

---

### Offline Infrastructure Extraction Pipeline

Instead of querying the OpenStreetMap Overpass API individually for every disaster event (which is slow and unreliable for thousands of requests), this project implements an offline infrastructure extraction pipeline that:

- Downloads regional OpenStreetMap extracts.
- Extracts hospitals, clinics, schools, and fire stations locally.
- Stores infrastructure in an optimized Parquet dataset.
- Uses KD-Tree spatial indexing for efficient nearest-neighbor queries.

This significantly reduces execution time while improving reliability and scalability.

---

### Machine Learning-Based Disaster Impact Prediction

The project develops a regression model capable of estimating disaster impact using:

- Disaster characteristics
- Population exposure
- Historical weather conditions
- Infrastructure availability

The predicted impact score forms the basis for future intelligent disaster response planning.

---

# Project Scope

The current implementation focuses on the **Impact Prediction** stage of the disaster management lifecycle.

The completed components include:

- Disaster data acquisition
- Multi-source dataset integration
- Population analysis
- Weather retrieval
- Infrastructure extraction
- Feature engineering
- Regression model development
- Impact prediction

The following modules are planned for future development:

- Resource demand estimation
- Relief material allocation
- Medical team deployment
- Shelter recommendation
- Route optimization
- Real-time disaster monitoring dashboard

---

# High-Level System Architecture

The complete project architecture is illustrated below.

```text
                           ┌────────────────────┐
                           │   USGS API         │
                           │ Earthquake Events  │
                           └─────────┬──────────┘
                                     │
                                     ▼

                           earthquake_data.csv

                                     ▲
                                     │

                           ┌─────────┴──────────┐
                           │    GDACS API       │
                           │ Multi-Hazard Feed  │
                           └─────────┬──────────┘
                                     │
                                     ▼

                              gdacs_data.csv

                                     │
                                     ▼

                    Data_Preprocessing.ipynb

                                     │
                                     ▼

                      combined_disasters.csv

                                     │
          ┌──────────────────────────┼──────────────────────────┐
          │                          │                          │
          ▼                          ▼                          ▼

 WorldPop Population          OpenMeteo API          OSM Infrastructure
       Analysis             Historical Weather        Offline Extraction

          │                          │                          │
          ▼                          ▼                          ▼

Population Features       Weather Features      Infrastructure Features

          └──────────────────────────┼──────────────────────────┘
                                     │
                                     ▼

                 Merge_Infrastructure.ipynb

                                     │
                                     ▼

          final_disaster_dataset_with_infrastructure.csv

                                     │
                                     ▼

                Feature_Engineering.ipynb

                                     │
                                     ▼

        final_disaster_dataset_engineered.csv

                                     │
                                     ▼

      ImpactScore_Regression_Model.ipynb

                                     │
                                     ▼

               Trained ML Model (.pkl)

                                     │
                                     ▼

          Future Resource Allocation System
```

---

# Complete Project Workflow

The project follows a sequential data engineering and machine learning pipeline.

```text
Step 1
│
├── Collect Earthquake Events (USGS)

Step 2
│
├── Collect Multi-Hazard Events (GDACS)

Step 3
│
├── Merge Disaster Records

Step 4
│
├── Estimate Population Exposure (WorldPop)

Step 5
│
├── Retrieve Historical Weather (OpenMeteo)

Step 6
│
├── Extract Infrastructure from OpenStreetMap

Step 7
│
├── Query Nearest Infrastructure using KD-Tree

Step 8
│
├── Merge Infrastructure Features

Step 9
│
├── Feature Engineering

Step 10
│
├── Train Impact Score Regression Model

Step 11
│
└── Predict Disaster Impact

Future

Resource Allocation

↓

Relief Coordination

↓

Route Optimization

↓

Disaster Intelligence Dashboard
```

---

# Repository Structure

```text
DisasterAssist-AI/
│
├── api/
│
├── datasets/
│   ├── earthquake_data.csv
│   ├── gdacs_data.csv
│   ├── combined_disasters.csv
│   ├── weather_useful_events.csv
│   ├── useful_disaster_events.csv
│   ├── final_disaster_dataset.csv
│   ├── final_disaster_dataset_with_infrastructure.csv
│   ├── final_disaster_dataset_engineered.csv
│   ├── event_infrastructure_summary.csv
│   ├── india_infrastructure.parquet
│   ├── population_data.tif
│   ├── population_clean.npy
│   ├── osm_regions/
│   ├── shapefiles/
│   └── osm_checkpoints/
│
├── notebooks/
│   ├── USGS_API.ipynb
│   ├── GDACS_API.ipynb
│   ├── OpenMeteo_API.ipynb
│   ├── WorldPop_API.ipynb
│   ├── Data_Preprocessing.ipynb
│   ├── Extract_Infrastructure.ipynb
│   ├── Query_Infrastructure.ipynb
│   ├── Merge_Infrastructure.ipynb
│   ├── Feature_Engineering.ipynb
│   ├── ImpactScore_Regression_Model.ipynb
│
│
├── README.md
│
└── requirements.txt
```

---

# Technology Stack

## Programming Language

- Python 3.10

---

## Data Processing

- Pandas
- NumPy

---

## Geospatial Analysis

- GeoPandas
- Shapely
- Rasterio
- SciPy KD-Tree

---

## Machine Learning

- Scikit-Learn
- XGBoost
- Joblib

---

## External Data Sources

- USGS Earthquake API
- GDACS Disaster Feed
- OpenMeteo Historical Weather API
- WorldPop Population Dataset
- OpenStreetMap (Geofabrik Extracts)

---

## Storage Formats

- CSV
- Parquet
- GeoPackage
- NumPy Arrays
- GeoTIFF
- Pickle Models

---

# End-to-End Data Flow

```text
External APIs
        │
        ▼

Raw Disaster Data

        │
        ▼

Preprocessing

        │
        ▼

Population Analysis

        │
        ▼

Weather Retrieval

        │
        ▼

Infrastructure Extraction

        │
        ▼

Infrastructure Query

        │
        ▼

Dataset Merging

        │
        ▼

Feature Engineering

        │
        ▼

Regression Model

        │
        ▼

Impact Prediction

        │
        ▼

Future Resource Allocation
```

---
# 2. Data Collection Pipeline

The first stage of the project focuses on collecting historical disaster events from multiple authoritative sources. Instead of relying on a single dataset, the system constructs a unified disaster database by integrating earthquake records from the United States Geological Survey (USGS) with multi-hazard disaster alerts from the Global Disaster Alert and Coordination System (GDACS).

These two datasets serve as the foundation for all subsequent preprocessing, population analysis, weather integration, infrastructure extraction, feature engineering, and machine learning tasks.

The overall workflow of the data collection stage is illustrated below.

```text
                 USGS Earthquake API
                         │
                         ▼
              earthquake_data.csv
                         │
                         │
                         │
GDACS Disaster Feed ─────┘
        │
        ▼
   gdacs_data.csv
        │
        ▼
 Data_Preprocessing.ipynb
```

---

# 2.1 USGS_API.ipynb

## Objective

The purpose of this notebook is to collect historical earthquake events affecting the Indian region from the United States Geological Survey (USGS).

The collected earthquake records provide the primary historical disaster data required for model training. Each earthquake event contains geographical coordinates, magnitude, depth, and occurrence time, which are later combined with environmental and demographic information.

---

## Data Source

**Provider**

United States Geological Survey (USGS)

**API**

https://earthquake.usgs.gov/fdsnws/event/1/query

**Response Format**

GeoJSON

---

## Input Parameters

The notebook sends requests to the USGS API using the following parameters.

| Parameter | Value | Description |
|-----------|-------|-------------|
| Start Date | 2000-01-01 | Beginning of historical earthquake records |
| End Date | 2026-12-31 | End date for data collection |
| Minimum Magnitude | 3.5 | Filters out low-magnitude earthquakes |
| Latitude Range | 6° to 38° | Approximate Indian geographical extent |
| Longitude Range | 68° to 98° | Approximate Indian geographical extent |
| Output Format | GeoJSON | Structured JSON response |

---

## Input

```text
USGS Earthquake API
```

No local dataset is required.

---

## Operations Performed

The notebook performs the following sequence of operations.

### Step 1

Send an HTTP request to the USGS Earthquake API using the configured search parameters.

↓

### Step 2

Receive earthquake records in GeoJSON format.

↓

### Step 3

Parse the JSON response.

↓

### Step 4

Extract the following attributes for every earthquake event.

- Magnitude
- Latitude
- Longitude
- Depth
- Event Time
- Event Identifier

↓

### Step 5

Convert timestamps into Python datetime format.

↓

### Step 6

Convert the extracted information into a structured Pandas DataFrame.

↓

### Step 7

Assign a unique project-level `SourceEventID` for every earthquake event.

↓

### Step 8

Perform basic data cleaning.

Operations include:

- Removing duplicate events
- Standardizing column names
- Resetting DataFrame index
- Converting numeric columns to appropriate data types

↓

### Step 9

Export the processed earthquake dataset.

---

## Output Dataset

```text
earthquake_data.csv
```

---

## Output Schema

| Column | Description |
|---------|-------------|
| SourceEventID | Unique project identifier |
| USGSEventID | Original USGS event identifier |
| Magnitude | Earthquake magnitude |
| Latitude | Epicenter latitude |
| Longitude | Epicenter longitude |
| Depth | Depth below Earth's surface (km) |
| Time | Event occurrence timestamp |

---

## Dataset Statistics

Approximate values used in the project.

| Property | Value |
|----------|------|
| Disaster Type | Earthquake |
| Records Collected | ~18,681 |
| Number of Columns | 7 |
| Time Coverage | 2000–2026 |
| Geographic Coverage | India |

---

## Output Produced

```text
earthquake_data.csv

↓

18,681 historical earthquake events
```

---

## Role in Overall Pipeline

The earthquake dataset acts as the primary historical disaster dataset.

It is later combined with GDACS disaster events to create a multi-hazard disaster database.

```text
earthquake_data.csv
        │
        ▼
Data_Preprocessing.ipynb
```

---

# 2.2 GDACS_API.ipynb

## Objective

While the USGS dataset only provides earthquake events, real-world disaster response systems must support multiple disaster types.

The objective of this notebook is therefore to collect multi-hazard disaster alerts from GDACS, enabling the project to include floods, cyclones, droughts, wildfires, volcanoes, and other disaster categories.

This significantly improves the diversity of the machine learning dataset.

---

## Data Source

**Provider**

Global Disaster Alert and Coordination System (GDACS)

**RSS Feed**

https://www.gdacs.org/xml/rss.xml

**Response Format**

RSS XML Feed

---

## Disaster Types Collected

The notebook extracts multiple disaster categories.

- Earthquake
- Flood
- Cyclone
- Drought
- Wildfire
- Volcano

---

## Input

```text
GDACS RSS Feed
```

No local dataset is required.

---

## Operations Performed

The notebook performs the following workflow.

### Step 1

Connect to the GDACS RSS feed.

↓

### Step 2

Download the latest disaster alerts.

↓

### Step 3

Parse the XML feed.

↓

### Step 4

Extract disaster metadata.

Information collected includes:

- Disaster title
- Disaster type
- Alert level
- Severity
- Country
- Latitude
- Longitude
- Published time
- Summary
- Reference URL

↓

### Step 5

Convert GDACS disaster codes into human-readable disaster categories.

Example:

```text
EQ → Earthquake

FL → Flood

TC → Cyclone

DR → Drought

WF → Wildfire

VO → Volcano
```

↓

### Step 6

Convert the extracted information into a structured Pandas DataFrame.

↓

### Step 7

Assign a unique project-level identifier.

↓

### Step 8

Perform data cleaning.

Operations include:

- Duplicate removal
- Missing value handling
- Timestamp formatting
- Column standardization

↓

### Step 9

Export the processed dataset.

---

## Output Dataset

```text
gdacs_data.csv
```

---

## Output Schema

| Column | Description |
|---------|-------------|
| GDACSEventID | GDACS disaster identifier |
| DisasterType | Disaster category |
| AlertLevel | GDACS alert level |
| Severity | Disaster severity |
| Country | Country affected |
| Latitude | Disaster latitude |
| Longitude | Disaster longitude |
| Title | Disaster title |
| Published | Publication timestamp |
| Link | GDACS event URL |
| Summary | Disaster description |

---

## Dataset Statistics

| Property | Value |
|----------|------|
| Disaster Categories | 6+ |
| Source | GDACS RSS Feed |
| Response Format | XML |
| Output Columns | 11 |

---

## Output Produced

```text
gdacs_data.csv

↓

Multi-hazard disaster dataset
```

---

## Role in Overall Pipeline

The GDACS dataset complements the earthquake dataset collected from USGS.

Instead of training only on earthquakes, the final disaster database includes multiple disaster categories.

```text
USGS_API.ipynb
        │
        ├──────────────┐
        │              │
        ▼              ▼
earthquake_data.csv    gdacs_data.csv
        │              │
        └──────┬───────┘
               ▼
Data_Preprocessing.ipynb
```

---

## Summary

At the completion of the data collection stage, two standardized datasets are available.

| Notebook | Output |
|----------|--------|
| USGS_API.ipynb | earthquake_data.csv |
| GDACS_API.ipynb | gdacs_data.csv |

These datasets provide the historical disaster information required for the next stage of the pipeline, where they are merged into a unified multi-hazard disaster dataset using **Data_Preprocessing.ipynb**.


# 2.3 Data_Preprocessing.ipynb

## Objective

The purpose of this notebook is to construct the final machine learning dataset by integrating disaster information, historical weather observations, and population exposure data into a single structured dataset.

Unlike the previous notebooks, this notebook does not collect new information from external APIs. Instead, it performs extensive preprocessing, validation, merging, filtering, and feature generation to produce a clean dataset suitable for regression model training.

The output of this notebook serves as the direct input to the **ImpactScore Regression Model**.

---

## Position in Project Workflow

```text
earthquake_data.csv
        │
        │
weather_useful_events.csv
        │
        │
WorldPop Population Raster
        │
        ▼
Data_Preprocessing.ipynb
        │
        ▼
final_disaster_dataset.csv
        │
        ▼
ImpactScore_Regression_Model.ipynb
```

---

## Input Files

The notebook requires the following datasets.

| Input File | Source | Purpose |
|------------|--------|----------|
| earthquake_data.csv | USGS_API.ipynb | Historical earthquake events |
| weather_useful_events.csv | OpenMeteo_API.ipynb | Historical weather conditions |
| worldpop_india_2020.tif | WorldPop_API.ipynb | Population raster |
| worldpop_selected_metadata.json | WorldPop_API.ipynb | Raster metadata |

---

## Input Features

The preprocessing pipeline begins with disaster information collected from USGS and weather observations obtained from Open-Meteo.

The primary attributes include:

```text
SourceEventID
Magnitude
Latitude
Longitude
Depth
Time
Temperature
Humidity
Rainfall
WindSpeed
```

Population information is then extracted from the WorldPop raster using each disaster location.

---

## Processing Pipeline

The notebook performs the following sequence of operations.

### Step 1 — Validate Required Inputs

Before processing begins, all required datasets are verified.

Validation includes:

- File existence
- Directory validation
- Required metadata availability
- Raster availability

If any required dataset is missing, the notebook terminates with an informative error message.

---

### Step 2 — Load Disaster Dataset

Historical earthquake events are loaded into a Pandas DataFrame.

Operations performed include:

- Parsing timestamps
- Removing duplicate records
- Standardizing column names
- Converting numeric columns
- Resetting DataFrame index

---

### Step 3 — Load Historical Weather Dataset

Historical weather observations are loaded.

Collected weather variables include:

```text
Temperature

Humidity

Rainfall

WindSpeed
```

The weather data is matched to disaster events using the common event identifier.

---

### Step 4 — Read WorldPop Population Raster

The notebook opens the WorldPop GeoTIFF raster.

For every disaster event:

- Latitude is converted into raster coordinates.
- Longitude is converted into raster coordinates.
- Raster cell values are extracted.
- Population exposure is computed.

The notebook also reads metadata describing:

- Country
- Year
- Coordinate Reference System
- Raster dimensions
- Pixel resolution

---

### Step 5 — Calculate Population Exposure

For every disaster location, the notebook estimates:

```text
Population

PopulationDensity
```

These features describe the potential number of people exposed to the disaster.

Events located outside the raster extent or containing invalid population values are removed.

---

### Step 6 — Merge Weather Information

Weather observations are merged with disaster records.

The merged dataset now contains:

- Disaster information
- Geographic coordinates
- Weather variables
- Population exposure

---

### Step 7 — Feature Engineering

Additional predictive variables are generated.

The notebook derives:

```text
Severity

ImpactScore
```

Severity is assigned using disaster characteristics.

ImpactScore is computed using multiple contributing factors including:

- Magnitude
- Population
- Population Density
- Rainfall
- Wind Speed

These engineered features become the target variables used during regression model development.

---

### Step 8 — Final Dataset Validation

Before exporting the dataset, the notebook performs several validation checks.

These include:

- Missing value detection
- Duplicate removal
- Numeric type validation
- Coordinate validation
- Population validation
- Weather validation

---

### Step 9 — Export Dataset

The processed dataset is exported as

```text
final_disaster_dataset.csv
```

---

## Output Dataset

```text
final_disaster_dataset.csv
```

---

## Output Features

The exported dataset contains information describing:

### Disaster Information

```text
SourceEventID

DisasterType

Magnitude

Depth

Time
```

### Geographic Information

```text
Latitude

Longitude
```

### Weather Features

```text
Temperature

Humidity

Rainfall

WindSpeed
```

### Population Features

```text
Population

PopulationDensity
```

### Engineered Features

```text
Severity

ImpactScore
```

---

## Role in Machine Learning Pipeline

The generated dataset represents the final feature matrix used for regression model training.

```text
Raw Disaster Data
        │
Weather Data
        │
Population Data
        │
        ▼
Data_Preprocessing.ipynb
        │
        ▼
final_disaster_dataset.csv
        │
        ▼
ImpactScore Regression Model
```

---

# 2.4 WorldPop_API.ipynb

## Objective

The purpose of this notebook is to acquire and prepare high-resolution population data for India using the WorldPop project.

Rather than storing population as simple tabular data, WorldPop provides a raster where every pixel represents the estimated number of people living within that geographic cell.

The notebook prepares this raster for rapid lookup during disaster preprocessing.

---

## Data Source

Provider

```text
WorldPop
```

API

```text
https://hub.worldpop.org
```

Dataset

```text
India Population Raster
```

Coordinate Reference System

```text
EPSG:4326
```

---

## Outputs Produced

The notebook generates several reusable files.

```text
worldpop_metadata.csv

worldpop_selected_metadata.json

worldpop_india_2020.tif

worldpop_population.npy
```

These outputs are later consumed by Data_Preprocessing.ipynb.

---

## Processing Workflow

```text
WorldPop API

        │

        ▼

Metadata Download

        │

        ▼

Select India Dataset

        │

        ▼

Download Population Raster

        │

        ▼

Validate Raster

        │

        ▼

Create Clean NumPy Array

        │

        ▼

Save Metadata

        │

        ▼

Ready for Population Lookup
```

---

## Step-by-Step Operations

### Step 1 — Retrieve Metadata

The notebook first attempts to connect to the WorldPop REST API.

The metadata catalogue contains information including:

- Country
- Dataset name
- Available years
- Raster URL
- Coordinate system

If the API is temporarily unavailable, the notebook falls back to the locally cached metadata file, ensuring reproducibility.

---

### Step 2 — Select India Dataset

The metadata catalogue is filtered to identify the required India population raster.

Selection criteria include:

- Country: India
- Population dataset
- Desired reference year

The selected metadata is saved for downstream processing.

---

### Step 3 — Download Population Raster

The selected GeoTIFF raster is downloaded.

The raster contains gridded estimates of the population distribution across India.

Each raster cell corresponds to a geographic location and stores the estimated number of residents.

---

### Step 4 — Validate Raster

After downloading, the notebook validates:

- Raster dimensions
- Coordinate Reference System
- Spatial bounds
- Resolution
- NoData values

This ensures the raster can be safely queried during preprocessing.

---

### Step 5 — Convert Raster to NumPy

To improve lookup performance, the raster is converted into a clean NumPy array.

Benefits include:

- Faster coordinate lookup
- Lower repeated disk access
- Efficient population extraction
- Simplified downstream computations

---

### Step 6 — Save Metadata

The notebook exports metadata describing:

- Country
- Dataset year
- Raster dimensions
- CRS
- Bounds
- Resolution

This metadata is later reused by the preprocessing notebook.

---

### Step 7 — Validate Population Lookup

A helper function performs coordinate-based lookup.

Given:

```text
Latitude

Longitude
```

the function:

1. Converts coordinates into raster indices.

2. Checks raster bounds.

3. Returns the corresponding population value.

4. Handles NoData pixels safely.

This validation confirms that population extraction works correctly before integrating the raster into the machine learning pipeline.

---

## Generated Files

| Output | Purpose |
|---------|---------|
| worldpop_metadata.csv | Complete metadata catalogue |
| worldpop_selected_metadata.json | Selected India dataset information |
| worldpop_india_2020.tif | Population raster |
| worldpop_population.npy | Optimized NumPy array |

---

## Role in Overall Pipeline

WorldPop provides demographic exposure information that cannot be obtained from disaster APIs alone.

The generated raster products are consumed directly by the preprocessing stage.

```text
WorldPop API

      │

      ▼

Population Raster

      │

      ▼

Data_Preprocessing.ipynb

      │

      ▼

Population

Population Density

      │

      ▼

Final Disaster Dataset
```

---

## Summary

The WorldPop notebook transforms raw population raster data into optimized geospatial resources suitable for machine learning.

Unlike traditional tabular datasets, the raster enables population estimation at any geographic coordinate, allowing every disaster event to be enriched with population exposure metrics. These features play a significant role in estimating disaster severity and predicting the overall impact score during model training.


# 2.5 OpenMeteo_API.ipynb

## Objective

The purpose of this notebook is to enrich every useful disaster event with the historical weather conditions that existed at the disaster location when the event occurred.

Unlike conventional weather datasets that provide observations for fixed meteorological stations, this notebook retrieves location-specific historical weather information directly from the Open-Meteo Archive API using the exact geographic coordinates and timestamp of each disaster.

The generated weather attributes become important predictive variables for the machine learning model, since rainfall, humidity, temperature, and wind speed significantly influence disaster severity and overall impact.

---

## Position in Project Workflow

```text
Useful Disaster Events
(from Data_Preprocessing filtering)

            │

            ▼

OpenMeteo_API.ipynb

            │

            ▼

Historical Weather Collection

            │

            ▼

weather_useful_events.csv

            │

            ▼

Final Dataset Construction
```

---

# Data Source

Provider

```text
Open-Meteo Historical Weather API
```

Dataset

```text
Historical Archive API
```

Coverage

```text
Worldwide
```

Coordinate System

```text
EPSG:4326 (Latitude / Longitude)
```

---

# Purpose

This notebook retrieves historical weather observations corresponding to every disaster event.

Instead of downloading an entire country's weather history, the notebook requests weather only for disaster locations, making the data collection process significantly more efficient.

For every disaster event, the notebook retrieves weather conditions nearest to the disaster occurrence time.

---

# Input Files

The notebook consumes the filtered disaster dataset generated during preprocessing.

Input file

```text
useful_disaster_events.csv
```

(The notebook reads the disaster dataset produced by the previous preprocessing stage.)

---

# Input Parameters

For every disaster event, the following information is supplied to the Open-Meteo Archive API.

```text
Latitude

Longitude

Event Time
```

These three parameters uniquely determine the weather conditions associated with the disaster.

---

# Weather Variables Retrieved

The notebook collects four environmental variables.

```text
Temperature

Relative Humidity

Rainfall

Wind Speed
```

These variables are later incorporated into the machine learning feature set.

---

# Processing Workflow

```text
Useful Disaster Events

        │

        ▼

Read Disaster Dataset

        │

        ▼

Validate Coordinates

        │

        ▼

Build OpenMeteo API Request

        │

        ▼

Request Historical Weather

        │

        ▼

Parse Hourly Response

        │

        ▼

Find Weather Closest
to Disaster Time

        │

        ▼

Extract Weather Variables

        │

        ▼

Checkpoint Save

        │

        ▼

weather_useful_events.csv
```

---

# Detailed Processing Steps

## Step 1 — Load Disaster Dataset

The notebook loads the disaster dataset.

Each record contains

```text
SourceEventID

Latitude

Longitude

Time
```

These attributes are required for querying the Open-Meteo Archive API.

---

## Step 2 — Validate Input Dataset

Before any API requests are sent, the notebook validates the input.

Validation includes

- Dataset availability
- Required columns
- Coordinate validity
- Timestamp availability
- Duplicate event IDs

Any invalid records are ignored before processing begins.

---

## Step 3 — Validate Geographic Coordinates

Every disaster coordinate is checked before contacting the API.

Validation includes

- Latitude range

```text
-90° to +90°
```

- Longitude range

```text
-180° to +180°
```

Events with invalid coordinates are skipped.

---

## Step 4 — Build Archive API Request

For every disaster, the notebook constructs a historical weather request.

The request contains

```text
Latitude

Longitude

Start Date

End Date

Hourly Variables
```

Hourly variables requested include

```text
temperature_2m

relative_humidity_2m

precipitation

wind_speed_10m
```

---

## Step 5 — Request Historical Weather

The notebook sends an HTTP request to the Open-Meteo Historical Archive API.

The returned JSON contains hourly observations covering the requested date.

The notebook automatically retries failed requests when temporary connection issues occur.

---

## Step 6 — Parse Hourly Weather

The JSON response is parsed into a structured DataFrame.

Hourly observations include

```text
Time

Temperature

Humidity

Rainfall

Wind Speed
```

---

## Step 7 — Match Disaster Time

A disaster rarely occurs exactly on an hourly timestamp.

Therefore, the notebook identifies the weather observation whose timestamp is nearest to the disaster occurrence time.

This ensures that the collected weather conditions closely represent the environmental conditions present during the disaster.

---

## Step 8 — Extract Required Variables

Only four variables are retained.

```text
Temperature

Humidity

Rainfall

Wind Speed
```

The remaining API response fields are discarded.

---

## Step 9 — Checkpointing

The notebook supports automatic checkpointing.

Already processed disaster events are detected using

```text
SourceEventID
```

When execution resumes after interruption, previously completed events are skipped automatically.

Benefits include

- Faster reruns
- Crash recovery
- Reduced API usage

---

## Step 10 — Final Validation

The completed weather dataset is validated.

Checks include

- Missing values
- Duplicate events
- Numeric data types
- Weather range validation

The notebook also generates summary statistics describing the collected weather variables.

---

## Step 11 — Exploratory Visualization

Several quality assurance plots are generated.

These include

### Temperature

Line plot showing historical temperature values.

### Rainfall

Bar chart illustrating precipitation observations.

### Relative Humidity

Time-series visualization.

### Wind Speed

Time-series visualization.

These plots help verify that the downloaded weather data appears realistic before it is merged into the machine learning dataset.

---

## Step 12 — Export Dataset

The final weather dataset is saved as

```text
weather_useful_events.csv
```

---

# Output File

```text
weather_useful_events.csv
```

---

# Output Columns

The generated dataset contains

```text
SourceEventID

Latitude

Longitude

EventTime

WeatherTime

Temperature

Humidity

Rainfall

WindSpeed
```

---

# Number of Records

One weather record is generated for every useful disaster event.

Dataset size

```text
≈ 2,374 weather observations
```

(one record corresponding to each filtered disaster event.)

---

# Validation Performed

The notebook performs multiple validation steps before exporting.

These include

✓ Input dataset validation

✓ Coordinate validation

✓ Timestamp validation

✓ Missing value detection

✓ Duplicate event detection

✓ Numeric type validation

✓ Weather range verification

✓ Checkpoint verification

---

# Generated Visualizations

The notebook creates exploratory plots for

```text
Temperature

Humidity

Rainfall

Wind Speed
```

These plots are intended for quality assurance rather than model training.

---

# Output Usage

The generated weather dataset is consumed by

```text
Data_Preprocessing.ipynb
```

where it is merged with

- Disaster events
- Population exposure
- Infrastructure information

to produce the final machine learning dataset.

---

# Role in the Overall Pipeline

```text
USGS Earthquake Data

            │

GDACS Disaster Data

            │

Useful Disaster Events

            │

            ▼

OpenMeteo_API.ipynb

            │

            ▼

weather_useful_events.csv

            │

            ▼

Data_Preprocessing.ipynb

            │

            ▼

Final Disaster Dataset

            │

            ▼

Regression Model Training
```

---

# Summary

The OpenMeteo_API notebook is responsible for enriching every disaster event with historical environmental conditions.

By retrieving weather observations specific to the disaster location and occurrence time, the notebook provides valuable meteorological features—including temperature, humidity, rainfall, and wind speed—that improve the predictive capability of the disaster impact model.

The notebook also incorporates robust validation, automatic checkpointing, visualization, and export functionality, making it a reliable component of the overall data engineering pipeline.

---

# 2.6 Extract_Infrastructure.ipynb

## Objective

The objective of this notebook is to build a nationwide infrastructure database from OpenStreetMap (OSM) that can later be used to enrich every disaster event with nearby critical infrastructure information.

Instead of querying the OpenStreetMap Overpass API for every disaster event (which is slow, rate-limited, and unreliable for thousands of requests), this notebook performs a one-time extraction from downloaded regional OSM extracts. The extracted infrastructure is stored locally and reused throughout the project.

This offline approach significantly improves scalability, reproducibility, and processing speed.

---

# Position in Project Workflow

```text
Regional OpenStreetMap (.osm.pbf)

            │

            ▼

Extract_Infrastructure.ipynb

            │

            ▼

Critical Infrastructure Extraction

            │

            ▼

india_infrastructure.parquet

            │

            ▼

Query_Infrastructure.ipynb

            │

            ▼

Infrastructure Features
for Every Disaster Event
```

---

# Motivation

Initially, the project attempted to retrieve infrastructure information directly from the OpenStreetMap Overpass API for every disaster event.

This approach resulted in multiple issues:

- API timeout errors
- Request rate limiting
- Long execution times
- Connection failures
- Poor scalability for thousands of events

To overcome these limitations, the workflow was redesigned to use offline OpenStreetMap extracts downloaded from Geofabrik.

Infrastructure is extracted only once and stored locally for repeated use.

---

# Data Source

Provider

```text
Geofabrik OpenStreetMap Downloads
```

Coverage

```text
India
```

Data Format

```text
OpenStreetMap PBF (.osm.pbf)
```

---

# Regional Dataset Organization

Instead of processing the complete India extract at once, the dataset is divided into six geographical regions.

The notebook processes the following regional extracts:

```text
central-zone-260710.osm.pbf

eastern-zone-260710.osm.pbf

north-eastern-zone-260710.osm.pbf

northern-zone-260710.osm.pbf

southern-zone-260710.osm.pbf

western-zone-260710.osm.pbf
```

Processing the country in smaller regional files reduces memory consumption and improves execution stability.

---

# Input Files

The notebook receives the following inputs.

## Regional OpenStreetMap Extracts

```text
6 × .osm.pbf files
```

located inside

```text
datasets/osm_regions/
```

---

# Infrastructure Categories Extracted

Only infrastructure directly relevant to disaster response is retained.

The notebook extracts

```text
Hospitals

Clinics

Schools

Fire Stations
```

using the OpenStreetMap

```text
amenity
```

tag.

Other infrastructure types are ignored to reduce processing time and storage requirements.

---

# Processing Workflow

```text
Regional OSM Files

        │

        ▼

Load One Region

        │

        ▼

Extract Amenities

        │

        ▼

Filter Required Categories

        │

        ▼

Standardize Columns

        │

        ▼

Append Region Name

        │

        ▼

Merge with Previous Regions

        │

        ▼

Repeat for All Six Regions

        │

        ▼

Remove Invalid Records

        │

        ▼

Export Parquet Dataset
```

---

# Detailed Processing Steps

## Step 1 — Locate Regional OSM Files

The notebook scans the project directory for all downloaded regional OpenStreetMap extracts.

Each file is processed independently.

---

## Step 2 — Load One Region

Each regional PBF file is loaded individually using Pyrosm.

Processing one region at a time minimizes memory usage compared to loading the entire country simultaneously.

---

## Step 3 — Read Amenity Layer

The notebook extracts only the OpenStreetMap amenity layer.

Instead of importing every OpenStreetMap object, only features containing the required amenity tags are parsed.

---

## Step 4 — Apply Infrastructure Filter

Only the following amenities are retained.

```text
hospital

clinic

school

fire_station
```

Every other OpenStreetMap object is discarded immediately.

This substantially reduces processing time and memory consumption.

---

## Step 5 — Standardize Attributes

Only the required attributes are preserved.

The resulting dataset contains

```text
Amenity Type

Infrastructure Name

Geometry
```

Additional OpenStreetMap metadata such as tags, identifiers, version history, and edit information are removed.

---

## Step 6 — Add Region Identifier

Each extracted feature receives an additional column recording the source regional extract.

Example

```text
RegionFile

central-zone-260710.osm.pbf
```

This information assists in debugging and validating regional extraction.

---

## Step 7 — Merge Regional Datasets

After processing a regional file, the extracted infrastructure is appended to a master GeoDataFrame.

The process repeats until all six regional extracts have been processed.

---

## Step 8 — Remove Invalid Features

The merged dataset undergoes quality validation.

Invalid records removed include

- Missing geometry
- Empty geometries
- Invalid coordinate locations
- Missing amenity category

---

## Step 9 — Reset Index

After merging all regions, duplicate indexing is removed.

A clean sequential index is generated.

---

## Step 10 — Export Infrastructure Dataset

The final GeoDataFrame is exported as

```text
india_infrastructure.parquet
```

This file becomes the permanent infrastructure database used by the remaining notebooks.

---

# Output File

```text
india_infrastructure.parquet
```

---

# Output Columns

The exported dataset contains

```text
amenity

name

geometry

RegionFile
```

where

**amenity**

```text
Infrastructure category
```

**name**

```text
OpenStreetMap object name
```

**geometry**

```text
Latitude and longitude of the infrastructure
```

**RegionFile**

```text
Regional extract from which the feature originated
```

---

# Dataset Statistics

The final extracted infrastructure database contains

```text
116,701 infrastructure locations
```

Category-wise distribution

| Infrastructure | Count |
|---------------|-------:|
| Hospitals | 55,605 |
| Schools | 37,815 |
| Clinics | 22,553 |
| Fire Stations | 728 |

Total

```text
116,701 records
```

---

# Coordinate Reference System

The infrastructure dataset is stored using

```text
EPSG:4326
```

This coordinate system is later converted to a projected CRS during nearest-neighbour calculations in the next notebook.

---

# Validation Performed

The notebook performs several validation checks before exporting.

These include

✓ Successful loading of all six regional files

✓ Valid geometry verification

✓ Missing geometry detection

✓ Amenity category validation

✓ Duplicate removal (if present)

✓ Output file integrity verification

✓ Record count verification

---

# Advantages of Offline Extraction

Compared with querying the OpenStreetMap API directly, this approach provides

- No API rate limits
- No internet dependency after download
- Faster repeated execution
- Reproducible results
- Stable processing for thousands of disaster events
- Scalable nationwide infrastructure analysis

---

# Output Usage

The generated infrastructure database is consumed by

```text
Query_Infrastructure.ipynb
```

where spatial nearest-neighbour searches are performed to calculate

- Nearest hospital distance
- Nearest clinic distance
- Nearest school distance
- Nearest fire station distance
- Infrastructure counts surrounding each disaster event

---

# Role in the Overall Pipeline

```text
Regional OSM Extracts

        │

        ▼

Extract_Infrastructure.ipynb

        │

        ▼

india_infrastructure.parquet

        │

        ▼

Query_Infrastructure.ipynb

        │

        ▼

Infrastructure Features

        │

        ▼

Final Machine Learning Dataset
```

---

# Summary

The **Extract_Infrastructure** notebook is responsible for constructing a reusable nationwide infrastructure database from offline OpenStreetMap regional extracts. By extracting only hospitals, clinics, schools, and fire stations, the notebook reduces storage requirements while retaining infrastructure that is directly relevant to disaster response and resource allocation. The resulting `india_infrastructure.parquet` dataset serves as the foundation for all subsequent geospatial infrastructure analysis in the project.

---

# 2.7 Query_Infrastructure.ipynb

## Objective

The purpose of this notebook is to spatially enrich every disaster event with critical infrastructure information extracted from OpenStreetMap.

Unlike the previous notebook, which focuses on downloading and storing infrastructure data, this notebook performs spatial analysis to determine the availability and accessibility of infrastructure around every disaster location.

Using efficient nearest-neighbour search techniques, the notebook computes the distance to the nearest emergency facilities and counts the number of facilities within the disaster impact radius.

The generated infrastructure features become important predictors for the disaster impact regression model because they describe the emergency response capability surrounding each disaster event.

---

# Position in Project Workflow

```text
OSM Regional Extracts

        │

        ▼

Extract_Infrastructure.ipynb

        │

        ▼

india_infrastructure.parquet

        │

        ▼

Query_Infrastructure.ipynb

        │

        ▼

event_infrastructure_summary.csv

        │

        ▼

Merge_Infrastructure.ipynb

        │

        ▼

final_disaster_dataset_with_infrastructure.csv
```

---

# Objective of Spatial Analysis

Emergency response is influenced not only by disaster characteristics but also by the surrounding infrastructure.

This notebook quantifies infrastructure accessibility by calculating

- Distance to the nearest hospital
- Number of hospitals within 25 km
- Distance to the nearest clinic
- Number of clinics within 25 km
- Distance to the nearest school
- Number of schools within 25 km
- Distance to the nearest fire station
- Number of fire stations within 25 km

These variables provide an estimate of healthcare accessibility, emergency response capability, and potential shelter availability.

---

# Input Files

The notebook consumes two datasets.

## Disaster Dataset

```text
final_disaster_dataset.csv
```

Contains

- SourceEventID
- Latitude
- Longitude
- Disaster information
- Weather variables
- Population variables

---

## Infrastructure Dataset

```text
india_infrastructure.parquet
```

Generated by

```text
OSM_Infrastructure_Extraction.ipynb
```

Contains

- Hospitals
- Clinics
- Schools
- Fire Stations

represented as geographic point geometries.

---

# Input Statistics

Approximate dataset sizes

| Dataset | Records |
|----------|---------:|
| Disaster Events | 2,374 |
| Infrastructure Locations | 116,701 |

---

# Infrastructure Categories Used

Only four categories are analysed.

```text
Hospital

Clinic

School

Fire Station
```

Each category is processed independently.

---

# Search Radius

The notebook considers infrastructure located within

```text
25 km
```

around every disaster event.

This radius approximates the immediate disaster response zone and provides a balance between local accessibility and regional service coverage.

---

# Processing Workflow

```text
Load Disaster Dataset

        │

        ▼

Load Infrastructure Dataset

        │

        ▼

Convert CRS

        │

        ▼

Convert Geometry to Points

        │

        ▼

Split by Infrastructure Type

        │

        ▼

Build KD-Trees

        │

        ▼

Iterate Through Disaster Events

        │

        ▼

Nearest Neighbour Search

        │

        ▼

Count Infrastructure Within 25 km

        │

        ▼

Generate Infrastructure Features

        │

        ▼

event_infrastructure_summary.csv
```

---

# Detailed Processing Steps

## Step 1 — Load Disaster Dataset

The notebook loads the processed disaster dataset.

Each record contains

```text
SourceEventID

Latitude

Longitude

Population

Weather Variables

Impact Features
```

These records represent the disaster events that require infrastructure enrichment.

---

## Step 2 — Load Infrastructure Dataset

The infrastructure database generated in the previous notebook is loaded.

```text
india_infrastructure.parquet
```

contains every extracted

- Hospital
- Clinic
- School
- Fire Station

within India.

---

## Step 3 — Coordinate System Transformation

For accurate distance calculations, both datasets are transformed from

```text
EPSG:4326
```

to

```text
EPSG:3857
```

which represents coordinates in metres.

This allows Euclidean distance calculations to approximate real-world distances.

---

## Step 4 — Geometry Standardization

Although infrastructure was previously converted into representative points, an additional validation step ensures that every geometry is a valid point.

Invalid geometries are removed before spatial indexing.

---

## Step 5 — Infrastructure Classification

The infrastructure dataset is divided into four independent GeoDataFrames.

```text
Hospitals

Clinics

Schools

Fire Stations
```

Each dataset is processed separately.

---

## Step 6 — Build KD-Tree Spatial Indexes

To improve computational efficiency, the notebook builds a SciPy KD-Tree for every infrastructure category.

Four KD-Trees are created.

```text
Hospital KD-Tree

Clinic KD-Tree

School KD-Tree

Fire Station KD-Tree
```

The KD-Tree stores the projected coordinates of every infrastructure location.

---

# Why KD-Tree?

A naïve approach would compare every disaster event against every infrastructure location.

Computational complexity

```text
O(N × M)
```

where

```text
N = Disaster Events

M = Infrastructure Locations
```

With

```text
2,374 disasters

116,701 infrastructure locations
```

this would require hundreds of millions of distance calculations.

Instead, KD-Trees reduce nearest-neighbour searches to approximately

```text
O(log M)
```

per query, allowing the entire notebook to execute within seconds.

---

## Step 7 — Iterate Through Disaster Events

The notebook processes every disaster event sequentially.

For each event

```text
Latitude

Longitude
```

are extracted from the projected GeoDataFrame.

---

## Step 8 — Nearest Infrastructure Search

Using the corresponding KD-Tree, the notebook identifies

```text
Nearest Hospital

Nearest Clinic

Nearest School

Nearest Fire Station
```

The Euclidean distance returned by the KD-Tree is converted into kilometres.

---

## Step 9 — Radius-Based Infrastructure Count

After identifying the nearest facility, the notebook searches for all infrastructure locations within

```text
25 km
```

using

```text
query_ball_point()
```

The total number of nearby facilities is calculated independently for each infrastructure category.

---

## Step 10 — Generate Infrastructure Features

For every disaster event, the notebook generates eight infrastructure variables.

```text
NearestHospitalDistanceKm

HospitalCount25Km

NearestClinicDistanceKm

ClinicCount25Km

NearestSchoolDistanceKm

SchoolCount25Km

NearestFireStationDistanceKm

FireStationCount25Km
```

These features describe both accessibility and local infrastructure availability.

---

## Step 11 — Validation

Several quality checks are performed before exporting.

Validation includes

✓ Successful KD-Tree construction

✓ Geometry validation

✓ Missing coordinate detection

✓ Distance calculation verification

✓ Infrastructure count verification

✓ Duplicate SourceEventID detection

✓ Dataset size verification

The notebook also produces descriptive statistics for every generated feature to verify that the resulting distributions are reasonable.

---

## Step 12 — Export Dataset

The generated infrastructure summary is exported as

```text
event_infrastructure_summary.csv
```

One record is produced for every disaster event.

---

# Output Dataset

```text
event_infrastructure_summary.csv
```

---

# Output Schema

| Column | Description |
|---------|-------------|
| SourceEventID | Unique disaster identifier |
| NearestHospitalDistanceKm | Distance to nearest hospital |
| HospitalCount25Km | Hospitals within 25 km |
| NearestClinicDistanceKm | Distance to nearest clinic |
| ClinicCount25Km | Clinics within 25 km |
| NearestSchoolDistanceKm | Distance to nearest school |
| SchoolCount25Km | Schools within 25 km |
| NearestFireStationDistanceKm | Distance to nearest fire station |
| FireStationCount25Km | Fire stations within 25 km |

---

# Generated Infrastructure Features

The notebook produces

## Healthcare Accessibility

```text
NearestHospitalDistanceKm

HospitalCount25Km

NearestClinicDistanceKm

ClinicCount25Km
```

---

## Shelter Availability

```text
NearestSchoolDistanceKm

SchoolCount25Km
```

Schools often serve as temporary evacuation shelters during disaster response.

---

## Emergency Response Capacity

```text
NearestFireStationDistanceKm

FireStationCount25Km
```

These variables estimate the availability of firefighting and rescue resources.

---

# Computational Performance

Using KD-Tree indexing, the notebook processes

```text
2,374 disaster events
```

against

```text
116,701 infrastructure locations
```

efficiently without requiring repeated OpenStreetMap API requests.

This significantly improves runtime compared to querying infrastructure individually for every disaster event.

---

# Advantages of This Approach

Compared with the original online OSM workflow, this notebook provides

- Offline execution
- No dependency on Overpass API
- No API rate limits
- Fast nearest-neighbour queries
- Scalable nationwide processing
- Reproducible infrastructure features
- Efficient memory utilization

---

# Role in Overall Pipeline

```text
Infrastructure Extraction

        │

        ▼

india_infrastructure.parquet

        │

        ▼

Query_Infrastructure.ipynb

        │

        ▼

event_infrastructure_summary.csv

        │

        ▼

Merge_Infrastructure.ipynb

        │

        ▼

Final Machine Learning Dataset
```

---

# Summary

The **Query_Infrastructure** notebook transforms raw infrastructure locations into meaningful spatial features for every disaster event. By leveraging KD-Tree spatial indexing, it efficiently computes nearest-neighbour distances and infrastructure counts within a 25 km radius for hospitals, clinics, schools, and fire stations. The resulting infrastructure summary dataset provides essential indicators of emergency response capability and accessibility, forming a critical component of the final machine learning feature set used for disaster impact prediction.

---

# 2.8 Merge_Infrastructure.ipynb

## Objective

The objective of this notebook is to integrate the infrastructure features generated in the previous spatial analysis stage with the processed disaster dataset.

This notebook performs the final merge between disaster information and infrastructure information using the unique disaster event identifier.

The merged dataset becomes the complete machine learning dataset used for disaster impact prediction.

Unlike previous notebooks that generate intermediate datasets, this notebook creates the final feature-rich dataset containing disaster characteristics, weather conditions, population information, and infrastructure accessibility.

---

# Position in Project Workflow

```text
USGS_API.ipynb
          │
          ▼
Earthquake Dataset

GDACS_API.ipynb
          │
          ▼
Multi-disaster Dataset

OpenMeteo_API.ipynb
          │
          ▼
Historical Weather

WorldPop_API.ipynb
          │
          ▼
Population Exposure

Query_Infrastructure.ipynb
          │
          ▼
Infrastructure Summary

                │
                ▼

Merge_Infrastructure.ipynb

                │
                ▼

final_disaster_dataset.csv

                │
                ▼

Impact_Assessment.ipynb
```

---

# Purpose

Previous notebooks independently generated

- Disaster information
- Weather variables
- Population information
- Infrastructure accessibility

However, machine learning requires all predictor variables to exist within a single tabular dataset.

This notebook combines these independent datasets into one unified machine learning dataset.

---

# Input Files

The notebook reads two datasets.

## Input 1

```text
final_disaster_dataset.csv
```

Generated after

```text
USGS

GDACS

OpenMeteo

WorldPop

Data_Preprocessing
```

Contains

- Disaster attributes
- Weather variables
- Population variables

---

## Input 2

```text
event_infrastructure_summary.csv
```

Generated by

```text
Query_Infrastructure.ipynb
```

Contains

- Hospital accessibility
- Clinic accessibility
- School accessibility
- Fire station accessibility

---

# Input Statistics

Approximate size

| Dataset | Rows |
|----------|------:|
| Disaster Dataset | 2,374 |
| Infrastructure Summary | 2,374 |

Both datasets contain one record for every disaster event.

---

# Primary Merge Key

The merge operation uses

```text
SourceEventID
```

This identifier uniquely represents every disaster event collected throughout the pipeline.

Using a unique identifier guarantees that infrastructure information is attached to the correct disaster event.

---

# Processing Workflow

```text
Load Disaster Dataset

        │

        ▼

Load Infrastructure Dataset

        │

        ▼

Validate Event IDs

        │

        ▼

Merge on SourceEventID

        │

        ▼

Check Missing Infrastructure

        │

        ▼

Validate Row Count

        │

        ▼

Export Final Dataset
```

---

# Detailed Processing Steps

## Step 1 — Load Disaster Dataset

The notebook loads

```text
final_disaster_dataset.csv
```

The dataset already contains

- Disaster type
- Magnitude
- Depth
- Weather
- Population
- Population Density
- Severity
- ImpactScore

---

## Step 2 — Load Infrastructure Summary

The notebook loads

```text
event_infrastructure_summary.csv
```

This dataset contains spatial infrastructure features computed using KD-Tree nearest-neighbour searches.

---

## Step 3 — Verify Dataset Integrity

Before merging, several validation checks are performed.

The notebook verifies

✓ SourceEventID exists

✓ No duplicated event IDs

✓ Equal data types

✓ Expected number of rows

---

## Step 4 — Merge Datasets

A left merge is performed using

```text
SourceEventID
```

Workflow

```text
Disaster Dataset

        +

Infrastructure Dataset

        │

        ▼

Merged Dataset
```

Every disaster record receives its corresponding infrastructure features.

---

## Step 5 — Preserve Disaster Records

A left join is used to guarantee that every disaster event remains in the dataset.

Even if infrastructure information is unavailable for a particular disaster, the disaster event is retained.

---

## Step 6 — Missing Infrastructure Validation

After merging, the notebook checks

```text
Hospital Columns

Clinic Columns

School Columns

Fire Station Columns
```

for missing values.

If any missing values exist, they are reported for further inspection.

---

## Step 7 — Duplicate Validation

The notebook verifies

```text
SourceEventID
```

remains unique after merging.

Duplicate disaster records would indicate an incorrect merge.

---

## Step 8 — Dataset Dimension Verification

The notebook confirms

- Row count remains unchanged

- No disaster event is lost

- Infrastructure columns were successfully added

---

## Step 9 — Final Dataset Inspection

The notebook displays

```text
head()

tail()

shape

columns

info()

describe()
```

to verify the merged dataset.

---

## Step 10 — Export Dataset

The merged dataset is exported as

```text
final_disaster_dataset.csv
```

This becomes the primary dataset used throughout model development.

---

# Output Dataset

```text
final_disaster_dataset.csv
```

---

# Output Features

The final dataset contains information from all previous notebooks.

## Disaster Features

```text
SourceEventID

DisasterType

Magnitude

Depth

Latitude

Longitude

Time
```

---

## Weather Features

```text
Temperature

Humidity

Rainfall

WindSpeed
```

---

## Population Features

```text
Population

PopulationDensity
```

---

## Infrastructure Features

```text
NearestHospitalDistanceKm

HospitalCount25Km

NearestClinicDistanceKm

ClinicCount25Km

NearestSchoolDistanceKm

SchoolCount25Km

NearestFireStationDistanceKm

FireStationCount25Km
```

---

## Target Variables

```text
Severity

ImpactScore
```

---

# Total Features

The exported dataset contains

```text
Disaster Information

+

Weather Variables

+

Population Variables

+

Infrastructure Variables

+

Target Variables
```

forming the complete machine learning dataset.

---

# Validation Performed

The notebook performs

✓ SourceEventID validation

✓ Duplicate detection

✓ Missing value detection

✓ Row count verification

✓ Column verification

✓ Successful merge verification

✓ Dataset export verification

---

# Final Dataset Usage

The generated dataset becomes the direct input for

```text
Impact_Assessment.ipynb
```

where regression models are trained to predict

```text
ImpactScore
```

using all engineered features.

---

# Advantages of Separate Merge Notebook

Separating the merge process into an independent notebook provides several advantages.

- Modular workflow
- Easier debugging
- Independent infrastructure updates
- Independent disaster dataset updates
- Faster experimentation
- Improved reproducibility
- Cleaner pipeline organization

Instead of recomputing infrastructure every time, the infrastructure summary can simply be regenerated and merged again.

---

# Complete Pipeline

```text
USGS_API.ipynb
        │
        ▼
Earthquake Data

GDACS_API.ipynb
        │
        ▼
Multi-disaster Data

Data_Preprocessing.ipynb
        │
        ▼
Filtered Disaster Dataset

OpenMeteo_API.ipynb
        │
        ▼
Weather Features

WorldPop_API.ipynb
        │
        ▼
Population Features

OSM_Infrastructure_Extraction.ipynb
        │
        ▼
india_infrastructure.parquet

Query_Infrastructure.ipynb
        │
        ▼
event_infrastructure_summary.csv

Merge_Infrastructure.ipynb
        │
        ▼
final_disaster_dataset.csv

Impact_Assessment.ipynb
```

---

# Summary

The **Merge_Infrastructure** notebook is the final data integration stage of the preprocessing pipeline. It combines the processed disaster dataset with the infrastructure summary generated through spatial analysis, producing a single feature-rich dataset ready for machine learning. The resulting `final_disaster_dataset.csv` contains disaster characteristics, historical weather, population exposure, and infrastructure accessibility for every disaster event, providing the complete set of predictor variables required for ImpactScore regression modelling.

---

# 2.9 Feature_Engineering.ipynb

## Objective

The purpose of this notebook is to transform the cleaned disaster dataset into a machine-learning-ready dataset by generating additional informative features from the existing variables.

Raw variables collected from multiple sources often represent similar concepts in different forms. Feature engineering combines these variables into more meaningful numerical representations that better capture the overall disaster situation.

Rather than directly using every raw feature independently, this notebook derives higher-level indicators such as overall weather severity and infrastructure accessibility, allowing regression models to learn more effectively.

---

# Position in Project Workflow

```text
USGS_API.ipynb

        │

GDACS_API.ipynb

        │

OpenMeteo_API.ipynb

        │

WorldPop_API.ipynb

        │

Merge_Infrastructure.ipynb

        │

        ▼

final_disaster_dataset.csv

        │

        ▼

Feature_Engineering.ipynb

        │

        ▼

engineered_disaster_dataset.csv

        │

        ▼

Impact_Assessment.ipynb
```

---

# Objective of Feature Engineering

Machine learning models generally perform better when important relationships between variables are explicitly represented.

Instead of allowing the model to discover these relationships entirely on its own, engineered features summarize multiple related variables into a single informative score.

This notebook creates two primary engineered features:

- WeatherScore
- InfrastructureScore

These features provide compact representations of environmental conditions and emergency response capability.

---

# Input Dataset

```text
final_disaster_dataset.csv
```

Generated from

```text
Merge_Infrastructure.ipynb
```

The dataset contains

- Disaster information
- Weather variables
- Population variables
- Infrastructure variables
- ImpactScore
- Severity

---

# Input Variables Used

## Weather Variables

```text
Temperature

Humidity

Rainfall
```

---

## Infrastructure Distance Variables

```text
NearestHospitalDistanceKm

NearestClinicDistanceKm

NearestSchoolDistanceKm

NearestFireStationDistanceKm
```

---

## Infrastructure Count Variables

```text
HospitalCount25Km

ClinicCount25Km

SchoolCount25Km

FireStationCount25Km
```

---

# Processing Workflow

```text
Load Final Dataset

        │

        ▼

Normalize Weather Variables

        │

        ▼

Create WeatherScore

        │

        ▼

Normalize Infrastructure Distances

        │

        ▼

Normalize Infrastructure Counts

        │

        ▼

Create InfrastructureScore

        │

        ▼

Validate Engineered Features

        │

        ▼

Export Engineered Dataset
```

---

# Detailed Processing Steps

## Step 1 — Load Final Dataset

The notebook loads

```text
final_disaster_dataset.csv
```

containing approximately

```text
2,374 disaster events
```

Each row corresponds to one disaster event with all collected attributes.

---

## Step 2 — Normalize Weather Variables

Weather variables have different numerical ranges.

For example

```text
Temperature

Humidity

Rainfall
```

cannot be directly averaged because each variable has different units and scales.

Therefore, Min-Max Normalization is applied.

Normalization transforms each feature into the range

```text
0 → 1
```

using

\[
x'=\frac{x-x_{min}}{x_{max}-x_{min}}
\]

This ensures that no weather variable dominates the engineered score.

---

## Step 3 — Generate WeatherScore

After normalization, the notebook computes

```text
WeatherScore
```

using

\[
WeatherScore=
\frac{
Temperature+
Humidity+
Rainfall
}{3}
\]

The resulting feature summarizes the overall environmental condition surrounding each disaster.

Higher values indicate more severe weather conditions.

---

# WeatherScore Interpretation

Higher values generally correspond to

- High rainfall
- High humidity
- Extreme temperature conditions

Lower values indicate relatively mild weather.

---

## Step 4 — Normalize Infrastructure Distances

Distance variables are normalized independently.

Variables

```text
NearestHospitalDistanceKm

NearestClinicDistanceKm

NearestSchoolDistanceKm

NearestFireStationDistanceKm
```

are scaled into

```text
0 → 1
```

using Min-Max Scaling.

---

## Step 5 — Normalize Infrastructure Counts

Similarly,

```text
HospitalCount25Km

ClinicCount25Km

SchoolCount25Km

FireStationCount25Km
```

are normalized.

This prevents categories with larger numerical counts from dominating the engineered feature.

---

## Step 6 — Generate InfrastructureScore

InfrastructureScore combines

Average Normalized Distance

and

Average Normalized Infrastructure Count

using

\[
InfrastructureScore=
\frac{
AverageDistance+
AverageCount
}{2}
\]

where

AverageDistance

is computed from

```text
NearestHospitalDistanceKm

NearestClinicDistanceKm

NearestSchoolDistanceKm

NearestFireStationDistanceKm
```

and

AverageCount

is computed from

```text
HospitalCount25Km

ClinicCount25Km

SchoolCount25Km

FireStationCount25Km
```

---

# Interpretation

InfrastructureScore summarizes the accessibility and availability of emergency facilities surrounding a disaster.

It combines

- proximity to emergency infrastructure

and

- local infrastructure density

into one numerical feature.

---

# Why Normalize?

Without normalization

Example

```text
Nearest Hospital

150 km

Hospital Count

12
```

The distance variable would dominate due to its larger numerical magnitude.

Normalization ensures equal contribution from every feature.

---

# Validation

After generating engineered features, the notebook performs

```text
describe()
```

for

```text
WeatherScore

InfrastructureScore
```

This confirms

✓ Valid ranges

✓ No missing values

✓ Reasonable distributions

---

# Output Dataset

The engineered dataset is exported as

```text
engineered_disaster_dataset.csv
```

---

# Newly Generated Features

| Feature | Description |
|----------|-------------|
| WeatherScore | Combined weather severity indicator |
| InfrastructureScore | Combined infrastructure accessibility indicator |

---

# Final Dataset Contents

The exported dataset contains

Original Disaster Features

+

Weather Variables

+

Population Variables

+

Infrastructure Variables

+

WeatherScore

+

InfrastructureScore

+

Target Variables

---

# Advantages

Feature engineering provides

- Reduced feature redundancy

- Better numerical stability

- Faster model convergence

- Improved interpretability

- Compact representation of environmental conditions

- Compact representation of infrastructure accessibility

---

# Computational Complexity

The notebook performs

- Min-Max Scaling

- Column-wise averaging

These are vectorized Pandas and Scikit-learn operations with linear complexity

```text
O(N)
```

where

```text
N = Number of disaster events
```

making execution nearly instantaneous.

---

# Output Usage

The generated dataset becomes the direct input to

```text
Impact_Assessment.ipynb
```

where regression models learn the relationship between engineered features and disaster impact.

---

# Role in Overall Pipeline

```text
Merge_Infrastructure.ipynb

        │

        ▼

final_disaster_dataset.csv

        │

        ▼

Feature_Engineering.ipynb

        │

        ▼

engineered_disaster_dataset.csv

        │

        ▼

Impact_Assessment.ipynb
```

---

# Summary

The **Feature_Engineering** notebook enhances the merged disaster dataset by creating higher-level predictors from existing variables. Weather-related attributes are combined into a **WeatherScore**, while infrastructure proximity and availability are summarized through an **InfrastructureScore** after Min-Max normalization. These engineered features improve the quality of the machine learning input data, reduce feature redundancy, and provide more meaningful representations of environmental severity and emergency response capability for disaster impact prediction.

---

# 2.10 ImpactScore_Regression_Model.ipynb

## Objective

The **ImpactScore_Regression_Model** notebook represents the final stage of the machine learning pipeline. Its objective is to train, evaluate, and compare multiple regression algorithms capable of predicting the **ImpactScore** of a disaster using the engineered dataset created throughout the previous stages of the project.

Unlike the earlier notebooks, which focus on data acquisition, preprocessing, geospatial analysis, and feature engineering, this notebook transforms the prepared dataset into a predictive model that can estimate disaster impact for previously unseen events.

The trained model forms the foundation for the future **DisasterAssist-AI**, where predicted impact scores will guide emergency resource allocation, relief planning, and decision support. This follows the intended project workflow of using disaster characteristics, weather, population, and infrastructure to estimate disaster impact and subsequently support resource planning. 

---

# Position in Project Workflow

```text
USGS_API.ipynb

        │

GDACS_API.ipynb

        │

WorldPop_API.ipynb

        │

OpenMeteo_API.ipynb

        │

OSM_Infrastructure_Extraction.ipynb

        │

Query_Infrastructure.ipynb

        │

Merge_Infrastructure.ipynb

        │

Feature_Engineering.ipynb

        │

        ▼

engineered_disaster_dataset.csv

        │

        ▼

ImpactScore_Regression_Model.ipynb

        │

        ▼

Trained Regression Model (.pkl)

        │

        ▼

Future Resource Allocation System
```

---

# Objective of Regression Modeling

The purpose of regression modeling is to estimate the expected disaster impact using historical observations.

Instead of manually estimating disaster severity every time a new disaster occurs, the trained model learns the relationship between disaster characteristics and the calculated ImpactScore.

After deployment, only the input features need to be supplied, and the model predicts the expected impact automatically.

---

# Machine Learning Problem

Problem Type

```text
Supervised Machine Learning
```

Learning Category

```text
Regression
```

Prediction Target

```text
ImpactScore
```

---

# Input Dataset

The notebook reads

```text
engineered_disaster_dataset.csv
```

generated by

```text
Feature_Engineering.ipynb
```

This dataset already contains

- Disaster information
- Weather variables
- Population variables
- Infrastructure variables
- Engineered features
- Target variable

---

# Input Features

The regression model uses multiple predictor variables describing different aspects of each disaster.

These include

## Disaster Features

```text
DisasterType

Magnitude

Depth

Latitude

Longitude
```

---

## Weather Features

```text
Temperature

Humidity

Rainfall

WindSpeed

WeatherScore
```

---

## Population Features

```text
Population

PopulationDensity
```

---

## Infrastructure Features

```text
NearestHospitalDistanceKm

HospitalCount25Km

NearestClinicDistanceKm

ClinicCount25Km

NearestSchoolDistanceKm

SchoolCount25Km

NearestFireStationDistanceKm

FireStationCount25Km

InfrastructureScore
```

---

## Target Variable

```text
ImpactScore
```

This numerical score represents the estimated severity and overall impact of a disaster event.

---

# Processing Workflow

```text
Load Engineered Dataset

        │

        ▼

Data Inspection

        │

        ▼

Missing Value Validation

        │

        ▼

Feature Selection

        │

        ▼

Target Selection

        │

        ▼

Train-Test Split

        │

        ▼

Train Regression Models

        │

        ▼

Predict Test Dataset

        │

        ▼

Model Evaluation

        │

        ▼

Performance Comparison

        │

        ▼

Feature Importance

        │

        ▼

Save Best Model
```

---

# Detailed Processing Steps

## Step 1 — Load Engineered Dataset

The notebook imports

```text
engineered_disaster_dataset.csv
```

containing all engineered predictor variables and the ImpactScore target.

---

## Step 2 — Dataset Inspection

Before training begins, the notebook examines

- Dataset dimensions
- Column names
- Data types
- Missing values
- Summary statistics

This ensures that the dataset is suitable for regression.

---

## Step 3 — Missing Value Validation

The notebook verifies that

- No missing predictor values remain.
- Target values are complete.
- Numeric columns contain valid data types.

If missing values exist, appropriate preprocessing is applied before training.

---

## Step 4 — Feature Selection

Independent variables (X) are selected by excluding identifier columns and the target variable.

The remaining numerical and encoded categorical variables become model inputs.

---

## Step 5 — Target Variable Selection

The dependent variable (y) is

```text
ImpactScore
```

The regression model learns the relationship between the selected features and this target.

---

## Step 6 — Train-Test Split

The dataset is divided into

```text
Training Set

80%
```

and

```text
Testing Set

20%
```

The random split ensures unbiased evaluation of model performance on unseen data. This follows the project training strategy of using an 80/20 split. :contentReference[oaicite:2]{index=2}

---

## Step 7 — Regression Model Training

Multiple regression algorithms are trained and compared.

Models evaluated include

```text
Linear Regression

Decision Tree Regressor

Random Forest Regressor

Extra Trees Regressor

Gradient Boosting Regressor

XGBoost Regressor
```

Each model is trained using identical training data to enable fair performance comparison.

---

## Step 8 — Prediction

After training, every model predicts

```text
ImpactScore
```

for the testing dataset.

These predictions are compared against the true ImpactScore values.

---

## Step 9 — Model Evaluation

Several regression evaluation metrics are computed.

### Mean Absolute Error (MAE)

Measures the average prediction error.

Lower values indicate better performance.

---

### Mean Squared Error (MSE)

Penalizes larger prediction errors more heavily.

Lower values are preferable.

---

### Root Mean Squared Error (RMSE)

Provides prediction error in the same units as the target variable.

Lower values indicate better predictive accuracy.

---

### Coefficient of Determination (R² Score)

Measures how well the model explains the variance in the target variable.

```text
Higher R² = Better Model
```

---

# Model Comparison

The notebook compares all trained models using identical evaluation metrics.

The comparison identifies

- Most accurate model
- Lowest prediction error
- Best generalization capability

The highest-performing model is selected for deployment.

---

# Feature Importance Analysis

For tree-based algorithms, feature importance scores are calculated.

This analysis identifies which variables contribute most strongly to disaster impact prediction.

Typical influential variables include

- Magnitude
- Population Density
- WeatherScore
- InfrastructureScore
- Rainfall
- Hospital Accessibility

Understanding feature importance improves model interpretability and supports future feature engineering.

---

# Model Persistence

After selecting the best-performing regression model, it is serialized and saved using

```text
Joblib

or

Pickle
```

Example output

```text
models/

impact_score_model.pkl
```

Saving the trained model eliminates the need for retraining during deployment.

---

# Output Files

The notebook produces

```text
impact_score_model.pkl

model_metrics.csv

feature_importance.csv

prediction_results.csv
```

Depending on the selected model, additional visualizations may also be generated.

---

# Generated Outputs

The notebook produces

✓ Predicted Impact Scores

✓ Model Evaluation Metrics

✓ Feature Importance Rankings

✓ Trained Regression Model

✓ Prediction Dataset

---

# Model Evaluation Metrics

The following metrics are reported for every trained model.

| Metric | Interpretation |
|---------|----------------|
| MAE | Lower is better |
| MSE | Lower is better |
| RMSE | Lower is better |
| R² Score | Higher is better |

---

# Advantages of the Regression Pipeline

The implemented machine learning workflow provides

- Automated impact prediction
- Data-driven decision support
- Scalable disaster analysis
- Quantitative model evaluation
- Comparison of multiple algorithms
- Reproducible training pipeline
- Easy deployment using serialized models

---

# Future Integration

The trained regression model will be integrated into the future disaster response system.

When a new disaster occurs, the workflow will be

```text
New Disaster Event

        │

        ▼

Weather Retrieval

        │

        ▼

Population Lookup

        │

        ▼

Infrastructure Query

        │

        ▼

Feature Engineering

        │

        ▼

ImpactScore Prediction

        │

        ▼

Resource Requirement Estimation

        │

        ▼

Relief Allocation

        │

        ▼

Emergency Decision Support
```

---

# Complete Machine Learning Pipeline

```text
Data Collection

        │

        ▼

Data Preprocessing

        │

        ▼

Population Analysis

        │

        ▼

Weather Integration

        │

        ▼

Infrastructure Analysis

        │

        ▼

Feature Engineering

        │

        ▼

Regression Model Training

        │

        ▼

ImpactScore Prediction

        │

        ▼

Future Disaster Resource Allocation
```

---

# Summary

The **ImpactScore_Regression_Model** notebook represents the culmination of the entire AI-based disaster response pipeline. It transforms the fully engineered disaster dataset into a predictive regression model capable of estimating disaster impact using geospatial, demographic, meteorological, and infrastructure-related features. Multiple regression algorithms are trained and evaluated using standard metrics such as MAE, MSE, RMSE, and R² score, allowing the best-performing model to be selected for deployment. The resulting model serves as the predictive engine for the future disaster response system, enabling automated impact estimation and forming the basis for intelligent resource allocation and relief coordination.

# 3. Final Dataset Description

After completing all preprocessing, geospatial processing, infrastructure extraction, weather integration, population estimation, and feature engineering, all information is merged into a single machine-learning dataset.

This dataset serves as the direct input for the regression models used to predict the disaster **ImpactScore**.

---

# Final Dataset

```text
engineered_disaster_dataset.csv
```

Generated by

```text
Feature_Engineering.ipynb
```

Used by

```text
ImpactScore_Regression_Model.ipynb
```

---

# Dataset Overview

| Property | Value |
|-----------|-------|
| Dataset Type | Structured Tabular Dataset |
| Format | CSV |
| Coordinate Reference System | WGS84 (EPSG:4326) |
| Geographic Coverage | India |
| Disaster Types | Earthquake, Flood, Cyclone, Drought |
| Total Records | ~2,374 Disaster Events |
| Total Features | 20+ Features (depends on engineered columns) |
| Target Variable | ImpactScore |

---

# Dataset Schema

The final dataset combines information collected from

- USGS Earthquake API
- GDACS Disaster Feed
- WorldPop Population Dataset
- Open-Meteo Weather API
- OpenStreetMap Infrastructure
- Feature Engineering

Each row represents one disaster event.

---

# Column Descriptions

---

## 1. SourceEventID

Type

```text
Integer
```

Description

Unique identifier assigned to every disaster event.

Purpose

Used only for identification.

Example

```text
1254
```

---

## 2. DisasterType

Type

```text
Categorical
```

Possible Values

```text
Earthquake

Flood

Cyclone

Drought
```

Description

Specifies the category of disaster.

Source

USGS + GDACS

---

## 3. Latitude

Type

```text
Float
```

Unit

```text
Decimal Degrees
```

Description

Latitude coordinate of disaster location.

Example

```text
17.6868
```

---

## 4. Longitude

Type

```text
Float
```

Unit

```text
Decimal Degrees
```

Description

Longitude coordinate of disaster location.

Example

```text
83.2185
```

---

## 5. Magnitude

Type

```text
Float
```

Description

Earthquake magnitude or equivalent disaster intensity.

Higher values indicate stronger disasters.

Example

```text
5.8
```

---

## 6. Depth

Type

```text
Float
```

Unit

```text
Kilometers
```

Description

Depth of earthquake hypocenter.

Applicable mainly for earthquake events.

---

## 7. Time

Type

```text
Datetime
```

Description

Timestamp representing when the disaster occurred.

Used for weather retrieval.

---

## 8. Temperature

Type

```text
Float
```

Unit

```text
°C
```

Source

Open-Meteo

Description

Average temperature during disaster occurrence.

---

## 9. Humidity

Type

```text
Float
```

Unit

```text
%
```

Source

Open-Meteo

Description

Relative humidity at the disaster location.

---

## 10. Rainfall

Type

```text
Float
```

Unit

```text
Millimeters
```

Source

Open-Meteo

Description

Rainfall recorded during the disaster.

Higher rainfall generally indicates increased flood risk.

---

## 11. WindSpeed

Type

```text
Float
```

Unit

```text
km/h
```

Source

Open-Meteo

Description

Wind speed recorded during disaster occurrence.

Important for cyclone analysis.

---

## 12. Population

Type

```text
Float
```

Source

WorldPop

Description

Estimated population affected within the disaster impact radius.

---

## 13. PopulationDensity

Type

```text
Float
```

Unit

```text
Persons / km²
```

Description

Population density around the disaster location.

Higher values indicate greater human exposure.

---

## 14. NearestHospitalDistanceKm

Type

```text
Float
```

Unit

```text
Kilometers
```

Source

OpenStreetMap

Description

Distance from disaster location to the nearest hospital.

---

## 15. HospitalCount25Km

Type

```text
Integer
```

Description

Number of hospitals located within a 25 km radius.

---

## 16. NearestClinicDistanceKm

Type

```text
Float
```

Description

Distance to the nearest clinic.

---

## 17. ClinicCount25Km

Type

```text
Integer
```

Description

Number of clinics within a 25 km radius.

---

## 18. NearestSchoolDistanceKm

Type

```text
Float
```

Description

Distance to the nearest school.

Schools may serve as temporary relief shelters.

---

## 19. SchoolCount25Km

Type

```text
Integer
```

Description

Number of schools located within a 25 km radius.

---

## 20. NearestFireStationDistanceKm

Type

```text
Float
```

Description

Distance to the nearest fire station.

---

## 21. FireStationCount25Km

Type

```text
Integer
```

Description

Number of fire stations located within a 25 km radius.

---

## 22. WeatherScore

Type

```text
Float
```

Generated In

```text
Feature_Engineering.ipynb
```

Description

Engineered feature representing overall weather severity.

Computed from

```text
Temperature

Humidity

Rainfall
```

Purpose

Provides a single numerical representation of weather conditions.

---

## 23. InfrastructureScore

Type

```text
Float
```

Generated In

```text
Feature_Engineering.ipynb
```

Description

Represents the accessibility and availability of emergency infrastructure.

Computed using

```text
Hospital accessibility

Clinic accessibility

School accessibility

Fire station accessibility

Infrastructure counts
```

Purpose

Provides a single feature describing emergency infrastructure around the disaster.

---

## 24. Severity

Type

```text
Categorical
```

Possible Values

```text
Low

Medium

High
```

Description

Severity class assigned based on disaster characteristics.

Used for analysis and visualization.

---

## 25. ImpactScore

Type

```text
Float
```

Role

```text
Target Variable
```

Description

Represents the estimated impact caused by the disaster.

This is the value predicted by the regression models.

Higher values indicate greater disaster impact.

---

# Dataset Categories

The final dataset consists of five major groups of features.

| Category | Features |
|-----------|----------|
| Disaster Information | DisasterType, Magnitude, Depth, Time |
| Spatial Information | Latitude, Longitude |
| Weather Information | Temperature, Humidity, Rainfall, WindSpeed |
| Population Information | Population, PopulationDensity |
| Infrastructure Information | Hospital, Clinic, School, Fire Station features |
| Engineered Features | WeatherScore, InfrastructureScore |
| Target Variable | ImpactScore |

---

# Feature Sources

| Feature Group | Source |
|---------------|--------|
| Disaster Data | USGS + GDACS |
| Weather Data | Open-Meteo |
| Population Data | WorldPop |
| Infrastructure Data | OpenStreetMap |
| Engineered Features | Feature_Engineering.ipynb |
| Target Variable | Impact Assessment Formula |

---

# Dataset Ready for Machine Learning

Before model training, the dataset satisfies the following conditions:

✓ Missing values handled

✓ Duplicate records removed

✓ Numerical feature engineering completed

✓ Weather information integrated

✓ Population estimates calculated

✓ Infrastructure accessibility calculated

✓ Geospatial processing completed

✓ Suitable for supervised regression training

---

# Final Machine Learning Objective

The regression model learns the relationship

```text
Disaster Characteristics

+

Weather Conditions

+

Population Exposure

+

Infrastructure Accessibility

↓

Predicted ImpactScore
```

The trained model will later be used by the disaster response system to estimate the expected impact of new disaster events and support intelligent relief planning and resource allocation. 

