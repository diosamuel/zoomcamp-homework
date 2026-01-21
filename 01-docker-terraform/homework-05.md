# Question 5.

Which was the pickup zone with the largest total_amount (sum of all trips) on November 18th, 2025? (1 point)

1. East Harlem North
2. East Harlem South
3. Morningside Heights
4. Forest Hills

## Solution

We need one more file for this task. Please download it using the code below:

```
!wget https://github.com/DataTalksClub/nyc-tlc-data/releases/download/misc/taxi_zone_lookup.csv
```

Example of the data:

| LocationID | Borough | Zone                      | service_zone |
|------------|---------|---------------------------|--------------|
| 1          | EWR     | Newark Airport            | EWR          |
| 2          | Queens  | Jamaica Bay               | Boro Zone    |
| 3          | Bronx   | Allerton/Pelham Gardens   | Boro Zone    |

Let’s import both files:

```python
import pandas as pd
df = pd.read_parquet("./green_tripdata_2025-11.parquet")
df_zone = pd.read_csv("./taxi_zone_lookup.csv")
df_zone = df_zone.dropna()
```

Next, merge the two tables using `PULocationID` and `LocationID` as the join keys:

```python
df_joined = pd.merge(df,df_zone,left_on="PULocationID",right_on="LocationID")
df_joined
```

This will create one combined table (the main `df` and `df_zone`) and store it in the `df_joined` variable.

Now, let’s filter trips for **November 18th, 2025**, then group by zone and aggregate the sum of `total_amount`:

```python
df_joined[
    (df_joined["day"] == 18) & (df_joined["months"] == 11) & (df_joined["year"] == 2025)
].groupby("Zone").agg(total=("total_amount", "sum")).sort_values("total", ascending=False)
```

Lastly, we can sort from the highest to the lowest `total_amount`.

| Zone                     | total    |
|--------------------------|----------|
| East Harlem North        | 9281.92  |
| East Harlem South        | 6696.13  |
| Central Park             | 2378.79  |
| Washington Heights South | 2139.05  |

We can see that East Harlem North is the pickup zone that have the highest total amount that user paying.

## Answer
```1. East Harlem North```