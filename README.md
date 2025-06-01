# Retail-Store-Sales-Dashboard
Analysis of products, product categories, sales, customer data and dates.

### Table of Content
- [Project Overview](#project-overview)
- [Data Source](#data-source)
- [Tools](#tools)
- [Data Cleaning and Preperation](#data-cleaning-and-preperation)
- [Questions for Data Analysis](#questions-for-data-analysis)
- [Dashboard](#dashboard)
- [Results and Findings](#results-and-findings)
- [Challanges in Analysis](#challanges-in-analysis)

### Project Overview
In this data analysis report, I focus on deriving insights from a detailed data set based on sales of consumer goods in a retail store. Through a comprehensive analysis of this dataset, I aim to identify sales and purchasing patterns, identify top customers and products contributing to revenue, detect sales seasonality and high demand periods and understand price elasticity and optimize pricing strategies.

### Data Source
The dataset used for this project is named [Retail Store Sales Transactions (Scanner Data)](https://www.kaggle.com/datasets/marian447/retail-store-sales-transactions/data) and can be found on Kaggle along with my [notebook](https://www.kaggle.com/code/yarsmi/y-s-retail-store-sales-transactions-eda) with my version of exploratory data analysis. The data includes information such as value of goods, quantities sold, IDs of goods and transactions and more thorough the physical period of 2016.

### Tools
The tools I used to complete this project are:
- **MS Excel**: 
  - Used to clean data from the source file.
- **Power BI**: 
  - Further clean data such as changing Date table format.
  - Visualize data through tables and charts.
  - Create measures and tables to make calculations.
  - Use Python visual tables for Python specific calculations and analysis.
  - Construct the final dashboard for presentation.
- **Kaggle**:
  - Download dataset
  - Created my own notebook to perform Python data cleaning and data visualization to help with the overall analysis.
  - Compared results to other analysis entries from other users.

 ### Data Cleaning and Preperation
- Loaded data from source file.
- Data inspection and cleaning.
  - Reviewing and changing data formats and values (i.e. Changed Date table to DD/MM/YYYY format), removing duplicate values and removing error cells.
- Created a calculated column for individual unit prices by dividing Sales_Amount by Quantity_Sold.
- Added column title to Order_ID (previously blank).
- Unchecked a SKU_ID that totaled itself to 1.47E+02.
- Filtered out rows with NULL/0 order count.
- Removed Quantity_Sold cells that included a decimal (a fraction of an item).
- Through Power Query Editor, I further cleaned data by changing the value type of tables from Decimal Number to Whole Numbers.
- Cleaned all table data types in Power Query Editor inside Power BI to the respective type. (Unit_Price into $, Date to Date format, IDs into integers, SKU_ID to strings...).

### Questions for Data Analysis
- Identify top customers and products contributing to revenue.
- How many customers are Champions in the RFM Segmentation Analysis?
- Understand customer purchasing patterns.
- Detect sales seasonality and high-demand periods.
- Find the most profitable SKU categories.
- Understand price elasticity and optimize pricing strategies.

### Dashboard
My interactive dashboard can be [viewed](https://app.powerbi.com/links/NuaXN5Hx_f?ctid=bcb5764e-ead9-4a1b-a125-348f0e65f5eb&pbi_source=linkShare&bookmarkGuid=663305f4-0775-4364-89c5-870c72fadbcb) or [download](https://github.com/yarosmi/Retail-Store-Sales-Dashboard/raw/4a87ce4e4c00bd98ac46de1bdd869095320a53c2/Retail_Store_Sales_Dashboard%20-%20Yaraslau%20Smirnou.pbix) the Power Bi file to look at the dashbaord is broader detail.
It contains 5 main pages with data, charts and tables and navigation along extras such as Python graphs, Drill-Through Pages and Tooltip pages.
![Capture 1](https://github.com/yarosmi/Retail-Store-Sales-Dashboard/blob/4a87ce4e4c00bd98ac46de1bdd869095320a53c2/Retail%20Store%20Sales%20Analysis%20Page%201.png)

### Results and Findings
I performed analysis for each column in the database. Here are the results and findings:

**Time-Series Analysis**
- Peak sales days, months, or seasons.
  - Peak sales of the year are led by Q4 having $415.55 in revenue due to the holiday season and Q1 having the lowest sales of $360.52 in revenue.
- Daily, weekly, and monthly trends.
  - 29 of the 31 days of the months are producing at least $40,000 consistently and peaking just over $60,000 on day 12, 14 and 22 which could relate to promotions, sales or holidays. The lowest earning days are day 1 and 31 due to not every month ending on day 31 and reflection from low beginning of month promotions. 
  - Trends for this retail store have similar time series trends that coincide with consumer shopping behavior with Q4 around Christmas time having the highest sales of the year due to the holiday season and gift giving activities within families. Q4 had the highest sales of the year with $8650.64 peaking during the whole year on December 16 but there are notable high spikes within each of other yearly quarters such as $8100+ peaking on Q1 at Mach 18, May 13 with almost $7900 and September 22 with over $8000 with back to school season. 
- Comparing performance year-over-year or month-over-month.
  - When looking at best performing months, December made $150,229.95 in sales due to the holidays, September came in 2nd with $148,227.18 in sales most likely due to back-to-school season and lastly, May with $142,155.20 in sales due to spring and summer time shipping trends.
- Weeks of year sales heatmap.
  - Looking at the heatmap based on most profitable weeks of the year, the most potent income weeks are week 51, 39, 29, 52 and 38. Those have the highest income ranges of the year by weeks.

**Customer Segmentation**
- RFM Analysis (Recency, Frequency, Monetary)
  - To prepare the data for RFM analysis, I created new measurements in the main Rscanner_data table to calculate Recency, Frequency and Monetary values. I got Recency using DATEDIFF command (to find how many days has been since last purchase from today) on Last_Transaction_Date that used MAXX syntax to figure out he most recent transaction from each customer id. Frequency was calculated using DISTINCTCOUNT on Transaction_ID to count individual orders per customer id. And I calculated Monetary by first SUMming Sales_Amount and Quantity_Sold individually and then dividing Total Sales_Amount by Total Quantity_Sold. 
  - To get the score of each segment I used the PERCENTILE.INC command to create 5 levels per segment by 20% increments by the value from the R, F, M Values tables. I then had to import a whole new dataset table with Customer Segments, the scores they are corresponding to and the index for easy organization I found online that are used in the retail and marketing industry. I had to edit the relationship of the data to link the “Scores” table from the import table with the RFM_Total_Scores table from the RFM table I created to see which segment will be given to which customer based on the RFM measures.
  - Using a pie chart to filter through segmented customers, the largest segment is **Potential Loyalist** at 3830 customers or 16.7% of all customers. This is a good baseline to have because these customers are familiar with your store and have made recent purchases in moderate frequency and spending.
  - Store’s best customers – **Champions** have 8.52% of the pie chart with 1299 Customers. They are the store’s best customers with recent, frequent and high value purchases. **While Cannot Lose Them** segment consists of 10.33% or 2370 customers, data suggest they need incentives to increase their frequency of visits. **Loyal** segment accounts for 12.73% or 2290 customers. They are similar to the best segments with frequent and high value spending but also struggle from recency. Use similar action with incentivizing to keep their business.
  - **At Risk** customers are counted for 12.94% or about 2970 people and **About to Sleep** 6.39% or 1460 people. The statistics in these segments indicate churn risk. They will eventually stop shopping at our retail store. At risk customers had high RFM scores previously but haven’t purchased recently. They need a boost with promotions. About To Sleep customers are still shopping but losing interest and will also benefit from certain promotion to keep them incentivized.
  - **New Customers** (7.95%/1,820 people) and **Promising** (6.39%/1470 people) both have high recency but need to increase their frequency and spending. They have potential to become higher ranked and are need of nurturing with promotions.
  - **Hibernating** (4.49%/1030 people) and **Lost Customers** (7.53/1730 people) are least engaged and is a gamble to re-engage. They have lost interest and your business but could be won back with strategic advertisements. Probably more impactful to use the ad budgets for New Customers.
  - **Summary**: Every segment is divided in a similar range of % but are dominated by Potential Loyalists, Hibernating and Promising customers. There is a strong foundation on steady income with Loyal and Potential Loyal customers and room to grow with New and Promising Customers. < br / >
![RFM Segments](https://github.com/user-attachments/assets/2514a18a-2290-49d7-a38c-149de7867ab8)
- Identifying high-value customers and churn risks.
  - **At Risk** customers are counted for 12.94% or about 2970 people and **About to Sleep** 6.39% or 1460 people. The statistics in these segments indicate churn risk. They will eventually stop shopping at our retail store. At risk customers had high RFM scores previously but haven’t purchased recently. They need a boost with promotions. About To Sleep customers are still shopping but losing interest and will also benefit from certain promotion to keep them incentivized.
  - **Champions** have 8.52% of the pie chart with 1.95 Customers. They are the store’s best customers with recent, frequent and high value purchases. While **Cannot Lose Them** segment consists of 10.33% or 2.370 customers, data suggest they need incentives to increase their frequency of visits. **Loyal** segment accounts for 12.73% or 2290 customers. They are similar to the best segments with frequent and high value spending but also struggle from recency. Use similar action with incentivizing to keep their business.
- Tracking repeat customers vs. one-time buyers.
  - Of all 22.6K unique customers, 27.85% (6.3K) shoppers were single time customers. They made a purchase and didn’t go back. The other 72.15% (16.3K) shoppers made more than one purchase at the retail store and are considered to be Repeat Buyers. This a good sign that more than 2/3s of all buyers went back for another purchase.

**Transaction Insights**
- Calculating average transaction value.
  - By dividing Total Sales Amount by Number of Transactions I was able to get the average transaction value that is made in the store of $11.98. Comparing this to average transaction amount of $56.14 in all of North America in 2016, this is rather low. But there are factors to consider that we don’t know such as the store type on location, age of comapny or if it’s a franchise.
- Analyzation of the distribution of transaction values.
  - According to a scatter plot between Sales_Amount and Customer_ID, Majority of transactional values are under $200 with only 28 transactions being above $300 and 1 outlier of $707.73.
- Tracking number of transactions per day and month.
  - From all of 131,706 transactions during 2016, the peak months in number of transactions were September with 12.256 orders, December with 12,200 orders and May with 12,009 orders which reflect the seasonal demand timeframes. January and February has the lowest transaction counts with 10,115 and 9,941 most likely due to post holiday and back to school seasonal spending.
  - 12th day of the months has the most orders with 5149 and day 31 has the lowest order amount with just 2008. This suggest people like to shop in the middle of the months and sales drop of by each end of the month.

**Category-Level Insights**
- Analyzing revenue and quantity sold by category.
  - From the top 10 categories contributing to revenue, only 1 breaks the $100k mark with ID 6BZ making $114,061.33. Spot 2 (SJS) and 3 (LPF) make $85,142.31 and 84,921.91. After when the revenue per category takes a step decline with $54K (ID OXH) doing to $34.7K (ID R6E) at 10th spot. The top 10 categories alone are contributing to $576,305.39 of the overall $1,578,038.62 revenue amount for the 2016 physical year.
  - Comparing top categories by quantity sold, only 2 categories sold over 10,000 units. JI5 with 13,194 and N8U with 12,148. Those are outliers because #3 and below ranked categories don’t even come close to 9000 units sold. #3 category LPF sold 8212 units the trendline decreases with each unit after. 
- Identify top-performing and low-performing categories.
  - By revenue, top performing category is 6BZ with $114,061.33 income and top selling category is JI5 with 13,194 unit sold.
  - By revenue, lowest performing category is R6E with only $34,784.59 income and lowest selling categories are tied with OTK and QON with both having only 1 unit sold each.
Comparing the popularity of categories over time.
  - Comparing top 10 categories by their quantity sold, there are noticeable outliers in popularity fluctuation. These categories display spikes on certain dates suggesting a use of promotional material, seasonal demand or specific events that are driving these units to move. Category U5F in cyan has noticeable peaks during the summer season with its highest quantity sold and peaking during the fall and winter season after that. Further examining categories such as JI5 in salmon color, it experiences similar peaks to U5F un the summer, fall and winter months but with more consistent falling and rising interest from consumers with profitable unit sold quantities. Taking a look at XG4 in light blue color, it seems to have frequent sales peaks through the year but more prominent quantity sold in Q3 and 4. Unlike GI5, it has harsher fall of periods in popularity during its off seasons in sales. Some categories stay consistent throughout the year such as categories R6E in deep cyan and N8U in deep purple. They remain relatively stable but lower but consistent volume sold, indicating steady and less variable demand of its products. H8O in dark blueish grey experiences its highest peak in July and few other peaks in Q3 and 4.
![Sku Category Popularity](https://github.com/user-attachments/assets/1cc4a563-cdc7-4995-b115-b0395e2f9996)


**Product-Level Insights**
- Ranking SKUs by revenue and quantity sold.
  - The top sku by revenue can be considered an outlier. SKU ID 3YDVF generated $29,419.35 in revenue in 2016, while in #2 spot, SKU ID LJ26I generated only $13,571.45 in revenue. The trendline decreases until it levels out at the cheapest sku of N5Sn2 generating $0.03 of revenue.
  - Of the total 195,561 units sold, the top sku by quantity sold is CKDW0 with 5769 units. In 2nd place there is sku TD3DD with 3786 units sold and ID UNJKW with 2179 units sold. After these the units, sold quantitates don’t go above 1600 units and gradually decrease until they get to ID 05ZN9 and 13 other IDs with 0 units sold.
- Identifying slow-moving products and top sellers.
  - Since we don’t have restocking information of each sku id or category id such as periodical stock levels, I will use DATEFIFF command to figure out how many days has it been since last purchase of a sku to determine slow selling skus. Based of retail store industry standards, a product that haven’t moved for 90 days is considered slow selling is the baseline for my analysis. And the date I am comparing the 90 days to is January 1, 2017 since this data is based on the whole year of 2016.
  - Based on the data, this retail store holds 5228 distinct skus of products and 1492 of them are counted as slow-moving due to 90 or more days since last sale. There are 11 that have entered the slow-moving stage because they are right on 90 days straight without a sale on Jan 1, 2017. Those SKU_IDs are: 0QPT3,1MV2N,29C7J,2OM6Q,4YFUH,6JXC8,9EUNP, BT7WJ, C9IXZ, EH5KR and IFG8D. It is a good idea to promote them for a little bit if they still have demand with advertising push or a discount. There are also 6 products that haven’t been purchased for the entire year since Jan1, 2016. Those product skus are: 0WX4V, 7UQEH, DZ6D5, DWHGV, KCTLH and UBJZ9. It is worth removing those products from the store’s inventory to make space for products that are selling faster in 90 days.
- Analyzing price elasticity by observing how changes in price affect sales.
  - In order to get price elasticity, I had to calculate change in price by percentage. I did that by subtracting minimum unit price from maximum unit price and then dividing that number by minimum price and multiplying by 100 to get the final % of change in price for each sku. Then I calculated the percent change in quantity sold by doing the same formula but with quantity sold data. And finally, to find the price elasticity for each sku I divided % in quantity change by $ change in price. 
  - Looking at the data, majority of products that didn’t receive adjustment in price through the physical year, stayed at a 0.00 or a 1.00 elasticity which indicates perfect inelasticity or just had no effect from sku price change. 
  - Sorting in descending order from the highest price change in the data of $62.63 for the sku EROH1, the elasticity went down only 0.9% with 3 units sold to just 1. This is expected for most products as they are following the normal consumer behavior. Similarly, with VUBGF and E3T4K have the 2nd and 3rd largest price changes but show low price elasticity due to customers being less sensitive to their price adjustment, also meaning they are price inelastic.
  - There are rare instances of skus like JSLMY and 5IINF showing a high elasticity score with a significant price change. JSLMY’s price increased from $8.98 to $42.72 while selling 19 more units at the higher price. This could indicate sales from seasonal demand, promotions, or product bundling. Similar situation happened with sku H15DO that received a $15,57 price hike from $15.55 to $31.12 and sold 23 more units at the new price while only 1 at the old price.
  - Negative price elasticity is mostly standard in units pricing with demand going down with higher prices. This evident with YV4DN where the price changed from $31.12 with 6 units sold to $48.26 and sold only 1 unit. This pattern appears on most negative elastic prices. But there are instances like QHOC9 where an increase in price can increase sales. This sku got a $28.61 price increase and sold 9 units whereas only 2 units were sold at the old price.
  - While most of the products that had a 0 or 1 elasticity change didn’t also didn’t have a change in price, there are a few anomalies or errors in the data where the calculations could be in fractions and show extreme values such as for sku 09K06 where is has a price elasticity of -21,625.08 with a $0.00 price change. On a scatter plot chart comparing Unit Price and Quantity Sold are shown displays 5 different plots for the same sku within the same $117.96 value.
![Price Elasticity](https://github.com/user-attachments/assets/ad2483af-8868-4fa7-9a81-6ac0005a5505)


**Demand Analysis**
- Identifying high-demand products and categories.
 - Certain products show a consistent demand throughout the whole year. SKU ID such as CKDW0 consistently sells 100+ units a day throughout majority days of month. But it’s one of a few SKUs that peaks at 300 and 400+ units sold on certain days. Another notable SKU ID is MXKDP that doesn’t have as high peaks but has no drop of points and consistently sell 28 at lowest and with a peak of 98 on majority of the year with no low sales days expect the 1st month of the year where it has no sales at all. It’s a strong contender for steady income. CYRX4 is the last notable SKU with it having a steady increase in demand for the first 5 months of the year and a constant demand of around 80 units through the rest of the year. With its consistency Q2 and up can be considered solid performance.
  - For categories, JI5 has frequent spikes in demand through the year. With up to 288 units sold in a single day and a range of between 100-200 units sold at every months for multiple days. H8O is also another notable category for high demand where it has also has frequently consistent peaks of selling 100 units and lows of 2 units a day. But it has the highest peak at over 400 units in July.
- Tracking quantity sold trends over time.
  - Looking a line chart of quantity sold over time suggest that products will always sell between 100 units at the lowest and 1000 units at peak with the exception of Christmas time with 1200 units. There are consistent peaks in majority days that are in the middle of the month and lowest sales being in later and early days of a month. And there is a subtle trend of increase in overall volume sold over the year. Promotions are encouraged to scale lower demand SKUs for increased statistics.
- Detecting anomalies and outliers (e.g., unusually high or low sales).
  - Unusually high sale price occurred with sku ID E3T4K with a sale price of $322.23. This was the most expensive single item purchase in this data set and can be considered an outlier. Another outlier is sku ID 09K06 with a unit price of 117.96. It sits well outside of the clusters because it was purchased 6 times in that order.

**Revenue Analysis**
- Calculating total, average, and median revenue.
  - Total revenue in 2016 was $1,578,038.62.
  - Average sale value is $11.98.
  - Median transaction value is $6.92
- Examining revenue contribution by customer.
  - Majority of customers contribute relatively small sales with amounts ranging below $1,000. There are frequent spikes but rarely exceed $2000. This indicated a large number of customers with a low individual revenue contribution. But there is a significant cluster of customers with much higher amounts spiking to $4000. This group includes top revenue contributor. 
  - The customer revenue chart is right-skewed where the high spending customers are. Those are within the 15K-20K of customer IDs.
- Tracking changes in revenue over time.
  - Revenue throughout the day to day of the year is consistent. Lowest revenue in a day was 503.88 at the end of Q1 and highest revenue in a day was $8650.64 in Q4. The daily revenue trendline has a consistent pattern with its peaks and dip. After every peak there is a small dip to the similar peak and then a dip to the average lowest sales and then it repeats. This suggests weekly sales retailers put out. All of high peaks are over $5000 in sales throughout the year.

**Price Analysis**
- Calculating unit price for each product.
  - Created a calculated column for individual unit prices by dividing Sales_Amount by Quantity_Sold.
- Analyzing how price variations affect sales volumes.
  - The highest price change happened with sku EROH1 with a $62.63 going from $8.03 to $70.66. The price elasticity is 0.09 because although it didn’t have large quantity sold from the old price the units sold went from 3 to 1 which demonstrates the traditional sales pattern of increase prices causes lower sales. There are several examples of this in this dataset such as 4FT32 that when from $1.90 and 113 units sold to $2.15 with only 26 units sold. It has a negative elasticity from a $0.25 price adjustment. There is an extreme case of price elasticity sensitivity where sku HYDRJ dropped from 33 units sold to 2 from a $0.01 change. Its elasticity score is -1,557.52. It could have been a niche product that was purchased only by a specific group of people and was on the verge of losing customers. Or in case of sku BLH3I, the product sells from 28 units from the lowest price of $2.86 to 114 units from a $0.01 price change. Again, it could depend on the seasonality or how niche a product is.
  - Another theory that is tested here is the theory of price going up as the product gets more popular. This is seen with the sku JSLMY that has only 1 unit sold at $8.98 and sold 20 units at $42.72 with and elasticity score of 5.06. Once people catch on with a product, the demand increases and the production cost increases to keep up with supply.
  - There are a number of products that sold only 1 unit at the lowest price and selling 573 units at its highest price (sku QGK3S) after it raised $1.06. This could have been an essential everyday item and it needs to be bought regardless of price. Also, sku GB05L got a price adjustment of $0.78 and sold 1 unit at its lowest price and 344 at its highest.
  - Products with no price change don’t experience any elasticity as predicted.
- Detecting pricing anomalies or errors.
  - A notable pricing anomaly I noticed while looking at the price changes in sku-ids is ID EROH1 where it went up by $62.63 at one point. The minimum price was only $8.03 on May 11 and at some points the maximum price increased to $70.66 where a sale was made July 12. There is a suggestion of supply and demand but it’s very unusual for it to increase so much so I would look out for this error in future analysis. 
  - A similar instance where a sku E3T4K increased in price by $44.61/ not as bad as EROH1 but still enough to raise a red flag. E3T4K cost 277.62 on April 10 and had an increase in price at July 17 to 322.23.
  - Error that occurred in pricing is that there were few hundred entries with Sales_Amount and Unit_Price that had 0 units sold. Those could have been errors or product returns but I filtered the data without them

### Challanges in Analysis
- When Saving and Loading the data from Power Query Editor into my worksheet, there were 80,000+ errors in the Date table. So every date cell had an error due to it trying to sort date cells from a CSV format. In the original data, the date format was Month/Day/Year, but the format that was in my files was Day/Month/Year. So Power BI didn’t try to calculate days into months so every cells with days past 12 were counted a months and thus gave an error. I tried creating separate columns to segment days, months and year to convert the date into text but the opposite effect was happening so the correct dates before day of 12 (which are counted as months in my file) were getting the error. How I was able to fix this was to convert all Date table using Locale and setting the table to Date format into English (United Kingdom) formator of MM/DD/YYYY.
-	Had to do the same thing in Kaggle to format DD/MM/YYYY. With format='%d/%m/%Y' in Python.
-	I had trouble figuring out if a calculation needed a new measure or column. Often times I just created both because creating calculation needed one or the other and I hard time figuring out which ones.
-	I filtered Quantity_Sold on all pages of the dashboard to filter orders greater than 0 to remove error orders that was in the original data that had sales number but with 0 quantity sold.
- Most time consumer challanges were learning new analysis methods sych as RFM Segmentation of customers and foguring out the calculations and proper tables to use for calclating. I have have used this method before in makreting so i had to learn this strategy from sratch.






