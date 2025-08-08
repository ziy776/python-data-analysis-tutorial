# Python Data Analysis Tutorial

Last updated: **07-08-2025**

Welcome to this Python data analysis tutorial! This guide is designed for beginners and intermediate users who want to learn how to analyze, visualize, and model data using Python.

 [View this README in Chinese 中文版](README_zh.md)



## Contents
1. [Anaconda Environment Setup](01-anaconda-setup.md)

    - [Install Anaconda](01-anaconda-setup.md#install-anaconda)

    - Manage Environment
        - [View All Environments](01-anaconda-setup.md#view-all-environments)
        - [Create a New Environment (Command Line)](01-anaconda-setup.md#create-environment)
        - [Create Environment via GUI](01-anaconda-setup.md#creating-an-environment-via-the-graphical-interface)
        - [Activate the Environment](01-anaconda-setup.md#activate-the-environment)
        - [Start the Python Interpreter](01-anaconda-setup.md#start-the-python-interpreter)
        - [Exit the Python Interpreter](01-anaconda-setup.md#exit-the-python-interpreter)
        - [Deactivate the Environment](01-anaconda-setup.md#deactivate-the-environment)

2. [Data Operations](02-data-operations.md)

    - [Set Working Directory](02-data-operations.md#set-working-directory)

    - [Read and Save CSV Data](02-data-operations.md#read-and-save-csv-data)

    - Data Exploration and Inspection
        - [head() and tail()](02-data-operations.md#data-exploration-and-inspection)
        - [shape, columns, dtypes](02-data-operations.md#data-exploration-and-inspection)
        - [info()](02-data-operations.md#data-exploration-and-inspection)
        - [describe()](02-data-operations.md#data-exploration-and-inspection)

    - Selecting Rows and Columns
        - [Name-based Selection (loc)](02-data-operations.md#selecting-rows-and-columns)
        - [Position-based Selection (iloc)](02-data-operations.md#selecting-rows-and-columns)
        - [Conditional Filtering](02-data-operations.md#selecting-rows-and-columns)
        - [Multiple Conditions](02-data-operations.md#selecting-rows-and-columns)

    - Row and Column Operations
        - [Add Columns](02-data-operations.md#row-and-column-operations)
        - [Delete Columns](02-data-operations.md#row-and-column-operations)
        - [Rename Columns](02-data-operations.md#row-and-column-operations)
        - [Delete Rows](02-data-operations.md#row-and-column-operations)

    - Merging and Concatenation
        - [pd.concat()](02-data-operations.md#merging-and-concatenation)
        - [pd.merge()](02-data-operations.md#merging-and-concatenation)
        - [join() method](02-data-operations.md#merging-and-concatenation)

    - Data Type Conversion
        - [astype()](02-data-operations.md#data-type-conversion)
        - [pd.to_datetime()](02-data-operations.md#data-type-conversion)

    - Sorting and Removing Duplicates
        - [sort_values()](02-data-operations.md#sorting-and-removing-duplicates)
        - [sort_index()](02-data-operations.md#sorting-and-removing-duplicates)
        - [drop_duplicates()](02-data-operations.md#sorting-and-removing-duplicates)

    - Set Operations
        - [Difference, Intersection, Union, Symmetric Difference](02-data-operations.md#set-operations)
        - [Use Cases in Data Analysis](02-data-operations.md#set-operations)

    - Index Operations
        - [set_index()](02-data-operations.md#index-operations)
        - [reset_index()](02-data-operations.md#index-operations)
        - [.copy() method tip](02-data-operations.md#index-operations)

    - Grouping and Aggregation
        - [groupby() basics](02-data-operations.md#grouping-and-aggregation)
        - [Common aggregation functions](02-data-operations.md#grouping-and-aggregation)

    - Handling Missing Data
        - [Detect missing values](02-data-operations.md#handling-missing-data)
        - [Fill missing values](02-data-operations.md#handling-missing-data)
        - [Drop missing values](02-data-operations.md#handling-missing-data)