# Radar Speed Analysis Dashboard

This Shiny web application merges and visualizes radar speed data collected by students from multiple GitHub repositories. It allows users to interactively explore how vehicle speed varies with factors like time of day, car type, and collector identity.

## Features

- **Data Merging**: Combines multiple datasets (CSV/XLSX) from GitHub.
- **Data Cleaning**: Standardizes inconsistent column names, parses time formats, and categorizes vehicle types.
- **Interactive Visualization**: Displays bar charts of average speed grouped by customizable X-axis and color grouping.
- **Live Table Output**: View the underlying data driving the plots.

## Technologies Used

- **R**
- **Shiny** (UI and interactivity)
- **ggplot2** (visualization)
- **dplyr** and **janitor** (data cleaning)
- **lubridate** (time parsing)
- **readr**, **readxl**, **httr** (data importing)
- **DT** (interactive data tables)

## Data Sources

This project loads radar speed tracking datasets from seven different GitHub repositories, with files in `.csv` and `.xlsx` formats. Each dataset may have slight differences in naming conventions and structure, which the app automatically resolves.

## Data Cleaning Details

- Merges similar columns like:
  - `speed`, `mph`, `final_speed` → `speed`
  - `time`, `hour`, `hr_min` → `time`
  - `recorder`, `student`, `name` → `name`
  - `type_of_car`, `vehicle_style`, `body_style` → `type_of_car`
- Cleans and normalizes:
  - Color labels (`light grey`, `dark grey`, etc. → `grey`)
  - Vehicle types (`1`, `van` → `minivan`, etc.)
- Parses and standardizes time to `HH:MM` format.

## Example Use Cases

- Analyze speeding patterns throughout the day.
- Compare speeds across student collectors.
- Identify which vehicle types tend to drive faster.

## This bar chart shows Speed vs type_of_car split by color

You can tell that black coupes are the fastest cars, whereas grey minivans are the slowest.

<img src="[Data332/carDataCollection/TypeByColor.png](https://github.com/PhilipExl/Data332/blob/main/carDataCollection/TypeByColor.png)">

## Shiny App

https://philipexldataclass.shinyapps.io/countCars/
