# Useful Pandas, Numpy and Matplotlib Functions


## Pandas

```df``` is a Pandas dataframe, ```s``` is a Pandas series

| Name | Description | Input Parameter(s) | Output |
| -------- | -------- | -------- | -------- |
| ```df.columns```  | Retrieves all of the column names from ```df``` | None | Array |
| ```df.shape```  | Returns a tuple of the number of rows and columns in ```df``` | None | Tuple of the form: ```(number of rows, number of columns)``` |
| ```df.col_name``` or ```df[col_name]```  or ```df.loc[:, col_name]```   | Retrieves ```col_name```  from ```df``` and returns a series| ```col_name``` : String of column name in ```df```     | Pandas series|
| ```df[[col_name_list]]```   or ```df.loc[:, [col_name_list]]```  | Retrieves all columns inside ```col_name_list``` from ```df``` and returns a dataframe | ```col_name_list``` : List of column names (as strings) in ```df```     | Pandas dataframe|
| ```s.iloc[row_index]```    | Retrieves a single item at index ```row_index``` from ```s```. If ```row_index``` is a list, it retrieves items at the corresponding indices from ```s``` | ```row_index``` : Index of item as an integer or list of indices in ```s``` | Item or Pandas series|
| ```df.iloc[row_index, col_index]```  | Retrieves a single item at row ```row_index``` and column ```col_index``` from ```df```. | ```row_index``` : Row index as an integer; ```col_index```: Column index as an integer | Item |
| ```df.iloc[list_of_row_indices, col_index]```  | Retrieves all items at the corresponding row indices and column index from ```df```. | ```list_of_row_indices``` : List of row indices ; ```col_index```: Column index as an integer | Pandas series |
| ```df.iloc[row_index, list_of_col_indices]```  | Retrieves all items at the given row index for all columns in ```list_of_col_indices``` from ```df```. | ```row_index``` : Row index as an integer ; ```list_of_col_indices```: List of column indices as an integer | Pandas dataframe |
| ```df.iloc[list_of_row_indices, list_of_col_indices]```  | Retrieves all rows in ```list_of_row_indices``` for all columns in ```list_of_col_indices``` from ```df``` | ```list_of_row_indices```: List of row indices; ```list_of_col_indices```: List of column indices as an integer | Pandas dataframe |
| ```df.head(n)``` or ```s.head(n)``` | Retrieves the first n rows | ```n```: Number of rows to display. If ```n``` is not specified, it defaults to 5 | Pandas dataframe or series|
| ```df.describe()``` or ```s.describe()``` | Provides summary statistics for ```s``` or across all columns in ```df``` | None | Pandas dataframe or series|
| ```s.unique()``` or ```df[col_name].unique()``` | Returns an array of all unique values in ```s``` or in column ```col_name``` in ```df``` | ```col_name``` : Name of column as a string | Array|
| ```s.value_counts()``` or ```df[col_name].value_counts()``` | Returns a series containing the number of times each value  in ```s``` or in column ```col_name``` of ```df``` appears | ```col_name``` : Name of column as a string | Pandas series |
| ```df.sort_values(col_name, ascending = True)``` or ```s.sort_values(ascending = True)``` | Sorts ```s``` or ```df``` rows by values in column ```col_name``` | ```col_name``` : Name of column as a string; (Optional) ```ascending```: If true sorts rows from least to greatest | Pandas dataframe or series|
| ```df.drop(columns = [list_of_column_names])``` | Removes all columns in ```list_of_column_names``` from ```df``` | ```list_of_column_names```: List of columns to drop | Pandas dataframe |
| ```df.dropna()``` or ```s.dropna()``` | Removes all rows containing missing values from ```df``` or ```s``` | None | Pandas dataframe or series with all rows containing missing values removed|
| ```df.dropna(axis = 1)``` | Removes all columns containing missing values from ```df``` or ```s``` | None | Pandas dataframe with all columns containing missing values removed|
| ```df.rename(axis = 1)``` | Removes all columns containing missing values from ```df``` or ```s``` | None | Pandas dataframe with all columns containing missing values removed|


Filtering

Merge
df.rename
pd.isnull() | Checks for null Values, Returns Boolean Arrray

df.group_by()



## Numpy

## Matplotlib
