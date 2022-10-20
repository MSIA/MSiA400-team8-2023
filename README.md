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
