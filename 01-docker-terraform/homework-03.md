# Question 3.

For the trips in November 2025, how many trips had a trip_distance of less than or equal to 1 mile? (1 point)

1. 7,853
2. 8,007
3. 8,254
4. 8,421

## Solution
First, open Jupyter Notebook or Google Colab to run the code.

Use the following code to download the Parquet dataset file:

```python
!wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-11.parquet
```

Then, read the `.parquet` file and display it as a DataFrame:

```python
import pandas as pd
df = pd.read_parquet("green_tripdata_2025-11.parquet")
df
```

This is a preview of the data, it consists of 21 columns.

| VendorID | lpep_pickup_datetime | lpep_dropoff_datetime | store_and_fwd_flag | RatecodeID | PULocationID | DOLocationID | passenger_count | trip_distance | fare_amount | extra | mta_tax | tip_amount | tolls_amount | ehail_fee | improvement_surcharge | total_amount | payment_type | trip_type | congestion_surcharge | cbd_congestion_fee |
|---------:|----------------------|-----------------------|--------------------|-----------:|-------------:|-------------:|----------------:|--------------:|------------:|------:|--------:|-----------:|--------------:|----------:|----------------------:|-------------:|-------------:|----------:|----------------------:|-------------------:|
| 2 | 2025-11-01 00:34:48 | 2025-11-01 00:41:39 | N | 1.0 | 74 | 42 | 1.0 | 0.74 | 7.20 | 1.00 | 0.5 | 1.94 | 0.0 | NaN | 1.0 | 11.64 | 1.0 | 1.0 | 0.00 | 0.00 |
| 2 | 2025-11-01 00:18:52 | 2025-11-01 00:24:27 | N | 1.0 | 74 | 42 | 2.0 | 0.95 | 7.20 | 1.00 | 0.5 | 0.00 | 0.0 | NaN | 1.0 | 9.70 | 2.0 | 1.0 | 0.00 | 0.00 |

Before we work with the data, it’s important to convert the column we’re using to the correct data type. In this case, we’ll convert `lpep_pickup_datetime` to a datetime column.

```python
df["lpep_pickup_datetime"] = pd.to_datetime(df["lpep_pickup_datetime"])
```

To filter the date range, we can use the `between()` method with two parameters: the start date and the end date (see [pandas.Series.between](https://pandas.pydata.org/docs/reference/api/pandas.Series.between.html)). Save the filtered result into a new variable called `df_result`.

```python
df_result = df[df["lpep_pickup_datetime"].between("2025-11-01","2025-12-01")]
```

Because the question asks for trips with a `trip_distance` of less than or equal to 1 mile, we can filter like this:

```python
df_result[df_result["trip_distance"] <= 1].reset_index()
```
This filters rows where `trip_distance` is less than or equal to 1.

We can count the total number of matching trips by using `len()`:

```python
len(df_result[df_result["trip_distance"] <= 1].reset_index())
```

## Answer
> 8007 Trips

