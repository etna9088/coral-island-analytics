# Coral Island Crop Analysis 
An automated commercial pricing model and resource allocation dashboard engineered in Power BI to optimize capital investments within a digital farming economy.

## Business Problem or Objective
In simulated economies (and real-world agriculture), managers face a strict resource allocation problem: balancing short-term cash flow with long-term capital investments under tight constraints (limited funds, land, and stamina). I am building this project to replace "guesswork" gameplay with a rigorous financial model. The objective is to project 36-month cumulative profit and identify the most capital-efficient inventory investments across 89 distinct asset classes.

## Core Features & Functionality
* **Dynamic Asset Amortization:** Implementing advanced DAX logic to identify multi-season assets and automatically amortize their initial seed cost across active seasons, preventing the engine from double-charging the initial capital expenditure.
* **Capital Efficiency Tracking:** Engineering nested conditional variables (`VAR`) to calculate a true 3-Year ROI % based on specific, highly-variable asset lifecycles and depreciation rates.
* **Cash Velocity Modeling:** Tracking short-term liquidity to prove that high-frequency, regrowing inventory is a critical driver for early-stage growth, despite looking less impressive on paper than high-margin long-term assets.

## Tech Stack & Tools
* **Data Curation:** MS Excel
* **BI / Visualization:** MS Power BI Desktop
* **Calculations:** DAX (Data Analysis Expressions)
* **Data Modeling:** Dimensional Modeling

## Data Architecture & Pipeline
Due to a lack of available clean telemetry, raw data is manually extracted and curated from v1.1 game telemetry and community wikis into a structured CSV file (`Crops_Data.csv`). This flat file is loaded into Power BI and modeled to handle strict 28-day seasonal granularity. Because multi-season assets create complex context transition errors, I am building sequential DAX measures utilizing hardcoded arrays to enforce strict accounting logic and calculate accurate cumulative profit.

## Installation & Deployment
*(Note: I am currently finalizing the report visuals and DAX measures. The full `.pbix` file will be available soon.)*

1. Clone the repository to your local machine to view the raw dataset and DAX methodology:
```bash
git clone [https://github.com/etna9088/coral-island-analytics.git](https://github.com/etna9088/coral-island-analytics.git)
```
2. Open the `/Data` folder to view the custom-built asset catalog.
