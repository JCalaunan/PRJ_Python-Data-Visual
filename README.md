# PRJ_Python-Data-Visual
Project to expand on Data wrangling process using Python with an emphasis on data visualizations for exploratory data analysis and the conclusive findings.

## Table of Contents (TOC)
* [Introduction](#introduction)
* [Initial Setup](#setup)
* [Global Functions](#functions)
* [Methodology](#method)
* [References](#references)

## Introduction
The project will primarily consist of two parts which demonstrate the use of data visualization in the data analysis process.
The dataset consist of loan data extracted from Prosper's database.
Part one of the project, reveals how visualizations during the exploratory data analysis (EDA) assist in the process by providing a high level overview of variable trends, potential relationships, what sectors of the dataset have inconsistencies. The visuals provide a roadmap that is easy to follow by others.

Part two of the project, shows the usefulness of visuals for use in presentations. They assist in the story telling process and help convey the message to the audience.

## Initial Setup
- pip install pandas
- pip install seaborn

## Global Functions
def sqrt_trans(x, inverse = False):
    if not inverse:
        return np.sqrt(x)
    else:
        return x ** 2

def log_trans(x, inverse = False):
    if not inverse:
        return np.log(x)
    else:
        return np.exp(x)

## Methodology:
1. Gather data
- [ ] Download, unzip 
- Read in provided CSV, from subfolder using pandas.
- Check file imported correctly.
- Create two copies, one backup of original and one to be cleaned.
- Review data dictionary and prepare to identify appropriate datatypes.

2. Data Wrangling
- Review size of dataset, data types and type change as required based on preliminary analysis of data dictionary. 
- LoanStatus and CreditGrade requiring data type modification to suit data dictionary definition.
- 



3. Exploratory data analysis
3.1 Univariate
3.2 Bivariate
3.3 Multivariate


4. Findings

5. Insights

## References:
### Udacity:
- [Counting Missing Data](https://classroom.udacity.com/nanodegrees/nd002/parts/9f7e8991-8bfb-4103-8307-3b6f93f0ecc7/modules/bc709f85-0ebb-45b8-907b-065adc25cbce/lessons/b86503df-e416-4f0e-9e2d-a7a3c08d0bc3/concepts/c33c9906-5be2-4c59-8012-eab668a50d3d)

### Docs:


### Misc:
- [Series equality test](https://stackoverflow.com/questions/42967848/how-to-subset-a-pandas-series-based-on-value)
- [text](link)

## To do:
1. Function to download files:
1.1 Prosper Loan Data, zip
https://s3.amazonaws.com/udacity-hosted-downloads/ud651/prosperLoanData.csv


1.1 Data dictionary
https://www.google.com/url?q=https://docs.google.com/spreadsheet/ccc?key%3D0AllIqIyvWZdadDd5NTlqZ1pBMHlsUjdrOTZHaVBuSlE%26usp%3Dsharing&sa=D&ust=1554486256024000
- Investigate whether programmatical download is available on Google Sheet provided links