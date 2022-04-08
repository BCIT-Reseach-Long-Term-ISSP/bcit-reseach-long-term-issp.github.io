---  
layout: default  
title: React CSV
parent: React  
grand_parent: Dashboard
has_toc: false
permalink: /docs/dashboard/react/react-csv
---  

# React CSV
{: .no_toc }

React CSV is a library used to convert data in CSV files for download. The website for it can be found [here](https://react-csv.github.io/react-csv/).

Below are components which are used within the dashboard. Please note that some components may take props which are unlisted here; the props listed here are merely the ones used in the dashboard.

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## CVSLink

CVSLink is a component that turns data into csv files and renders a link to download it.

**Props Used:**
- *data*: An object; the data to be turned into a csv.
- *filename*: A string; the csv file name.