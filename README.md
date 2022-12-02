# MSiA400-team8-2023

## Description
<to be filled later when project is clearly defined>

## Weekly Updates
### Oct 14th
Updates:
- Set up GitHub repository shared with 4 team members, TA, and Prof Diego
- Set up pgAdmin and Northwestern VPN to query data in the future
- Import four tables (everything except skuinfo.csv) into pgAdmin for our team
- Directly import deptinfo.csv, skstinfo.csv, and strinfo.csv into pgAdmin
- Reorder columns of trnsact.csv and import into pgAdmin
- Create initial area of interest for ML problem: regression analysis on product discount information (could change in the future) 
  
Next Steps:
- "Play" with the data (EDA with SQL)
- Reconfirm the ML problem
- Clean skuinfo.csv data to upload into pgAdmin next week
- Generate framework to perform EDA on the data

### Oct 21st
Updates:
- Generate two business areas/questions to investigate (will decide on one final idea)
- First, what kind of products need more discounts than others to be sold? What kind of products can be sold with little amount of discounts?
-> Could regress discount amount onto features (will think of as many features that can effect this)
-> Problem/concern: 1,425,811 transactions from 120 millions transactions have OrgPrice = $0 (we could remove them -> [some hint from TA would be nice :)])
- Second, What products can be combined together to create "bulk sale" with some discount (compare to summing all products' prices)?
-> ML ideas: clustering analysis or doing association rule on transaction table -> see which products get bought together. 
-> Problem/concern: hard to quantify the result (ROI) -> we could split transaction table into train and test by a point in time.
- SKU table: notice extra commas in color values for some rows -> filter out these rows and will fix by changing that special comma into backslash and add them back to the data (in the process of cleaning)

Next steps:
- EDA mainly transaction table
- try to clean and upload SKU table
- adapt business/ML problem from TA's comments

### Oct 28th
Updates:
- Populated SKU table 
- Successfully connect pgAdmin to jupyter notebook
- Perform EDA on transaction tables (mainly) and other table (not yet on skutable)
- EDA -> this week focus on discount price business problem (SQL-based EDA)
- Transaction table
  - 120M records
  - 52.6% of transactions have discount -> 2004 48% (46M), 2005 55% (74.6M)
  - 300k rows are problematic (original price lower than amount paid) -> will be removed
  - joining with strinfo
  - 29 states -> discount proportion ranging from 41% to 60% (IA and IL are the top two while AR is at the bottom) -> state might not be the primary feature (could be helpful in tree for interaction term) -> the actual discount avg ranges from 48.6% to 57% 
  - 327 zip code, discount proportion ranging from 35% to 88% (disregard zip with 100% and 1 transaction) -> could be a good feature -> the actual discount avg ranges from 34% to 69%
  - Most of the columns in transaction tables are categorical variables, so doing correlation plots is not super meaningful.
- SKST table
  - Conducted EDA on skst table (found out missing values, obtained first and second moments for each variable, drawing distribution graphs for numeric features and correlation visualizations)
  
Next Steps:
- Perform EDA for SKU table (also joining it with transaction table)
- Perform additional EDA on transaction table in a probabilistic approach (pandas-based -> histogram and join correlation plot with other tables)
- Perform EDA for the second business question (in case the first business question doesn't work out)
  
### Nov 4th
Updates:
SKU
  - 1.556m rows for sku table (after excluded 9k problematic rows)
  - ~70k distinct colors
  - ~2.6k distinct brand
  
Brand with transaction
  - Max average discount at $555 (right skewed)
  - log transformed -> range from -2 to 2.74
  - proportion of discount transaction ranges from 0 to 100 (some brand appears on transaction table only a few times -> might need to determine some cutoff, such as 10 transaction, to determine that some brand have small transactions and create another feature indicating low-transaction brands)
  
Others
  - cost in sksinfo ranges from 0 to 2700, retail ranges from 0 to 6017
  - There were 11629 stores had total orgprice of 0 (out of 714499 stores)
  - over 92.5% of the transaction had R type and 7.5 % had P type
  - Of all stores, there are 5029 stores where the average cost for that store is larger than the average retail price; there are 703 stores where the average cost for that store is equal to the average retail price; the remaining are those who are making positive profit.


Next Steps:
  - Feature Engineering
  - Try Regression models: Ridge/Lasso regresison or Random Forest
  
### Nov 11th  
Updates:
  - Perform feature engineering
  - features: states (dummy), zip code (~327 dummies in the entire data), brand (~2000 dummies), store (dummies), time (dummy month -> expecting Nov and Dec to have more discount transactions), Orgprice
  - Labels: Discount % (OrgPrice - AMT)/OrgPrice -> for regression, binary 1&0 for discount or not -> for classification problem
  - Point to ask TA/ get advices:
    -Some of the features have lots of dummy (such as brand), given that we have 120M transaction data, we are not sure whether having this much features (all the dummies) will be appropriate since we might not be able to use all 120M data point due to computation resources
    - We are debating whether we should use all 120M data or sample some of them to train the data for the ease of computation (and to not crash).
    - What's the most appropriate price to use for calculation. At the moment, we are using OrgPrice; however, we are debating that we can also use "retail" or "cost" columns.
  
Next Steps:
  - Perform correlation matrix or EDA to decide which problem to go for (regression vs classification)
  - Fit the initial model

### Nov 18th
Updates:
  
Feature Engineering
  - perform cluster on brands
  - feature -> log(avg retail price) and log(count occurrence in each store -> joining to skst table)
  - Generate 6 clusters:
    - 1 cluster: all brands that don't exist in skst table (262 samples)
    - 1 cluster: all brands that appear in skst table only once (103 samples) -> identify them as new brand to the market (peak in the histogram)
    - 4 clusters: divided the rest equally separated by Q1, median, and Q3 of log(avg retail price)
  
Modelling
  - Focus on classification problem first (which product offer discount)
  - Create skeleton code for logistic regression, random forest, and XGBoost
  - Sampling data from 120M rows without brand first
  
Next Steps:
  - Fit the model with and without brand features and investigate AUC
  - Efficiently sample data to fit the model
 
Dec 2nd
Updates
  - Fit models: logistic regression, random forest, and SVM
  - Started writing the report: introduction, EDA, feature engineering
Next Steps:
  - ROI analysis
  - update report: executive summary, modeling, ROI analysis, and conclusion (any additional part? any suggestion from the TA?)
