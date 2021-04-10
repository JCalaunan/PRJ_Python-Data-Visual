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

## Global 
### Functions
#### FUNCTION TO PLOT VALS ALONG X-AXIS, NOMINAL VALS ON Y
def yplot_values(gx, form):
    initialx = 0
	
    # Logic to print the proportion text on the bars
    for g in gx.patches:
        gx.text(g.get_width(), initialx + g.get_height()/4,
                form.format(g.get_width()),
                color='black',
                ha="left") 
        initialx+=1

#### FUNCTION TO PLOT VALS ALONG Y-AXIS, NOMINAL VALS ON X
def xplot_values(gy, form):
    initialy = 0
    
    # Logic to print the proportion text on the bars
    for g in gy.patches:
        gy.text(initialy + g.get_width()/13, g.get_height(), 
        form.format(g.get_height()), 
        color='black',
        ha='center', # 'center', 'right', 'left'
        va='bottom') # 'top', 'bottom', 'center', 'baseline', 'center_baseline'
        initialy+=1
		
### Variables
ticks_Borrow_low = np.arange(0, loans_df.BorrowerRate.max()+0.02, 0.02)
ticks_Borrow_high = np.arange(0, loans_df.BorrowerRate.max()+0.05, 0.05)
ticks_range_MLP = np.arange(0, loans_df.MonthlyLoanPayment.max()+200, 200)

.set(xticks = xticks_range_MLP)
g1.set(xticks = xticks_range_Borrow)

## Methodology:
1. Gather data
1.1 General process
- [ ] Download, unzip
- Read in provided CSV, from subfolder using pandas.
- Check file imported correctly, checking info(), describe() and cross reference to data dictionary.
- Create two copies, one backup of original and one to be modified for analysis.
- Review data dictionary and prepare to identify appropriate datatypes.


1.1 Initial Scope
A summary of the variables of interest after reviewing the dataset, are listed below:

Variables of interest (19:
Categorical/Qualitative Types:
Nominal, no order
- EmploymentStatus *
- BorrowerState *
- Occupation *
[3]
Ordinal - variables have a specific order
- CreditGrade ***
- ProsperScore *
- ProsperRating (alpha) - similar to CreditGrade, rather then using numeric
[3]
Numerical/Quantitative Types:
Discrete, numerical that can be measured
- IncomeRange
- Term
- CurrentDelinquencies *
- BorrowerRate
- DebtToIncomeRatio
- MonthlyLoanRepayment
[6]
Continuous - e.g. time series
- ListingCreationDate
- ClosedDate *
[2]


GENERAL QUESTIONS OF INTEREST:
- 1. What affects a loan repayments interest rate ()?
- 2. What factors affected the success of a loan being approved?
- 3. What were the characteristics of individuals requiring a loan (i.e. occupation,)
- 4. There are two Prosper ratings that measure the loans level of risk, CreditGrade pre 2009, ProsperRating (alpha/numeric) and ProsperScore for loans post 2009. How do ProsperRating alpha and ProsperScore relate to one another? Why are there two measures?


Q: - ProsperScore was introduced to better highlight

2. Data Wrangling
2.1 Perform typical data wrangle steps:
- Review size of dataset, missing variables, data types and type change as required based on preliminary analysis of data dictionary.

2.1.1 Missing variables visual
- There are 42/81 variables in total with missing data. Some with numerous amounts. Columns affected with NA have been marked above with '*'.

2.1.2 Duplicate data check
- No duplicates were found.

2.1.3 Data types
- CreditGrade contains NaN and NC otherwise considered to be Nan and requires modification. Replacing NaN with N/A results in NC converting into Nan
**- ListingCreationDate is an object and needs conversion into datetime
- ListingCategory is an int, however data dictionary better describes the representation of the numbers i.e. 0 = N/A. Column to be changed and values to be amended.

2.1.4 ListingCategory (numberic)
- Convert numbers ranging from 0-20 to the appropriate category per the datadictionary
**

3. Exploratory data analysis
3.1 What affects a loan repayments interest rate ()?
3.1.1 Univariate - Stacked histogram plot
EmploymentStatus
- Generally there is a peak at ~0.33% with a majority of the borrow rates are around 0.15 or 15%, evident with the two peaks.
- Indicates loans are provided primarily to 'Employed' followed by Full-time.

3.1.2 Bivariate
EmploymentStatus:
- As above however the transformation provides clearer representation of the smaller EmploymentStatus. Clearly showing 'Retired' as the lowest, followed by Part-time and surprisingly 'Not Employed' in ascending order.
BorrowerState:
- As there are a significant amount of States, the top X number of states, in this case 5, have been generated.

3.3 Multivariate
Pairplot
3.3.1 ProsperScore
- Term: There is no linear relationship with Term, as the spread of Scores are present across the 3 terms, i.e 12, 36 and 60.
- CurrrentDelinquincies: Generally there are a significant amount of deliquincies across the varying ProsperScores, however there are no relationships 
- BorrowerRate: The ProsperScores of 10 have lower rates generally < 20%, whereas the scores of 1 are mainly spread from 15% to 40%. The scores inbetween slightly decrease 
- DebtToIncomeRatio: The higher ProsperScores reveal they have lower debts evident by the lower ratios. As the scores go lower the plots show an increase in debt evident by the slope.
- MonthlyLoanRepayment: No real relations apparent apart from higher ProsperScore plots being tighter and less spread out. 

BorrowerState
- State # 5 contains the most number of loans.

3.2


4. Findings

5. Insights

## References:
### Udacity:
- [Counting Missing Data](https://classroom.udacity.com/nanodegrees/nd002/parts/9f7e8991-8bfb-4103-8307-3b6f93f0ecc7/modules/bc709f85-0ebb-45b8-907b-065adc25cbce/lessons/b86503df-e416-4f0e-9e2d-a7a3c08d0bc3/concepts/c33c9906-5be2-4c59-8012-eab668a50d3d)
- [Exploratory vs. Explanatory Analyses](https://classroom.udacity.com/nanodegrees/nd002/parts/9f7e8991-8bfb-4103-8307-3b6f93f0ecc7/modules/bc709f85-0ebb-45b8-907b-065adc25cbce/lessons/728cb608-ddd4-48d6-9dea-d355a99524c3/concepts/87aa9106-ba97-412c-b092-a485f879a9fa)

### Docs:
- [Seaborn barplot](https://seaborn.pydata.org/generated/seaborn.barplot.html)
- [Matplotlib list of colors](https://matplotlib.org/3.1.0/gallery/color/named_colors.html)
- [Matplotlib specifying colors](https://matplotlib.org/3.1.0/tutorials/colors/colors.html)
- [Series Sort Values](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.Series.sort_values.html)
- [Dataframe Drop Column](https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.drop.html)
- [String Format](https://www.w3schools.com/python/ref_string_format.asp)

### Misc:
- [Series equality test](https://stackoverflow.com/questions/42967848/how-to-subset-a-pandas-series-based-on-value)
- [Value on Seaborn graph](https://medium.com/@dey.mallika/transform-your-graphs-with-seaborn-ea4fa8e606a6)
- [Set alpha/transparency on violinplot](https://github.com/mwaskom/seaborn/issues/622)
- [Set transparency on boxplot](https://github.com/mwaskom/seaborn/issues/979)
- [Seaborn major grid lines](https://stackoverflow.com/questions/33541085/control-gridline-spacing-in-seaborn)
- [Seaborn change palette to specific explicit colors](https://cmdlinetips.com/2019/04/how-to-specify-colors-to-scatter-plots-in-python/)
- [Rotate xticks on x-axis](https://github.com/mwaskom/seaborn/issues/1853)
- [Joint plot axis changer](https://stackoverflow.com/questions/34209140/setting-the-axes-tick-values-of-a-seaborn-jointplot)
- [Multiple if conditions](https://stackoverflow.com/questions/48872234/using-apply-in-pandas-lambda-functions-with-multiple-if-statements)
- [Seaborn colormap](https://stackoverflow.com/questions/62884183/trying-to-add-a-colorbar-to-a-seaborn-scatterplot)

## To do:
1. Function to download files:
1.1 Prosper Loan Data, zip
https://s3.amazonaws.com/udacity-hosted-downloads/ud651/prosperLoanData.csv


1.1 Data dictionary
https://www.google.com/url?q=https://docs.google.com/spreadsheet/ccc?key%3D0AllIqIyvWZdadDd5NTlqZ1pBMHlsUjdrOTZHaVBuSlE%26usp%3Dsharing&sa=D&ust=1554486256024000
- Investigate whether programmatical download is available on Google Sheet provided links