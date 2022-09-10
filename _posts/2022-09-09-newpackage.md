---
layout: post
title: PWS Helper Package Released
---

After struggling with retrieving the Latitude and Longitude of Public Water Systems(PWS) provided by the Environmental Protection Agency(EPA), I developed and released a Python package that processes the PWSID and outputs the geographical location.

It uses the `BeautifulSoup` package to scrape the address of water systems from the [EPA's Safe Drinking Water Information System](https://www.epa.gov/enviro/sdwis-search). In turn, it uses the `GeoPy` and `Pgeocode` packages to geocode the addresses and locate the water system.

## Table of Contents
1. [Requirements](#require)
2. [Example](#example)
3. [Repository](#repo)
4. [Download](#download)
5. [References](#ref)

## Requirements <a name="require"></a>
- `GeoPy` and `Pgeocode`
- `Pandas`
- `NumPy`
- `BeautifulSoup`

## Example <a name="example"> </a>

Let us assume we want to get the Lat/Long data for water systems in the state of Alabama. 

```python
import pws_helper.locator as locator
import pandas as pd

df = pd.read_csv("Alabama.csv")
df.head()
```

The dataframe looks as such.

|   |                 System Name |     PWSID |
|--:|----------------------------:|----------:|
| 0 |       ALABASTER WATER BOARD | AL0001148 |
| 1 | ALBERTVILLE UTILITIES BOARD | AL0000933 |
| 2 |        ARDMORE WATER SYSTEM | AL0001420 |
| 3 |           ARLEY WATER WORKS | AL0001403 |
| 4 |            ATHENS UTILITIES | AL0000824 |

```python
res = locator.frame_latlonger(df, "AL", "Alabama")
```
> There are missing entries. Please fill spots with the postalcoder function

This means that our initial search did not work for some PWSIDs

```python
df = res[0]
missing = res[1]

missing
```

|    |                        System Name |     PWSID | Latitude | Longitude |
|---:|-----------------------------------:|----------:|---------:|----------:|
| 19 | DEER PARK-VINEGAR BEND WATER & FPA | AL0001368 |      NaN |       NaN |

There are two options to fill these missing entries. The first option users should choose is the `postalcoder()` function.

```python
res = locator.postalcoder(df, missing, "AL")
```

If there are no output messages, then the `pandas` dataframe is final and ready to go. If there are still missing entries, the function will output

> There are still missing entries. Please fill manually with manual_filler

In this case, the user must find an address that Nominatim(OpenStreetMap) can process.

```python
manual_dict = {"AL0001368": "Deer Park, Alabama"}
res = locator.manual_filler(df, manual_dict)
```

If the manually inputted addresses do indeed work, there should be no more missing entries.

```python
res[res.Latitude.isnull()]
```

> System Name	PWSID	Latitude	Longitude

If the user wishes to save this result, the user may do so using the `pandas.to_csv()` function.

```python
res.to_csv("[FILE NAME].csv")
```

## Repository <a name="repo"> </a>

Detailed documentation about the package is at my [GitHub repository](https://github.com/bpark67/PWS_Helper). 

## Download <a name="download"> </a>

You may directly download the package with this [link](https://github.com/bpark67/PWS_Helper/archive/refs/tags/v1.0.0-alpha.tar.gz).

## References <a name="ref"></a>
- https://srome.github.io/Parsing-HTML-Tables-in-Python-with-BeautifulSoup-and-pandas/
- https://www.epa.gov/enviro/sdwis-search