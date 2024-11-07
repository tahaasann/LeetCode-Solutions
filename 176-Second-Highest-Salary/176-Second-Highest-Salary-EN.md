# 176. Second Highest Salary

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
1. **Employee Table:**
    - ```id```(int): A unique identifier for each employee.
    - ```salary```(int): Represents the employee's salary.
    

**Task:** Find the second highest distinct salary from the Employee table. If there is no second highest salary, return ```null``` (```None``` in Pandas).

### Step 1: Understand the Problem
- Input: Employee table (columns: id and salary).
- Output: The second highest distinct salary. If there is only one unique salary, return ```null```.

### Step 2: Break Down the Problem
1. Find the distinct salaries: First, we need to get all distinct salaries.
2. Sort: Sort these unique salaries in descending order.
3. Select the second highest salary: Pick the second element from the sorted list.
4. Return the result: Return the second highest salary if it exists, otherwise return ```null``` (None).

### Step 3: Design the Algorithm
1. Get the distinct salaries.
2. Sort the salaries in descending order.
3. Select the second element.
4. Return ```None``` if there is no second element.

### Step 4: Define the Necessary Data Structures and Functions
- **Data Structures:**
    - ```employee```: pandas DataFrame

- **Functions:**
    - ```unique()```: To get unique values.
    - ```sort_values()```: To sort values.
    - ```iloc[]```: To access values at a specific index.
    - ```shape```: To check DataFrame dimensions.

### Step 5: Coding
```py
import pandas as pd

def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    """
    Finds the second highest distinct salary from the Employee table.
    Returns null (None) if there is no second highest salary.
    
    Args:
    - employee (pd.DataFrame): Employee table
    
    Returns:
    - pd.DataFrame: A DataFrame containing the second highest salary
    """
    
    # Step 1: Get the distinct salaries
    unique_salaries = employee['salary'].unique()
    # Using 'unique()' to get unique values from the 'salary' column
    
    # Step 2: Sort the unique salaries in descending order
    sorted_salaries = sorted(unique_salaries, reverse=True)
    # Using 'sorted()' to sort the salaries
    # 'reverse=True' for sorting in descending order
    
    # Step 3: Select the second highest salary
    if len(sorted_salaries) >= 2:
        second_highest = sorted_salaries[1]
        # If there are at least two distinct salaries, select the second element
    else:
        second_highest = None
        # If there is only one unique salary, assign 'None'
    
    # Step 4: Return the result as a DataFrame
    # Creating a DataFrame to return the result in the desired format
    result = pd.DataFrame({
        'SecondHighestSalary': [second_highest]
    })
    
    return result
```

### Step 6: Optimization
The algorithm is already efficient for this simple problem. However, for larger datasets, different techniques can be used to improve performance. For example, using the ```nlargest()``` function to get only the top two distinct salaries.

**Usage**:
```py
    # Step 1: Get distinct salaries and sort them in descending order
    sorted_salaries = employee['salary'].drop_duplicates().nlargest(2)
    # Using 'drop_duplicates()' to get unique salaries
    # Using 'nlargest(2)' to get the top two salaries
```