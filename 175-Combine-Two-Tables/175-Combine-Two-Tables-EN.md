# 175. Combine Two Tables

## Table of Contents
[Problem Summary](#problem-summary)
[Step 1: Understand the Problem](#step-1-understand-the-problem)
[Step 2: Break Down the Problem](#step-2-break-down-the-problem)
[Step 3: Design the Algorithm](#step-3-design-the-algorithm)
[Step 4: Define the Necessary Data Structures and Functions](#step-4-define-the-necessary-data-structures-and-functions)
[Step 5: Coding](#step-5-coding)
[Step 6: Optimization](#step-6-optimization)

## Problem Summary

**Tables:**
1. **Person Table:**
    - ```personId```(int): Primary key, unique for each person.
    - ```lastName```(varchar): Person's last name.
    - ```firstName```(varchar): Person's first name.

2. **Address Table:**
    - ```addressId```(int): Primary key, unique for each address.
    - ```personId```(int): The corresponding person’s ```personId```.
    - ```city```(varchar): City.
    - ```state```(varchar): State.

**Task:** For each person in the Person table, report their first name, last name, city, and state information. If a person does not have an address in the Address table, the city and state should be reported as ```null```.

### Step 1: Understand the Problem
We want to join two tables to get each person’s information. If a person does not have an address in the Address table, the city and state information should be ```null```. This is known as a left outer join (```LEFT JOIN```) in SQL and can be achieved using the ```merge``` function in pandas.

### Step 2: Break Down the Problem
1. **Join (Merge):** We will join the Person table with the Address table on the ```personId``` column.
2. **Select Columns:** After the join, we will select the ```firstName```, ```lastName```, ```city```, and ```state``` columns.
3. **Handle Missing Data:** For people without address information, the values will be ```null```.

### Step 3: Design the Algorithm
1. **Determine the Join Type:** We will use a left outer join (```left join```) as we want to include all records from the Person table.
2. **Specify Columns for Joining:** We will join on the ```personId``` column.
3. **Create the Result Table:** Select the required columns and drop unnecessary ones.

### Step 4: Define the Necessary Data Structures and Functions
- **Data Structures:**
    - ```person```: pandas DataFrame
    - ```address```: pandas DataFrame

- **Functions:**
    - ```pd.merge()```: To merge the DataFrames.
    - ```fillna()```: To fill missing values (optional – in our case, the missing values are automatically displayed as ```null``` without using ```fillna()```, and using it results in an error).

- **Data Types:**
    - ```personId```: int
    - ```lastName```, ```firstName```, ```city```, ```state```: varchar (string)

### Step 5: Coding
```py
import pandas as pd

def combine_two_tables(person: pd.DataFrame, address: pd.DataFrame) -> pd.DataFrame:
    """
    Combines the Person and Address tables to return 
    firstName, lastName, city, and state information for each person.
    For people without address information, city and state will be null.
    
    Args:
    - person (pd.DataFrame): Person table
    - address (pd.DataFrame): Address table
    
    Returns:
    - pd.DataFrame: Merged table
    """

    # Merge operation: Using left outer join (left join)
    merged_df = pd.merge(person, address, on="personId", how='left')

    # Selecting the required columns
    result_df = merged_df[['firstName', 'lastName', 'city', 'state']]

    # If we want to show missing values as 'null' (but it throws an error as output is "null" instead of direct null values):
    # result_df = result_df.fillna('null')

    return result_df
```


### Step 6: Optimization
Since this is a simple join operation, there is no need for further optimization. However, when dealing with large datasets, techniques such as indexing or pre-selecting specific columns can be used to improve performance.