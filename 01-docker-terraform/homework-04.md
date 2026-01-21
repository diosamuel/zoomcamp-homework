# Question 4.
Which pickup day had the longest total trip distance? Only consider trips with a trip_distance less than 100 miles. (1 point)

1. 2025-11-14
2. 2025-11-20
3. 2025-11-23
4. 2025-11-25

## Solution
First, open Jupyter Notebook or Google Colab to run the code.

Use the following code to download the Parquet dataset file:

```python
!wget https://d37ci6vzurychx.cloudfront.net/trip-data/green_tripdata_2025-11.parquet
```

Next, read the `.parquet` file and display it as a DataFrame:

```python
import pandas as pd
df = pd.read_parquet("green_tripdata_2025-11.parquet")
```

There are several ways to complete this task, but I prefer to extract the month, day, and year from the pickup datetime column and store them in separate variables.

```python
df["month"] = df["lpep_pickup_datetime"].dt.month
df["day"] = df["lpep_pickup_datetime"].dt.day
df["year"] = df["lpep_pickup_datetime"].dt.year
```
Let's aggregate the data by month and day, summing the trip_distance column, so we get the total trip distance for each date.

```python
df[df["trip_distance"] < 100].groupby(["month", "day"]).agg(total=("trip_distance", "sum")).sort_values("total", ascending=False)
```

Here is the resulting table of total trip distances (less than 100 miles), grouped by month and day:

| Month | Day | Total Trip Distance |
|-------|-----|--------------------|
| 11    | 20  | 6377.03            |
|       | 19  | 6031.56            |
|       | 18  | 5976.12            |
|       | 6   | 5973.34            |
|       | 25  | 5954.80            |
|       | 5   | 5841.01            |

The day with the longest total trip distance is **20 November 2025**.

## Answer
> 2. 2025-11-20