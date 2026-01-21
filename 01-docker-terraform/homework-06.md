# Question 6.
For the passengers picked up in the zone named "East Harlem North" in November 2025, which drop-off zone had the largest tip? (1 point)

1. JFK Airport
2. Yorkville West
3. East Harlem North
4. LaGuardia Airport

## Solution

Based on code from previous homework, let's first combine the main dataframe with the zone dataframe to get the drop-off location.
```python
df_dropout = pd.merge(df, df_zone, left_on="DOLocationID", right_on="LocationID")
```

Next, we merge `df_dropout` and `df_zone` again using `PULocationID` (which refers to the pick-up location). Here is the code:

```python
df_pickup = pd.merge(df_dropout, df_zone, left_on="PULocationID", right_on="LocationID")
```

It seems the column names are temporarily confusing, so let's rename the relevant columns:
```python
df_drop_zone = df_pickup.rename(columns={"Zone_x": "zone_drop", "Zone_y": "zone_pickup"})
```
Finally, we can group by `zone_drop` (since the question asks about the drop-off zone). We then aggregate `tip_amount`, and sort the results from highest to lowest total tip amount to identify the drop-off zone with the largest tips given by customers.
```python
df_drop_zone.groupby("zone_drop").agg(total=("tip_amount", "sum")).sort_values("total", ascending=False)
```

| zone_drop               | total    |
|-------------------------|----------|
| LaGuardia Airport       | 7233.92  |
| Upper East Side North   | 6964.59  |
| Upper West Side North   | 5470.67  |
| East Harlem South       | 4473.86  |

From the table, we can see that LaGuardia Airport received the highest total tip amount.

## Answer
> 4. LaGuardia Airport