# 2024_Olympic_Dashboard

The Paris 2024 Summer Olympics promise to be a grand event, and analyzing the related datasets can provide valuable insights into various aspects of the games. In this blog, we will explore how to use Python to download and manage the dataset from Kaggle and then utilize Power BI to visualize the insights for effective analysis.

This project involves several steps, from downloading the data to preparing it for visualization. Here’s a breakdown of the entire process:

#Step 1: Setting Up Kaggle API and Python Environment:
First, we need to set up the Kaggle API to access and download datasets. Follow these steps:

Sign up on Kaggle: If you don’t have a Kaggle account, sign up here.
Create an API Token: In your Kaggle account settings, go to the “API” section and click “Create New API Token.” This will download a kaggle.json file containing your credentials.
Save the API Token: Place the kaggle.json file in a secure directory on your machine, where it will be used to authenticate the Kaggle API.
Python Environment Setup
Make sure you have Python installed along with the necessary libraries:

pip install kaggle pandas

#Step 2: Python Script for Downloading the Dataset:
Below is the Python script that automates the process of downloading the Paris 2024 Olympic dataset from Kaggle and loading it into Pandas DataFrames for analysis.

import kaggle
import os
import pandas as pd

## Set Kaggle API credentials directory
os.environ['KAGGLE_CONFIG_DIR'] = 'C:/Users/tushar/.kaggle'  # Update this path to your Kaggle configuration directory

## Specify the dataset identifier
dataset = 'piterfm/paris-2024-olympic-summer-games'

## Set the download path
download_path = 'C:/Users/tushar/Downloads/Power BI_Imp Summary/Olympic/Source' # Change this to your preferred download directory

## Remove existing files in the folder to prevent duplicates or outdated files
for file in os.listdir(download_path):
    file_path = os.path.join(download_path, file)
    try:
        if os.path.isfile(file_path):
            os.unlink(file_path)  # Delete the file
            print(f"Deleted {file_path}")
    except Exception as e:
        print(f"Error deleting {file_path}: {e}")

## Download the dataset using the Kaggle API and unzip the files
kaggle.api.dataset_download_files(dataset, path=download_path, unzip=True)

## List of CSV files to be imported
csv_files = [
    'athletes.csv',
    'events.csv',
    'medallists.csv',
    'medals.csv',
    'medals_total.csv',
    'schedules.csv',
    'schedules_preliminary.csv',
    'teams.csv',
    'torch_route.csv',
    'venues.csv'
]

## Initialize a dictionary to hold DataFrames
dataframes = {}

## Iterate through each CSV file and load it into a DataFrame
for file in csv_files:
    ## Construct the full path to the CSV file
    file_path = os.path.join(download_path, file)
    
    ## Load the CSV file into a Pandas DataFrame
    df = pd.read_csv(file_path)
    
    ## Add the DataFrame to the dictionary using the file name as the key
    table_name = file.split('.')[0]  # Remove the .csv extension
    dataframes[table_name] = df
