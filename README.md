# Analysis of Prosper Loan Data Set
## by: David Ugochukwu Asogwa


## Dataset
This data set contains 113,937 loans with 81 variables (in columns) on each loan, including loan amount, borrower rate (or interest rate), current loan status, borrower income, and many others. This data will be used for performing univariate, bivariate and multivarite analysis in order to answer questions like how loan amount is correlated with occpuation, loan payment and borrowing rate by different occupation and genders, correlation between active loans, completed loans and occupation and salary range and many more questions that will arise. Below is a description of the columns in this data set. Due do the enormous nature of the columns, only a few have been described in this exploratory analysis. A full description of the columns can be found in the variables description csv sheet.

1. ListingKey: Unique key for each listing, same value as the 'key' used in the listing object in the API.
2. ListingNumber: The number that uniquely identifies the listing to the public as displayed on the website.
3. ListingCreationDate: The date the listing was created.
4. CreditGrade: The Credit rating that was assigned at the time the listing went live. Applicable for listings pre-2009 period and will only be populated for those listings.
5. Term: The length of the loan expressed in months.
6. LoanStatus: The current status of the loan: Cancelled,  Chargedoff, Completed, Current, Defaulted, FinalPaymentInProgress, PastDue. The PastDue status will be accompanied by a delinquency bucket.
7. ClosedDate: Closed date is applicable for Cancelled, Completed, Chargedoff and Defaulted loan statuses. 

The data was not clean as observed from assessing programmatically and manually. A lot of issues was detectd and fixed. These issues are as listed below:
1. Inconsistent column names.
2. Convert ListingCreationDate data type to datetime, extract the year into `list_year` with data type category.
3. Drop rows with duplicate values in the ListingKey column.
4. Change terms to short, medium and long in Term column, and change data type to categorical.
5. Convert ClosedDate to datetime, extract year into `closed_year`, fill empty cells with `ongoing` and convert to category data type.
6. Replace missing states with unknown, and change all names to their full names.
7. Replace missing values in occupation with other
8. Replace missing values in employment status with `unknown` and convert to category data type
9. Rename listingCatergory (numeric) to listing_category, change numeric values to their actual values and convert to category
10. Rename IsBorrowerHomeowner to homeowner
11. In DebtToIncomeRatio, replace missing cells with the value of the column.
12. Convert LoanOriginationDate data type to datetime, extract the year into `origin_year` with data type category.
13. Creat new column: `days`, which is the number of days from listing to origination. Subtract origination date from listing date.
14. Drop unnecessary columns to avoid information overload.
15. Rename all necessary columns for easy readablility, and save master data set


## Summary of Findings

On exploring individual features of the dataset, different observations were made, some were clear on the spot but other's needed further deep dive to get a better understanding of the distribution of the datset. The loan_amount data appeared to be right skewed with a single peak in the histogram chat, but on further exploration by varying the bin size, there apeeared to be several peaks at different intervals, though still right skewed and tailed towards the end, the change in bin size gave a clearer view of the distribution.

The monthly_payment showed similar behaviour as the loan_amount but this time had only a single peak and right skewed also. The monthly_income showed the most strange behaviour among the datasets as the distribution only showed a single bar using default settings. Diving down into the feature by collecting random samples (100, 1,000, 10,000) showed the distributions behaviour was better observed. Most borrower's are low income earners as seen from the sample with 100 and 1,000 data. Increasing the sample size showed there are outlier values of huge monthly_income.

Looking into the number of days from listing to originating a loan, it was observed that most loans take between 0 to 25 days to go from listing to origination. The loan term showed that the medium term loans are the most in which borrowers apply for. This is followed by the long term and short term loans.

Performing univariate exploration on the features, a strong positive corrrelation was observed between loan amount and the monthly payment made. An increase in the loan amount increases the monthly payment. There's also a strange behaviour in the dataset: it has three divisions which cannot be explained at this point. Probably a relationship between other features in the dataset.

Exploring the listing year with the loan term, it is observed that the medium term loan is the most preferred loan by borrowers over the years. The short term loan had few borrower's, followed by the long term loan. I was also found out that employed and full-time borrowers are favoured more while retired and non-employed borrowers have the least chance of getting a loan.



## Key Insights for Presentation

Income_verifiable feature having a True or False value is not evenly distributed over the years. It is pertinent to say that borrower's with verifiable income source have a higher possibility of getting a loan. Non verified borrower's obtained the highest loan in 2013 with only 1.971% of the total loan that year compared to 28.80% given to verified borrower's.

Employed borrower's favour medium term loans to long term and short term loans, though the long term loan have a high percentage than short term loan. Full-time workers also favour medium term loans. In general, the medium term loan is favoured in all, this might be as a result of the percentage interest paid or the purpose in which the loan is used for.

Having established a strong positive correlation between loan amount and monthly payment, adding an extra feature, term, to it shows another relationship. The is also a strong positive correlation between these features and aside that, it is observed that the short term loans have higher payments, followed by the medium term and long term loans. This might be as a result of the time interval needed to payup the loan amount, that is, short term loans having the  time frame of 12 months requires a higher payment in order to complete it within the time frame. But long term loan with 60 months payment period will be paid in smaller bits. From the plot, it is seen also that the maximum short term loan amount is about 25,000 dollars.
