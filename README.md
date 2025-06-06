# Task 1: Data Cleaning and Preprocessing - Customer Data

**Date:** 26/05/2025

**Company:** Elevate Labs

**Intern Name:** Angelina Nayak

**Dataset Used:**  <a href="Customer - Sheet1.csv">Customer - Sheet1.csv</a>
## Objective

The primary goal of this task was to perform essential data cleaning and preprocessing on a raw customer dataset using Python in a Jupyter Notebook. The aim was to address common data quality issues such as missing values and duplicate entries, preparing the data for further analysis.

## Cleaning and Preprocessing Steps Performed

I am cleaning data using Python in a Jupyter Notebook, and the dataset I am working with is <a href="Customer - Sheet1.csv">Customer - Sheet1.csv</a>

Here's a summary of the steps I have taken:

1.  **Dataset Upload & Kernel Setup:**
    * I uploaded the <a href="Customer - Sheet1.csv">Customer - Sheet1.csv</a> file to my Jupyter Notebook environment.
    * I opened a new Python kernel within my Jupyter Notebook and named it `task 1 elevate labs customer data`.
![image](https://github.com/user-attachments/assets/f8de408e-aabc-4972-847c-89af4738b763)


2.  **Library Imports:**
    I ran the following code block to import essential Python libraries:
    ```python
    #Libraries
    import pandas as pd
    import numpy as np
    from matplotlib import pyplot as plt
    import seaborn as sns

    #Ignore the warnings
    import warnings
    warnings.filterwarnings("ignore")
    ```
  ![image](https://github.com/user-attachments/assets/52e117d5-caed-4d97-aab5-c95edf840fcc)


3.  **Dataset Loading:**
    I successfully loaded `Customer - Sheet1.csv` into a Pandas DataFrame named `df` and displayed its contents.
    ```python
    df = pd.read_csv('Customer - Sheet1.csv')
    df
    ```
    This showed my DataFrame contained 2005 rows and 11 columns.
 ![image](https://github.com/user-attachments/assets/2ab1dc36-b3b9-4735-be93-ba5c9a4f2b4b)


4.  **Initial Data Information (`df.info()`):**
    I ran the following code to get a summary of my DataFrame, including data types and non-null counts:
    ```python
    df.info()
    ```
    The output indicated that the `Profession` column had 1970 non-null entries and the `Season` column had 1976 non-null entries, suggesting missing values in these columns.
   ![image](https://github.com/user-attachments/assets/4fa6d981-0d3b-471b-ac9a-f8ab6ab84691)


5.  **Column Header Verification:**
    I executed the following code to retrieve and display a list of all column headers to check for errors:
    ```python
    # We want to check all the column headers to avoid errors
    df = pd.DataFrame(df)
    df.head()
    column_list = list(df.columns)
    column_list
    ```
    The result confirmed the existing column names.
![image](https://github.com/user-attachments/assets/333d92de-0684-400f-973e-14c4b6a38b4c)


6.  **Drop 'Profession' Column:**
    I dropped the `Profession` column from the DataFrame, as it was not needed for data analysis, using this code:
    ```python
    #Drop the Profession column - not needed in data analysis
    df.drop(columns="Profession", inplace=True)
    df.head()
    ```
  ![image](https://github.com/user-attachments/assets/d4b4f53d-18a6-436a-b4a5-b1cbeb6817de)


7.  **Add 'Age Group' Column:**
    I created a new column named `Age Group` by categorizing the `Age` column into predefined bins using the following code:
    ```python
    df['Age Group'] = pd.cut(df['Age'], bins=[0, 18, 25, 35, 45, 55, 65, float('inf')],
                             labels=['Under 18', '18-24', '25-34', '35-44', '45-54', '55-64', '65+'],
                             include_lowest=True)
    ```
   ![image](https://github.com/user-attachments/assets/f91e421c-fe63-47d6-93b6-be8428b4c3b7)


8.  **Check for Missing Values (`df.isna().sum()`):**
    I ran the following code to check for N/A or null values in the DataFrame:
    ```python
    #check for N/A values
    df.isna().sum()
    ```
   ![image](https://github.com/user-attachments/assets/b3fe60b3-761c-4b93-bbf3-311aa780ddd4)


9.  **Drop Nulls in 'Season' Column:**
    I identified that the `Season` column had 29 null values and subsequently dropped the rows containing these nulls using this code:
    ```python
    #Drop N/A values in Season column
    df = df.dropna(subset = ["Season"])
    ```
  ![image](https://github.com/user-attachments/assets/e3841482-2007-4a07-a5ae-7adeb727562b)


10. **Check and Drop Duplicate Customer IDs:**
    I checked for duplicate `CustomerID` values using the code below, which reported 5 duplicate entries:
    ```python
    #Check the column for duplicates
    df.duplicated('CustomerID').sum()
    ```
    Following this, I dropped these duplicate rows, keeping only the first occurrence for each `CustomerID`, with this code:
    ```python
    df.drop_duplicates(subset = "CustomerID", inplace = True)
    df.duplicated('CustomerID').sum()
    ```
   ![image](https://github.com/user-attachments/assets/80415e69-ecab-4580-b87b-7bc94a00a5cc)


11. **Data Description (`df.describe()`):**
    I ran the following code to view descriptive statistics for the numerical columns (`CustomerID`, `Age`, `Purchase Amount`) in my cleaned dataset:
    ```python
    #Description of the data
    df.describe()
    ```
    The output of this command provided the count, mean, std, min, quartiles, and max for these columns.
   ![image](https://github.com/user-attachments/assets/b50183c8-1402-485c-9465-e83925ea9bd6)

12. **Save Cleaned Data to CSV:**
    After all cleaning operations were complete, I saved the final cleaned DataFrame to a CSV file on my local machine using the following code:
    ```python
    import os

    # Define the output folder path (adjust to your actual path)
    output_folder_path = r'C:\Users\nayak\Downloads\ELEVATE LABS\TASK 1'

    # Ensure the directory exists
    if not os.path.exists(output_folder_path):
        os.makedirs(output_folder_path)

    # Define the exact filename for the cleaned CSV (must match GitHub link)
    cleaned_file_name = 'Cleaned Customer Data Task 1 - Elevate Labs.csv'
    full_save_path = os.path.join(output_folder_path, cleaned_file_name)

    # Save the DataFrame to CSV, without the index
    df.to_csv(full_save_path, index=False)

    print(f"Cleaned dataset saved to: {full_save_path}")
    ```
![image](https://github.com/user-attachments/assets/c8ac8c3c-b60b-49d6-880f-d5f57c8b20e7)



## Deliverables for this Task

* <a href="task 1.pdf">Task File</a>: The original task file given by Elevate Labs.
* <a href="Customer - Sheet1.csv">Customer - Sheet1.csv</a>: The raw dataset used for this task.
* <a href="Cleaned Customer Data Task 1 - Elevate Labs.ipynb">Jupyter Notebook</a>: The Jupyter Notebook file containing all the Python code for data cleaning and preprocessing.
* <a href="Summary Task 1 - Elevate Labs.pdf">"Summary Task 1 - Elevate Labs.pdf</a>: This summary file, explaining the cleaning steps.
* <a href="Cleaned Customer Data Task 1 - Elevate Labs.csv">Cleaned Customer Data Task 1 - Elevate Labs.csv</a>: The csv file containing the cleaned data. 

## Conclusion

This task provided hands-on experience in identifying and resolving common data quality issues, utilizing Python's Pandas library for effective data manipulation. The result is a clean, structured dataset ready for further analytical insights.
![image](https://github.com/user-attachments/assets/70896f50-3c59-43a7-b9a9-11a0c4cacc3d)

