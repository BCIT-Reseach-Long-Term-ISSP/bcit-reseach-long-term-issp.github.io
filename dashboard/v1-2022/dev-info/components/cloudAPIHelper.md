---  
layout: default  
title: React - Dashboard API Helper
parent: Archive - Dashboard v2 (2022)
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/v2-2022/cloudAPIHelper
---  

# Dashboard API Helper
{: .no_toc }

A file of constants and helper functions used to dynamically build URIs for accessing the database and process the data retrieved.

**Exported Functions:**
- *buildCurrentURL*: Returns a url in the a valid format for current data queries.
    - selected_ids: An array of device ids as strings.
- *buildHistoricalURL*: Returns a url in the a valid format for historical data queries.
    - selected ids: An array of device ids as strings.
    - measure_name: A string representing the shorthand for the desired metric, in lower case.
    - time_start: A date object representing the start of the desired time range.
    - time_end: A date object representing the end of the desired time range.
- *buildThresholdURL*: Returns a url in the a valid format for threshold data queries.
    - selected ids: An array of device ids as strings.
    - measure_name: A string representing the shorthand for the desired metric, in lower case.
    - time_start: A date object representing the start of the desired time range.
    - time_end: A date object representing the end of the desired time range.
    - comparison_operator: A string of either ">" or "<" indicating whether the desired return values are greater than or less than the number given.
    - threshold: A float or integer indicating the desired threshold value.
- *metricValueTypeHandler*: Accepts the shorthand metric name as a string and returns the measure_value type it is associated with in the database (Currently either "measure_value::double" or "measure_value::boolean).
- *isQuantitative*: Accepts the shorthand metric name as a string and returns true if the values associated with the metric are quantitative. Returns false if qualitative.
- *isWithinThreshold*: Accepts a shorthand metric name as a string and a value as a float and returns true if the value provided is within the (currently hardcoded) threshold for that metric.

**Exported Constants:**
- *BUILD_ID_LIST_URL*: The url used in GET requests for a list of unique IDs.
- *METRIC_NAMES*: An object containing key: value pairs of shorthand metric names and their full counterparts as a string.
- *METRIC_VALUE_TYPES*: An object containing key: value pairs of the measure_value types used in the database and the metric names associated with those types.
- *METRIC_UNITS*: An object containing key: value pairs of shorthand metric names and their associated measured units as a string.
- *GET_REQUEST_OPTIONS*: An object containing the options used for the dashboard API get requests.