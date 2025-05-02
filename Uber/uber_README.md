# Uber Project

## Data Cleaning & Preperation:

The first step of my data analysis is to clean the data and prepare it accordingly. The process was fairly simple since the data was already well oganized. I only had to bind the data together into one main dataset and format the Date Time column. Here is what the R code would look like:

<img src="Data332/Uber/cody.png" height = 250 width = 400>

## Pivot tables

First I had to make pivot tables out of the data and used the function group_by

<img src="Uber/screenshot_89.png" height = 250 width = 400>

## Chart showing Trips every day

Analysis: Trips tend to increase toward the end of the month, peaking multiple times and on the 30th.

<img src="Uber/tripsEveryDay.png" height = 250 width = 400>

## Chart showing Trips by Day and Month

Analysis: High activity seen throughout September, especially around the 13th.

<img src="Uber/tripsDayMonth.png" height = 250 width = 400>

## Chart showing Heat Map by Month and Day

Analysis: September has many busy days, particularly 5th–7th and 18th–28th.

<img src="Uber/heatMonthDay.png" height = 250 width = 400>

## Geospital Map

Analysis: Pickup locations plotted from a subset of Uber rides. The more central the more rides.

<img src="Uber/GeoMap.png" height = 250 width = 400>

## Prediciton Model

This section builds a simple linear model to predict total trips based on hour and month.

<img src="Uber/predict.png" height = 250 width = 400>

## Shiny App
https://philipexldataclass.shinyapps.io/Uber/
