# (Prosper Loans Dataset Exploration)
## by Jian Carlo CALAUNAN

## Dataset

Project to expand on Data wrangling process using Python with an emphasis on data visualizations for exploratory data analysis and the conclusive findings.
<br>
The project will primarily consist of two parts which demonstrate the use of data visualization in the data analysis process.
The dataset consist of loan data extracted from Prosper's database.
<br>
Part one of the project, reveals how visualizations during the exploratory data analysis (EDA) assist in the process by providing a high level overview of variable trends, potential relationships, what sectors of the dataset have inconsistencies. The visuals provide a roadmap that is easy to follow by others.
<br>
Part two of the project, shows the usefulness of visuals for use in presentations. They assist in the story telling process and help convey the message to the audience.
<br>

> Provide basic information about your dataset in this section. If you selected your own dataset, make sure you note the source of your data and summarize any data wrangling steps that you performed before you started your exploration.

## Methodology

GENERAL QUESTIONS OF INTEREST:
- 1. What affects a loan repayments interest rate?
- 2. What were the characteristics of individuals requiring a loan (i.e. occupation, income range)
- 3. There are two Prosper ratings that measure the loans level of risk, CreditGrade pre 2009, ProsperRating (alpha/numeric) and ProsperScore for loans post 2009.


## Summary of Findings

1. Data types
- CreditGrade contains NaN and NC otherwise considered to be Nan and requires modification. Replacing NaN with N/A results in NC converting into Nan
- ListingCreationDate is an object and needs conversion into datetime
- ListingCategory is an int, however data dictionary better describes the representation of the numbers i.e. 0 = N/A. Column to be changed and values to be amended.

2. Nan Variables
Prior to the commencement of analysis of the above variables/columns. 
A pre-check is to be performed to see the current state of the dataset, specifically the amount of columns that have missing variables.

3. Numerical variable correlations
A combination of a pairplot and a correlation heatmap lets us quickly analyse the variables and determine the correct numerical variables to investigate.
- Due to the large quantity of observations, a sample of the population is taken to assist with keeping lower processing times.
- There was 1 high and 2 moderately correlated variables from the analysis combined *Prosper Rating*, *Monthly Loan Payment* and *Listing Creation Date* respectively.
- There is no linear relationship with Term, as the spread of ratings are present across the 3 terms, i.e 12, 36 and 60.
- Generally there are a significant amount of deliquincies across the varying ratings, however there are no relationships.
- The better ratings have lower rates generally < 20%, and then trend in rating types slowly spread out with increasing borrower rates.
The higher ratings reveal they have lower debts evident by the lower debt to income ratios. As the scores go lower the plots show an increase in debt evident by the slope.
- No real relations with Monthly Loan Payments are apparent, apart from higher ratings plots being tighter and less spread out. 

4. Categorical Variables
4.1. EmploymentStatus
- Generally there is a peak at ~0.33% with a majority of the borrow rates are around 0.15 or 15%, evident with the two peaks.
- Indicates loans are provided primarily to 'Employed' followed by Full-time.
- As above however the transformation provides clearer representation of the smaller EmploymentStatus. Clearly showing 'Retired' as the lowest, followed by Part-time and surprisingly 'Not Employed' in ascending order.

4.2. BorrowerState:
- As there are a significant amount of States, the top X number of states, in this case 5, have been generated.


## Key Insights for Presentation

> Select one or two main threads from your exploration to polish up for your presentation. Note any changes in design from your exploration step here.

- There are a significant amount of values missing for particular variables.
- Generally the borrow rates from Prosper show a multi modal distribution with the vast majority approximately around 8% to 22%.
- Excluding employed and other employment statuses, generally borrow rates favoured full-time, part time, retired then self-employed loanees.
- Loanees with higher income ranges generally had the best borrow rates.
- Key occupations had better borrow rates then other, a vast majority had varying borrow rates evident by the large IQR's.