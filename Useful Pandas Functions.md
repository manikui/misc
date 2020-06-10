# Useful Pandas and Numpy Functions


## Pandas

```df``` is a Pandas dataframe, ```s``` is a Pandas series, ```pd``` refers to the Pandas package that is typically imported in the following way: ```import pandas as pd```

| Name | Description | Input Parameter(s) | Output |
| -------- | -------- | -------- | -------- |
| ```df.columns```  | Retrieves all of the column names from ```df``` | None | Array |
| ```df.shape```  | Returns a tuple of the number of rows and columns in ```df``` | None | Tuple of the form: ```(number of rows, number of columns)``` |
| ```df.col_name``` or ```df[col_name]```  or ```df.loc[:, col_name]```   | Retrieves ```col_name```  from ```df``` and returns a series| ```col_name``` : String of column name in ```df```     | Pandas series|
| ```df[[col_name_list]]```   or ```df.loc[:, [col_name_list]]```  | Retrieves all columns inside ```col_name_list``` from ```df``` and returns a dataframe | ```col_name_list``` : List of column names (as strings) in ```df```     | Pandas dataframe|
| ```s.iloc[row_index]```    | Retrieves a single item at index ```row_index``` from ```s```. If ```row_index``` is a list, it retrieves items at the corresponding indices from ```s``` | ```row_index``` : Index of item as an integer or list of indices in ```s``` | Item or Pandas series|
| ```df.iloc[row_index, col_index]```  | Retrieves a single item at row ```row_index``` and column ```col_index``` from ```df```. | ```row_index``` : Row index as an integer; ```col_index```: Column index as an integer | Item |
| ```df.iloc[list_of_row_indices, col_index]``` or ```df.iloc[start_row_index : end_row_index]``` | Retrieves all items at the corresponding row indices and column index from ```df```. | ```list_of_row_indices``` : List of row indices ; ```col_index```: Column index as an integer | Pandas series |
| ```df.iloc[row_index, list_of_col_indices]``` or ```df.iloc[row_index, start_col_index : end_col_index]``` | Retrieves all items at the given row index for all columns in ```list_of_col_indices``` from ```df```. | ```row_index``` : Row index as an integer ; ```list_of_col_indices```: List of column indices as an integer | Pandas dataframe |
| ```df.iloc[list_of_row_indices, list_of_col_indices]``` or ```df.iloc[start_row_index : end_row_index, start_col_index : end_col_index]```  | Retrieves all rows in ```list_of_row_indices``` for all columns in ```list_of_col_indices``` from ```df``` | ```list_of_row_indices```: List of row indices; ```list_of_col_indices```: List of column indices as an integer | Pandas dataframe |
| ```df.head(n)``` or ```s.head(n)``` | Retrieves the first n rows | ```n```: Number of rows to display. If ```n``` is not specified, it defaults to 5 | Pandas dataframe or series|
| ```df.describe()``` or ```s.describe()``` | Provides summary statistics for ```s``` or across all columns in ```df``` | None | Pandas dataframe or series|
| ```s.unique()``` or ```df[col_name].unique()``` | Returns an array of all unique values in ```s``` or in column ```col_name``` in ```df``` | ```col_name``` : Name of column as a string | Array|
| ```s.value_counts()``` or ```df[col_name].value_counts()``` | Returns a series containing the number of times each value  in ```s``` or in column ```col_name``` of ```df``` appears | ```col_name``` : Name of column as a string | Pandas series |
| ```df.sort_values(col_name, ascending = True)``` or ```s.sort_values(ascending = True)``` | Sorts ```s``` or ```df``` rows by values in column ```col_name``` | ```col_name``` : Name of column as a string; (Optional) ```ascending```: If true sorts rows from least to greatest | Pandas dataframe or series|
| ```df.drop(columns = [list_of_column_names])``` | Removes all columns in ```list_of_column_names``` from ```df``` | ```list_of_column_names```: List of columns to drop | Pandas dataframe |
| ```df.dropna()``` or ```s.dropna()``` | Removes all rows containing missing values from ```df``` or ```s``` | None | Pandas dataframe or series with all rows containing missing values removed|
| ```df.dropna(axis = 1)``` | Removes all columns containing missing values from ```df``` or ```s``` | None | Pandas dataframe with all columns containing missing values removed|
| ```df.rename(dict, axis = 1)``` | Renames columns in ```df``` according to dictionary ```dict``` passed in | ```dict```: A dictionary mapping previous column values to new column values | Pandas dataframe with renamed columns|
| ```df[bool_array]``` or ```df.loc[bool_array]```| Filters rows in ```df``` according to boolean array passed in | ```bool_array```: array of True or False values that correspond to whether a row is included or excluded in the dataframe. Common ```bool_array``` example: ```df[col_name] >= value``` | Pandas dataframe containing filtered rows|
| ```df.groupby(column).function()```| Groups unique values in ```column``` together, then applies ```function()``` to them | ```column```: Name of column to group values over or list of column names; ```function()```: Aggregation function, typically ```mean()``` or ```count()``` | Pandas dataframe containing grouped values with each unique value getting 1 row|
| ```pd.merge(left, right, how = "inner", on = col_name)```| Joins 2 dataframes ```left``` and ```right``` using their values in column ```a```. Requires both dataframes have a column named ```a```. | ```left, right```: Dataframes to merge; ```on```: Name of column containing values to merge | Pandas dataframe containing merged values from ```left``` and ```right```|
| ```left.merge(right, how = "inner", left_on = left_col_name, right_on = right_col_name)```| Joins ```right``` dataframe on ```left``` using values in column ```left_col_name``` and ```right_col_name```. Does not require both dataframes have similarly-named columns. | ```left, right```: Dataframes to merge; ```left_on```: Name of column in ```left``` containing values to merge; ```right_on```: Name of column in ```right``` containing values to merge; | Pandas dataframe containing merged values from ```left``` and ```right```|
| ```df.set_index(col_name)``` | Re-indexes ```df``` using values from ```col_name```. Note: this requires all values in ```col_name``` be unique | ```col_name```: Name of column that will be the new index | Pandas dataframe with ```col_name``` as the index|
| ```pd.read_csv(file_name)``` | Reads in a CSV file located in ```file_name``` as a dataframe or series (if the CSV only has 1 column) | ```file_name```: Name of CSV file to be read in | Pandas series or dataframe |

## Numpy

```np``` refers to the numpy package, typically imported in the following way: ```import numpy as np```
| Name | Description |
| -------- | -------- |
| ```np.arange(start, stop, step)``` | Creates an array of numbers starting at ```start``` and ending at ```stop```, not inclusive, with step size ```step```. If ```step``` is not specified, it defaults to 1 |
| ```np.linspace(start, stop, num = ...)``` | Creates an array of numbers that are evenly space starting at ```start``` and ending at ```stop```, not inclusive. If ```num``` is not specified, it defaults to 50 |
| ```np.mean(array)```, ```np.std(array)```,```np.median(array)```, ```np.max(array)```,```np.min(array)``` | Different summary statistics functions that can be applied to arrays of numbers |
| ```np.count_nonzero(array)```| Counts the number of non-zero (or True) elements in an array |
| ```np.append(array, item_to_append)```| Appends ```item_to_append``` to the end of ```array``` |
| ```np.percetile(array, q)```| Calculates the value at percentile ```q```  in ```array```|