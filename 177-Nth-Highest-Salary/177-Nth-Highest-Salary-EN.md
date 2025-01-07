# 177. Second Highest Salary

## Table of Contents

- [177. Second Highest Salary](#177-second-highest-salary)
  - [Table of Contents](#table-of-contents)
  - [Problem Summary](#problem-summary)
  - [Step 1: Understand the Problem](#step-1-understand-the-problem)
  - [Step 2: Break Down the Problem](#step-2-break-down-the-problem)
  - [Step 3: Design the Algorithm](#step-3-design-the-algorithm)
  - [Step 4: Define the Necessary Data Structures and Functions](#step-4-define-the-necessary-data-structures-and-functions)
  - [Step 5: Coding](#step-5-coding)
  - [Step 6: Optimization](#step-6-optimization)

## Problem Summary

**Tables:**

1. **Employee Table:**

    -   `id`(int): A unique identifier for each employee.
    -   `salary`(int): Represents the employee's salary.

**Task:** Find the second highest distinct salary from the `Employee` table. If there is no second highest salary, return `null` (`None` in Pandas).

## Step 1: Understand the Problem

-   **Input:** `Employee` table (columns: `id` and `salary`).
-   **Output:** The second highest distinct salary. If there is only one unique salary or no data, return `null`.

## Step 2: Break Down the Problem

1. **Find the distinct salaries:** First, we need to get all distinct salaries.
2. **Sort:** Sort these unique salaries in descending order.
3. **Select the second highest salary:** Pick the second element from the sorted list.
4. **Return the result:** Return the second highest salary if it exists, otherwise return `null` (`None`).

## Step 3: Design the Algorithm

1. Get the distinct salaries.
2. Sort the salaries in descending order.
3. Select the second element.
4. Return `None` if there is no second element.

## Step 4: Define the Necessary Data Structures and Functions

-   **Data Structures:**
    -   `employee`: pandas DataFrame

-   **Functions:**
    -   `drop_duplicates()`: To get unique values.
    -   `nlargest()`: To get a certain number of largest values.
    -   `sorted()`: To sort values.
    -   `len()`: To get the number of elements in a list.

## Step 5: Coding

```python
import pandas as pd

def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:
    """
    Finds the Nth highest distinct salary from the Employee table.
    Returns null (None) if there is no Nth highest salary.

    Args:
    - employee (pd.DataFrame): Employee table
    - N (int): Which highest salary to find

    Returns:
    - pd.DataFrame: A DataFrame containing the Nth highest salary
    """
    # Find unique salaries, sort them in descending order, and select the Nth largest salary
    # Step 1 & 2: Get distinct salaries and sort them in descending order
    sorted_salaries = employee['salary'].drop_duplicates().nlargest(N)

    # Step 3 & 4: Select the Nth highest salary and return it as a DataFrame
    if len(sorted_salaries) == N:
        # If the Nth largest salary exists, get it
        nth_salary = sorted_salaries.iloc[N - 1]
        return pd.DataFrame({'getNthHighestSalary({})'.format(N): [nth_salary]})
    else:
        # If the Nth largest salary does not exist, return None
        return pd.DataFrame({'getNthHighestSalary({})'.format(N): [None]})
```

**Example:**
```py
# Code that calls the Second Highest Salary function and returns the result for N=2
def second_highest_salary(employee: pd.DataFrame) -> pd.DataFrame:
    """
    Finds the second highest distinct salary from the Employee table.
    Returns null (None) if there is no second highest salary.

    Args:
    - employee (pd.DataFrame): Employee table

    Returns:
    - pd.DataFrame: A DataFrame containing the second highest salary
    """
    return nth_highest_salary(employee, 2)
```

## Step 6: Optimization
Using the nlargest() function is already quite efficient for this problem. The nlargest() function is optimized for finding the N largest values and is faster than sorting the entire dataset. For even larger datasets, we can further reduce the processing time by dividing the data into chunks and applying nlargest() to each chunk.