# PRJ_Python-Data-Visual
Project to expand on Data wrangling process using Python with an emphasis on data visualizations for exploratory data analysis and the conclusive findings.
<br>
The project will primarily consist of two parts which demonstrate the use of data visualization in the data analysis process.
The dataset consist of loan data extracted from Prosper's database.
<br>
Part one of the project, reveals how visualizations during the exploratory data analysis (EDA) assist in the process by providing a high level overview of variable trends, potential relationships, what sectors of the dataset have inconsistencies. The visuals provide a roadmap that is easy to follow by others.
<br>
Part two of the project, shows the usefulness of visuals for use in presentations. They assist in the story telling process and help convey the message to the audience.
<br>
## Introduction- [PRJ_Python-Data-Visual](#prj_python-data-visual)
  - [Table of Contents (TOC)](#table-of-contents-toc)
  - [Introduction](#introduction)
  - [Initial Setup](#initial-setup)
  - [Load Dataset](#load-dataset)
    - [Google Colab remote](#google-colab-remote)
    - [Google Colab local host](#google-colab-local-host)
  - [Functions](#functions)
    - [FUNCTION TO PLOT VALS ALONG X-AXIS, NOMINAL VALS ON Y](#function-to-plot-vals-along-x-axis-nominal-vals-on-y)
    - [FUNCTION TO PLOT VALS ALONG Y-AXIS, NOMINAL VALS ON X](#function-to-plot-vals-along-y-axis-nominal-vals-on-x)
  - [Methodology:](#methodology)
  - [References:](#references)
    - [Udacity:](#udacity)
    - [Docs:](#docs)
    - [Misc:](#misc)
  - [To do:](#to-do)

## Initial Setup
- pip install pandas
- pip install seaborn
- pip install modin # used to import pandas and enabling multi-core


## Load Dataset
### Google Colab remote
from google.colab import drive
drive.mount('/content/drive')

* Google colab read csv
loans_raw = pd.read_csv('/content/drive/My Drive/Colab Notebooks/prosperLoanData.csv')


### Google Colab local host
* Local drive read csv
dir = '.../PRJ_Python-Data-Visual/'


## Functions
List of common functions used throughout.

### FUNCTION TO PLOT VALS ALONG X-AXIS, NOMINAL VALS ON Y
def yplot_values(gx, form):
    initialx = 0

    * Logic to print the proportion text on the bars
    for g in gx.patches:
        gx.text(g.get_width(), initialx + g.get_height()/4,
                form.format(g.get_width()),
                color='black',
                ha="left") 
        initialx+=1


### FUNCTION TO PLOT VALS ALONG Y-AXIS, NOMINAL VALS ON X
def xplot_values(gy, form):
    initialy = 0
    
    * Logic to print the proportion text on the bars
    for g in gy.patches:
        gy.text(initialy + g.get_width()/13, g.get_height(), 
        form.format(g.get_height()), 
        color='black',
        ha='center', # 'center', 'right', 'left'
        va='bottom') # 'top', 'bottom', 'center', 'baseline', 'center_baseline'
        initialy+=1


## Methodology:
1. Gather data
1.1 General process
- [ ] Download, unzip
- Read in provided CSV, from subfolder using modin.pandas.
- Check file imported correctly, checking info(), describe() and cross reference to data dictionary.
- Create two copies, one backup of original and one to be modified for analysis.
- Review data dictionary and prepare to identify appropriate datatypes.

1.1 Initial Scope
A summary of the variables of interest after reviewing the dataset, are listed below:

Variables of interest (19:
Categorical/Qualitative Types:
Nominal, no order [3]
- EmploymentStatus
- BorrowerState
- Occupation

Ordinal - variables have a specific order [3]
- CreditGrade
- ProsperScore
- ProsperRating (alpha) - similar to CreditGrade, rather then using numeric

Numerical/Quantitative Types: [6]
Discrete, numerical that can be measured
- IncomeRange
- Term
- CurrentDelinquencies
- BorrowerRate
- DebtToIncomeRatio
- MonthlyLoanRepayment

Continuous - e.g. time series [2]
- ListingCreationDate
- ClosedDate

GENERAL QUESTIONS OF INTEREST:
- 1. What affects a loan repayments interest rate?
- 2. What were the characteristics of individuals requiring a loan (i.e. occupation, income range)
- 3. There are two Prosper ratings that measure the loans level of risk, CreditGrade pre 2009, ProsperRating (alpha/numeric) and ProsperScore for loans post 2009. How do ProsperRating alpha and ProsperScore relate to one another? Why are there two measures?

2. Data Wrangling
2.1 Perform typical data wrangle steps:
- Review size of dataset, missing variables, data types and type change as required based on preliminary analysis of data dictionary.

2.1.1 Missing variables visual
- There are 42/81 variables in total with missing data. Some with numerous amounts. Columns affected with NA have been marked above with '*'.

2.1.2 Duplicate data check
- No duplicates were found.

2.1.3 Data types
- Date time data format corrected for ListingCreationDate. Similarly Year and Months extracted for loan start and close dates.
- CreditGrade and ProsperRating combined to limit Nan values.
- Ordinal categories are defined and set.

3. Exploratory data analysis
3.1 Analysis of the dataset
3.1.1 Nan Variables
Prior to the commencement of analysis of the above variables/columns. A pre check is to be performed to see the current state of the dataset, specifically the amount of columns that have missing variables.

3.1. Correlation between variables
A combination of a pairplot and a correlation heatmap lets us quickly analyse the variables and determine the correct numerical variables to investigate.
Due to the large quantity of observations, a sample of the population is taken to assist with keeping lower processing times.
There was 1 high and 2 moderately correlated variables from the analysis combined *Prosper Rating*, *Monthly Loan Payment* and *Listing Creation Date* respectively.
There is no linear relationship with Term, as the spread of ratings are present across the 3 terms, i.e 12, 36 and 60.
Generally there are a significant amount of deliquincies across the varying ratings, however there are no relationships 
The better ratings have lower rates generally < 20%, and then trend in rating types slowly spread out with increasing borrower rates.
The higher ratings reveal they have lower debts evident by the lower debt to income ratios. As the scores go lower the plots show an increase in debt evident by the slope.
No real relations with Monthly Loan Payments are apparent, apart from higher ratings plots being tighter and less spread out. 

3.2 What affects a loan repayments interest rate?
3.2.1 Borrower Rate:
- The violin plot stacked onto a box plot allows for the viewing of the data spread as well as the statistical information information such as the quartiles, min, max and medians.
- The histogram plot with the log transformation improves the clarity of low value observations not capture by the previous plot. 

3.2.2 EmploymentStatus:
- The hist plot and log transformation plot provides a clearer representation of the smaller *EmploymentStatus* counts.
- Creating a bivariate against the main variable (BorrowerRate) in question helps view the spread of employment types.
- A combined box and violin plot rather then creating subplots, thus saving space and allows the sharing of statistical information and the benefits of each plot.
- Occupations are the next variables that can be expanded after understanding the types of employment types available.

3.2.3 Occupation:
- The vertical histplot to provide a brief overview of the occupations that have applied for loans. Values were plotted to assist in visualising the results.
- A bar plot was chosen over a violin plot due to the compactness of the figure, which limits the view of the spread of the distribution that a violin plot offers.
- Occupations are broken into their respective sectors to limit the amount of values to be plotted. Variables excluded are plotted for completeness.
- The incomes of the respective occupations are the next logical variable to review to see how each occupations income compares against one another.

3.2.4 IncomeRange:
- Same plot types utilised for consistency, however with the inclusion of a facetgrid to analyse the occupations sampled previously back in Occupations.
- With the incomes analysed, the plot of monthly loan repayments and there respective terms are viewed next.

3.2.5 MonthlyLoanPayment:
- A histplot with a log transformation are the appropriate plots to initially determine the distribution of the variable in question.
- A multivariate plot of Occupations against Monthly Loan Payments and Term is used to understand the payments varying across different lengths.
- The jointplot provides a scatter plot not seen in the other plots, the right kde plot is a bivariate of the initial histplot in the section. The top kde plot however provides a bivariate plot of distribution for counts against term, not previously provided.

3.2.6 CreditRating / ProsperRating (numeric):
- A new consolidated column is created merging pre and post 2009.
- Another jointplot is repeated however the distribution is faceted against Credit Ratings, further explored with a FacetGrid to clearly visualise the distributions.
- A combined box and violin plot is utilised this time round to see how each occupation fares across the varying CreditRatings, where ProsperRatingNum is the numerical equivalent of CreditRating. This allows the display of statistical information i.e. median, etc.
- The results are further explored in a FacetGrid where Ratings against employment type are faceted against the subset of Occupations narrowed out previously.
- The remaining categorical variables will be explored.

3.2.7 BorrowerState:
- As there are a significant amount of States, the top X number of states in this case 9, have been generated to evenly distribute as a 3x3 on a FacetGrid.

3.2.8 DebtToIncomeRatio:
- A distribution of the numerical variable with a logarithmic transformation is used to show the low numerical values not seen in the previous pairplot.
- Investigation of ratios greater then 1, are filtered and reviewed.
- Minimal impact to BorrowerRate hence no indepth review.

3.2.9 ListingCreationDate and ClosedDate
- Investigations into the opening and closing dates are completed with a general histplot
- Minimal impact to BorrowerRate hence no indepth review.

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

2. Data Wrangling
2.1 Create new column employment sector. i.e. business, health, engineering, hospitality, law, etc.