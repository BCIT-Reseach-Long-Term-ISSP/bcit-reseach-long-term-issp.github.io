---  
layout: default  
title: react-timeseries-charts
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/v2-2022/react-timeseries-charts
---  

# react-timeseries-charts
{: .no_toc }

React Timeseries Charts is a chart library for React built from the ground up with special focus on time series data. It is used to create simple charts. It uses pondjs to handle time series data. The website for it can be found [here](http://software.es.net/react-timeseries-charts/#/).

Below are components which are used within the dashboard. Please note that some components may take props which are unlisted here; the props listed here are merely the ones used in the dashboard.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## ChartContainer

ChartContainer is a container for the whole chart.

**Props Used:**
- *options*: An object; the options set to customize the graph.
- *timeRange*: A TimeSeries object range; the full x range of the chart .
- *maxTime*: A TimeSeries object; the maximum time being displayed.
- *minTime*: A TimeSeries object; the minimum time being displayed.
- *onTimeRangeChanged*: A function; handles time range changes.
- *enablePanZoom*: A boolean; enables pan and zoom of the chart.
- *onTrackerChanged*: A function; handles tracker location changes.
- *onMouseMove*: A function; handles mouse movement.
- *minDuration*: An int; the distance between x axis ticks in milliseconds.
- *timeAxisAngledLabels*: A boolean; enables angled x axis labels.
- *timeAxisTickCount*: An int; the number of maximum ticks displayed on the x axis.
- *timeAxisHeight*: An int; the height of the x axis in pixels.
- *timeAxisStyle*: An object; the styling for the x axis.
- *showGrid*: A boolean; shows the vertical gridlines.

## ChartRow

ChartRow is a container for all the rows in the chart.

**Props Used:**
- *height*: An int; the height of the y axis section of the chart .

## YAxis

YAxis defines the Y axis of the chart.

**Props Used:**
- *id*: A string; the id of the y axis.
- *label*: A string; the label for the y axis.
- *min*: A number; the minimum value displayed on the y axis.
- *max*: A number; the maximum value displayed on the y axis.
- *showGrid*: No value; shows the horizontal gridlines.
- *style*: An object; the styling for the y axis.
- *format*: A string; the display format of the values of the y axis.
- *width*: An int; the width of the y axis in pixels.

## Charts

Charts is the actual time series chart being plotted.

## LineChart

LineChart defines the line being plotted on the chart from time series data.

**Props Used:**
- *axis*: A string; the id of the y axis.
- *series*: A TimeSeries; the dataset used in the line plot.
- *columns*: An array of strings; the ids/labels of the dataset columns.
- *style*: An object; the styling for the line plot.

## Baseline

Baseline defines the baselines being plotted on the chart.

**Props Used:**
- *axis*: A string; the id of  the y axis.
- *style*: An object; the styling for the baseline.
- *value*: A number; the y value that the baseline sits at.
- *label*: A string; the label for the baseline.
- *position*: A string; the positioning of the baseline's label.