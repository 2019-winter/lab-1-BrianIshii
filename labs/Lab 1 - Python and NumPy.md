---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.1'
      jupytext_version: 1.2.4
  kernelspec:
    display_name: Python 3
    language: python
    name: python3
---

# Name(s)
**Brian Ishii**


**Instructions:** This is an individual assignment, but you may discuss your code with your neighbors.


# Python and NumPy

While other IDEs exist for Python development and for data science related activities, one of the most popular environments is Jupyter Notebooks.

This lab is not intended to teach you everything you will use in this course. Instead, it is designed to give you exposure to some critical components from NumPy that we will rely upon routinely.

## Exercise 0
Please read and reference the following as your progress through this course. 

* [What is the Jupyter Notebook?](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/What%20is%20the%20Jupyter%20Notebook.ipynb#)
* [Notebook Tutorial](https://www.datacamp.com/community/tutorials/tutorial-jupyter-notebook)
* [Notebook Basics](https://nbviewer.jupyter.org/github/jupyter/notebook/blob/master/docs/source/examples/Notebook/Notebook%20Basics.ipynb)

**In the space provided below, what are three things that still remain unclear or need further explanation?**


**Is there package management with notebooks?**


## Exercises 1-7
For the following exercises please read the Python appendix in the Marsland textbook and answer problems A.1-A.7 in the space provided below.


## Exercise 1

```python
# Make an array a of size 6 × 4 where every element is a 2.

# YOUR SOLUTION HERE

import numpy as np

a =  np.ones((6,4), dtype=int) * 2
a
```

## Exercise 2

```python
# Make an array b of size 6 × 4 that has 3 on the leading diagonal and 1
# everywhere else. (You can do this without loops.)
#b[range(4),range(4)] = 3 works too

# YOUR SOLUTION HERE
b =  np.ones((6,4))
np.fill_diagonal(b, 3)
b
```

## Exercise 3

```python
# Can you multiply these two matrices together? Why does a * b work, but
# not dot(a,b)?

# YOUR SOLUTION HERE
print(a * b) # works

try:
    np.dot(a,b)
except:
    print("doesn't work")
    
# dot product doesn't work because it is matrix multiplication,
# and it requires num_col_a == num_row_b
```

## Exercise 4

```python
# Compute dot(a.transpose(),b) and dot(a,b.transpose()). Why are
# the results different shapes?
print(np.dot(a.transpose(),b))
print(np.dot(a,b.transpose()))
# YOUR SOLUTION HERE

# dot(a.transpose(),b)
# this is 4x6 * 6x4 => 4x4 matrix

# dot(a.transpose(),b)
# this is 6x4 * 4x6 => 6x6 matrix
```

## Exercise 5

```python
# Write a function that prints some output on the screen and make sure you
# can run it in the programming environment that you are using

# YOUR SOLUTION HERE
def func():
    print("Hello, World.")
    
func()
```

## Exercise 6

```python
# Now write one that makes some random arrays and prints out their sums,
# the mean value, etc.

# YOUR SOLUTION HERE
def random_matrix(size=4):
    matrix = np.random.rand(size)
    
    matrix.sum()
    print("Sum: " + str(matrix.sum()))
    print("Mean: " + str(matrix.mean()))
    
random_matrix()
```

## Exercise 7

```python
# Write a function that consists of a set of loops that run through an array
# and count the number of ones in it. Do the same thing using the where() function
# (use info(where) to find out how to use it).

# YOUR SOLUTION HERE

# check .shape element
# for i in zip(*inxs):
#     print(i)
def count_ones(array):
    count = 0
    for i in range(array.shape[0]):
        for j in range(array.shape[1]):
            if array[i][j] == 1:
                count += 1
    where_temp = len(np.where(b == 1)[0])

    return count

print((count_ones(a),len(np.where(a == 1)[0])))
print((count_ones(b),len(np.where(b == 1)[0])))

```

## Excercises 8-???
While the Marsland book avoids using another popular package called Pandas, we will use it at times throughout this course. Please read and study [10 minutes to Pandas](https://pandas.pydata.org/pandas-docs/stable/getting_started/10min.html) before proceeding to any of the exercises below.


## Exercise 8
Repeat exercise A.1 from Marsland, but create a Pandas DataFrame instead of a NumPy array.

```python
# YOUR SOLUTION HERE
import pandas as pd

a =  np.ones((6,4)) * 2
df_a = pd.DataFrame(a)
df_a
```

## Exercise 9
Repeat exercise A.2 using a DataFrame instead.

```python
# YOUR SOLUTION HERE
# can use iloc here
b =  np.ones((6,4))
np.fill_diagonal(b, 3)
df_b = pd.DataFrame(b)
df_b
```

## Exercise 10
Repeat exercise A.3 using DataFrames instead.

```python
# Can you multiply these two matrices together? Why does a * b work, but
# not dot(a,b)?

# YOUR SOLUTION HERE
df_a * df_b

try:
    np.dot(df_a, df_b)
except:
    print("doesn't work")
# dot product doesn't work because it is matrix multiplication,
# and it requires num_col_a == num_row_b
```

## Exercise 11
Repeat exercise A.7 using a dataframe.

```python
# Write a function that consists of a set of loops that run through an array
# and count the number of ones in it. Do the same thing using the where() function
# (use info(where) to find out how to use it).

# YOUR SOLUTION HERE
#use iloc instead of ==

def count_ones_df(df):
    count = 0
    for i in range(df.shape[0]):
        for j in range(df.shape[1]):
            if df.iloc[i][j] == 1:
                count += 1
    where_temp = len(np.where(b == 1)[0])

    return count

print((count_ones_df(df_a),len(np.where(df_a == 1)[0])))
print((count_ones_df(df_b),len(np.where(df_b == 1)[0])))
```

## Exercises 12-14
Now let's look at a real dataset, and talk about ``.loc``. For this exercise, we will use the popular Titanic dataset from Kaggle. Here is some sample code to read it into a dataframe.

```python
titanic_df = pd.read_csv(
    "https://raw.githubusercontent.com/dlsun/data-science-book/master/data/titanic.csv"
)
titanic_df
```

Notice how we have nice headers and mixed datatypes? That is one of the reasons we might use Pandas. Please refresh your memory by looking at the 10 minutes to Pandas again, but then answer the following.


## Exercise 12
How do you select the ``name`` column without using .iloc?

```python
## YOUR SOLUTION HERE
titanic_df["name"]
```

## Exercise 13
After setting the index to ``sex``, how do you select all passengers that are ``female``? And how many female passengers are there?

```python
## YOUR SOLUTION HERE
titanic_df.set_index('sex',inplace=True)

only_females = titanic_df.loc["female"]
titanic_df.reset_index(inplace=True)

print("Number of female passengers: " + str(len(only_females)))
only_females
```

## Exercise 14
How do you reset the index?

```python
## YOUR SOLUTION HERE
titanic_df.reset_index(inplace=True)
```
