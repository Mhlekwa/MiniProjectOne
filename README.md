import pandas as pd
import duckdb

data = pd.read_csv("delivery_data.csv")

duckdb.register("delivery_data", data)

result = duckdb.query("""
    SELECT city, COUNT(*) AS number_of_delays
    FROM delivery_data
    WHERE delay_minutes > 0
    GROUP BY city
    """).to_df()

result

