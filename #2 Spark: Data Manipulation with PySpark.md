**Sorting Data**
- Use the orderBy() function to sort your data based on specific columns.
    - ```python
      # Sort data based on a column
      sorted_df = df.orderBy('column_name')
      ```

**Filtering Data**
- Filter data based on specific conditions to extract exactly what you need.
    - ```python
      # Filtering data based on a condition
      filtered_df = df.filter(df['column'] > 100)
      ```

    - ```python
      # Filtering data with multiple conditions
      filtered_df = df.filter((df['column1'] > 100) & (df['column2'] == 'value'))
      ```

**Grouping and Aggregating Data**
- Organize your data into groups and perform calculations on those groups.
    - ```python
      # Grouping data by a column and calculating aggregate functions
      grouped_df = df.groupBy('column').agg({'column2': 'sum', 'column3': 'avg'})
      ```
      
    - ```python
      # Applying aggregate functions to entire DataFrame
      agg_df = df.agg({'column1': 'max', 'column2': 'min'})
      ```

**Joins and Combining DataFrames**
- Merge different datasets based on common keys to create a unified dataset.
    - ```python
      # Performing inner join
      inner_join_df = df1.join(df2, df1['key'] == df2['key'], 'inner')
      ```
      
    - ```python
      # Performing left join
      left_join_df = df1.join(df2, df1['key'] == df2['key'], 'left')
      ```

**Handling Missing Data**
- Deal with missing or null values using functions like fillna() and dropna().
    - ```python
      # Fill null values with a specific value
      filled_df = df.fillna(0)

      # Drop rows with null values
      cleaned_df = df.dropna()
      ```

**Working with Dates and Times**
- Extract useful information like year, month, or day from date columns.
    - ```python
      from pyspark.sql.functions import year, month, dayofmonth

      # Extracting year from date column
      df = df.withColumn('year', year(df['date_column']))
      
    - ```python
      from pyspark.sql.functions import year, month, dayofmonth
      
      # Extracting month from date column
      df = df.withColumn('month', month(df['date_column']))
      
    - ```python
      from pyspark.sql.functions import year, month, dayofmonth
      
      # Extracting day of month from date column
      df = df.withColumn('day', dayofmonth(df['date_column']))
      ```

**Pivoting Data**
- Transform data from a long format to a wide format using pivot() or groupBy().pivot().
    - ```python
      # Pivot data based on a column
      pivoted_df = df.groupBy('column1').pivot('column2').agg({'column3': 'sum'})
      ```

**Window Functions**
- Perform calculations across a set of rows related to your current row using window functions.
    1. ```python
       from pyspark.sql.window import Window
       from pyspark.sql.functions import row_number

       # Define window specification
       windowSpec = Window.partitionBy('column1').orderBy('column2')
       ```
       
    2. ```python       
       # Use window function
       df = df.withColumn('row_number', row_number().over(windowSpec))
       ```

**Sampling Data**
- Use methods like sample() to extract a subset of data for exploratory analysis or testing.
    - ```python
      # Sample data
      sampled_df = df.sample(fraction=0.5, seed=42)
      ```

**User-Defined Functions (UDFs)**
- Create custom functions to perform specific operations on DataFrame columns.
      
    1. ```python
       from pyspark.sql.functions import udf
       from pyspark.sql.types import IntegerType

       # Define a UDF
       def square(x):
           return x * x
       ```
      
    2. ```python
       # Register UDF
       square_udf = udf(square, IntegerType())
       ```
      
    3. ```python
       # Apply UDF to DataFrame column
       df = df.withColumn('squared_column', square_udf(df['column']))
       ```
