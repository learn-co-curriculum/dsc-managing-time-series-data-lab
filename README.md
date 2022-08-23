# Managing Time Series Data - Lab

## Introduction

In the previous lesson, you learned that time series data are everywhere and working with time series data is an important skill for data scientists!

In this lab, you'll practice your previously learned techniques to import, clean, and manipulate time series data.

The lab will cover how to perform time series analysis while working with large datasets. The dataset can be memory intensive so your computer will need at least 2GB of memory to perform some of the calculations.


## Objectives

You will be able to:

- Load time series data using pandas and perform time series indexing 
- Perform data cleaning operation on time series data 
- Change the granularity of a time series 


## Let's get started!

Import the following libraries: 

* `pandas`, using the alias `pd` 
* `pandas.tseries` 
* `matplotlib.pyplot`, using the alias `plt` 
* `statsmodels.api`, using the alias `sm`


```python
# Load required libraries

```

## Loading time series data
The `statsmodels` library comes bundled with built-in datasets for experimentation and practice. A detailed description of these datasets can be found [here](http://www.statsmodels.org/dev/datasets/index.html). Using `statsmodels`, the time series datasets can be loaded straight into memory. 

In this lab, we'll use the **Atmospheric CO2 from Continuous Air Samples at Mauna Loa Observatory, Hawaii, U.S.A.**, containing CO2 samples from March 1958 to December 2001. Further details on this dataset are available [here](http://www.statsmodels.org/dev/datasets/generated/co2.html).

In the following cell we: 

- Load the `co2` dataset using the `.load()` method 
- Converted this into a pandas DataFrame 


```python
# Run this cell without changes

# Load the 'co2' dataset from sm.datasets
data_set = sm.datasets.co2.load()

# load in the data_set into pandas dataframe
CO2 = pd.DataFrame(data=data_set['data'])
```

With all the required packages imported and the `CO2` dataset as a dataframe ready to go, we can move on to indexing our data.

## Date Indexing

While working with time series data in Python, having dates (or datetimes) in the index can be very helpful, especially if they are of `DatetimeIndex` type. Further details can be found [here](http://pandas.pydata.org/pandas-docs/stable/generated/pandas.Timestamp.html).

The exact structure of the data from `sm.datasets` has changed over time depending on the version of StatsModels. So below we check whether the index is already a `DatetimeIndex`, and if it isn't, we set it to be one. Either way we'll also set the name of the index to be `date`.


```python
# Run this cell without changes

# Confirm that date values are used for indexing purpose in the CO2 dataset 
if isinstance(CO2.index, pd.DatetimeIndex):
    CO2.index.name = 'date'
else:
    CO2.rename(columns={'index':'date'}, inplace=True)
    CO2.set_index('date', inplace=True)
    
CO2.head()
```

We can also inspect the index itself:


```python
# Run this cell without changes
CO2.index
```

The output above shows that our dataset clearly fulfills the indexing requirements. Look at the last line:


> **dtype='datetime64[ns]',... length=2284,...'**


* `dtype=datetime[ns]` field confirms that the index is made of timestamp objects.
* `length=2284` shows the total number of entries in our time series data. 

## Resampling

Remember that depending on the nature of analytical question, the resolution of timestamps can also be changed to other frequencies. For this dataset we can resample to monthly CO2 consumption values. This can be done by using the `.resample()` method as seen in the earlier lesson. 

* Group the data into buckets representing 1 month using `.resample()` method 
* Call the `.mean()` method on each group (i.e. get monthly average) 
* Combine the result as one row per monthly group 


```python
# Group the time series into monthly buckets
CO2_monthly = None

# Take the mean of each group 
CO2_monthly_mean = None

# Display the first 10 elements of resulting time series

```

Looking at the index values, we can see that our time series now carries aggregated data on monthly terms, shown as `Freq: MS`. 

### Time-series Index Slicing for Data Selection

Slice our dataset to only retrieve data points that come after the year 1990.


```python
# Slice the timeseries to contain data after year 1990 

```

Retrieve data starting from Jan 1990 to Jan 1991: 


```python
# Retrieve the data between 1st Jan 1990 to 1st Jan 1991

```

## Missing Values

Find the total number of missing values in the dataset.


```python
# Find the total number of missing values in the time series

```

Remember that missing values can be filled in a multitude of ways. 

- Replace the missing values in `CO2_monthly_mean` with a previous valid value 
- Next, check if your attempt was successful by checking for number of missing values again 


```python
# Perform backward filling of missing values
CO2_final = None

# Find the total number of missing values in the time series

```

Great! Now your time series data are ready for visualization and further analysis.

## Summary

In this introductory lab, you learned how to load and manipulate time series data in Python using pandas. You confirmed that the index was set appropriately, performed queries to subset the data, and practiced identifying and addressing missing values.
