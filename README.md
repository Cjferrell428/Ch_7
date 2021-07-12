# Ch_7

Create a Web Application for an ETF Analyzer
In this Challenge assignment, you’ll build a financial database and web application by using SQL, Python, and the Voilà library to analyze the performance of a hypothetical fintech ETF.

Instructions:

Use this notebook to complete your analysis of a fintech ETF that consists of four stocks: GOST, GS, PYPL, and SQ. Each stock has its own table in the etf.db database, which the Starter_Code folder also contains.

Analyze the daily returns of the ETF stocks both individually and as a whole. Then deploy the visualizations to a web application by using the Voilà library.

The detailed instructions are divided into the following parts:

Analyze a single asset in the ETF

Optimize data access with Advanced SQL queries

Analyze the ETF portfolio

Deploy the notebook as a web application

Analyze a Single Asset in the ETF
For this part of the assignment, you’ll use SQL queries with Python, Pandas, and hvPlot to analyze the performance of a single asset from the ETF.

Complete the following steps:

Write a SQL SELECT statement by using an f-string that reads all the PYPL data from the database. Using the SQL SELECT statement, execute a query that reads the PYPL data from the database into a Pandas DataFrame.

Use the head and tail functions to review the first five and the last five rows of the DataFrame. Make a note of the beginning and end dates that are available from this dataset. You’ll use this information to complete your analysis.

Using hvPlot, create an interactive visualization for the PYPL daily returns. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.

Using hvPlot, create an interactive visualization for the PYPL cumulative returns. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.

Optimize Data Access with Advanced SQL Queries
For this part of the assignment, you’ll continue to analyze a single asset (PYPL) from the ETF. You’ll use advanced SQL queries to optimize the efficiency of accessing data from the database.

Complete the following steps:

Access the closing prices for PYPL that are greater than 200 by completing the following steps:

Write a SQL SELECT statement to select the dates where the PYPL closing price was higher than 200.0.

Using the SQL statement, read the data from the database into a Pandas DataFrame, and then review the resulting DataFrame.

Select the “time” and “close” columns for those dates where the closing price was higher than 200.0.

Find the top 10 daily returns for PYPL by completing the following steps:

Write a SQL statement to find the top 10 PYPL daily returns. Make sure to do the following:

Use SELECT to select only the “time” and “daily_returns” columns.

Use ORDER to sort the results in descending order by the “daily_returns” column.

Use LIMIT to limit the results to the top 10 daily return values.

Using the SQL statement, read the data from the database into a Pandas DataFrame, and then review the resulting DataFrame.

Analyze the ETF Portfolio
For this part of the assignment, you’ll build the entire ETF portfolio and then evaluate its performance. To do so, you’ll build the ETF portfolio by using SQL joins to combine all the data for each asset.

Complete the following steps:

Write a SQL query to join each table in the portfolio into a single DataFrame. To do so, complete the following steps:

Use a SQL inner join to join each table on the “time” column. Access the “time” column in the GDOT table via the GDOT.time syntax. Access the “time” columns from the other tables via similar syntax.

Using the SQL query, read the data from the database into a Pandas DataFrame. Review the resulting DataFrame.

Create a DataFrame that averages the “daily_returns” columns for all four assets. Review the resulting DataFrame.

Hint Assuming that this ETF contains equally weighted returns, you can average the returns for each asset to get the average returns of the portfolio. You can then use the average returns of the portfolio to calculate the annualized returns and the cumulative returns. For the calculation to get the average daily returns for the portfolio, use the following code:

etf_portfolio_returns = etf_portfolio['daily_returns'].mean(axis=1)
You can use the average daily returns of the portfolio the same way that you used the daily returns of a single asset.

Use the average daily returns in the etf_portfolio_returns DataFrame to calculate the annualized returns for the portfolio. Display the annualized return value of the ETF portfolio.

Hint To calculate the annualized returns, multiply the mean of the etf_portfolio_returns values by 252.

To convert the decimal values to percentages, multiply the results by 100.

Use the average daily returns in the etf_portfolio_returns DataFrame to calculate the cumulative returns of the ETF portfolio.

Using hvPlot, create an interactive line plot that visualizes the cumulative return values of the ETF portfolio. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.

Deploy the Notebook as a Web Application
For this part of the assignment, complete the following steps:

Use the Voilà library to deploy your notebook as a web application. You can deploy the web application locally on your computer.

Take a screen recording or screenshots to show how the web application appears when using Voilà. Include the recording or screenshots in the README.md file for your GitHub repository.

Review the following code which imports the required libraries, initiates your SQLite database, popluates the database with records from the etf.db seed file that was included in your Starter_Code folder, creates the database engine, and confirms that data tables that it now contains.
# Importing the required libraries and dependencies
import numpy as np
import pandas as pd
import hvplot.pandas
import sqlalchemy
​
# Create a temporary SQLite database and populate the database with content from the etf.db seed file
database_connection_string = 'sqlite:///etf.db'
​
# Create an engine to interact with the SQLite database
engine = sqlalchemy.create_engine(database_connection_string)
​
# Confirm that table names contained in the SQLite database.
engine.table_names()
['GDOT', 'GS', 'PYPL', 'SQ']
Analyze a single asset in the FinTech ETF
For this part of the assignment, you’ll use SQL queries with Python, Pandas, and hvPlot to analyze the performance of a single asset from the ETF.

Complete the following steps:

Write a SQL SELECT statement by using an f-string that reads all the PYPL data from the database. Using the SQL SELECT statement, execute a query that reads the PYPL data from the database into a Pandas DataFrame.

Use the head and tail functions to review the first five and the last five rows of the DataFrame. Make a note of the beginning and end dates that are available from this dataset. You’ll use this information to complete your analysis.

Using hvPlot, create an interactive visualization for the PYPL daily returns. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.

Using hvPlot, create an interactive visualization for the PYPL cumulative returns. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.

Step 1: Write a SQL SELECT statement by using an f-string that reads all the PYPL data from the database. Using the SQL SELECT statement, execute a query that reads the PYPL data from the database into a Pandas DataFrame.
# Write a SQL query to SELECT all of the data from the PYPL table
query = "Select * From PYPL"
​
# Use the query to read the PYPL data into a Pandas DataFrame
pypl_dataframe = pd.read_sql_query(query, con=engine)
​
Step 2: Use the head and tail functions to review the first five and the last five rows of the DataFrame. Make a note of the beginning and end dates that are available from this dataset. You’ll use this information to complete your analysis.
# View the first 5 rows of the DataFrame.
pypl_dataframe.head()
​
time	open	high	low	close	volume	daily_returns
0	2016-12-16 00:00:00.000000	39.90	39.90	39.12	39.32	7298861	-0.005564
1	2016-12-19 00:00:00.000000	39.40	39.80	39.11	39.45	3436478	0.003306
2	2016-12-20 00:00:00.000000	39.61	39.74	39.26	39.74	2940991	0.007351
3	2016-12-21 00:00:00.000000	39.84	40.74	39.82	40.09	5826704	0.008807
4	2016-12-22 00:00:00.000000	40.04	40.09	39.54	39.68	4338385	-0.010227
# View the last 5 rows of the DataFrame.
pypl_dataframe.tail()
​
time	open	high	low	close	volume	daily_returns
994	2020-11-30 00:00:00.000000	212.51	215.83	207.0900	214.200	8992681	0.013629
995	2020-12-01 00:00:00.000000	217.15	220.57	214.3401	216.520	9148174	0.010831
996	2020-12-02 00:00:00.000000	215.60	215.75	210.5000	212.660	6414746	-0.017827
997	2020-12-03 00:00:00.000000	213.33	216.93	213.1100	214.680	6463339	0.009499
998	2020-12-04 00:00:00.000000	214.88	217.28	213.0100	217.235	2118319	0.011901
Step 3: Using hvPlot, create an interactive visualization for the PYPL daily returns. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.
# Create an interactive visualization with hvplot to plot the daily returns for PYPL.
pypl_dataframe['daily_returns'].hvplot(x= "time", xlabel= "days", ylabel = "daily returns", title = "PYPL Daily Returns")
​
Step 4: Using hvPlot, create an interactive visualization for the PYPL cumulative returns. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.
# Create an interactive visaulization with hvplot to plot the cumulative returns for PYPL.
(1+pypl_dataframe["daily_returns"]).cumprod().hvplot(x="time", xlabel="Time", ylabel="Cumulative Returns", title="PYPL Cumulative Returns")
​
Optimize the SQL Queries
For this part of the assignment, you’ll continue to analyze a single asset (PYPL) from the ETF. You’ll use advanced SQL queries to optimize the efficiency of accessing data from the database.

Complete the following steps:

Access the closing prices for PYPL that are greater than 200 by completing the following steps:

Access the closing prices for PYPL that are greater than 200 by completing the following steps:

Write a SQL SELECT statement to select the dates where the PYPL closing price was higher than 200.0.

Select the “time” and “close” columns for those dates where the closing price was higher than 200.0.

Using the SQL statement, read the data from the database into a Pandas DataFrame, and then review the resulting DataFrame.

Find the top 10 daily returns for PYPL by completing the following steps:

Write a SQL statement to find the top 10 PYPL daily returns. Make sure to do the following:

Use SELECT to select only the “time” and “daily_returns” columns.

Use ORDER to sort the results in descending order by the “daily_returns” column.

Use LIMIT to limit the results to the top 10 daily return values.

Using the SQL statement, read the data from the database into a Pandas DataFrame, and then review the resulting DataFrame.

Step 1: Access the closing prices for PYPL that are greater than 200 by completing the following steps:
- Write a SQL `SELECT` statement to select the dates where the PYPL closing price was higher than 200.0.

- Select the “time” and “close” columns for those dates where the closing price was higher than 200.0.

- Using the SQL statement, read the data from the database into a Pandas DataFrame, and then review the resulting DataFrame.
# Write a SQL SELECT statement to select the time and close columns 
# where the PYPL closing price was higher than 200.0.
query = """ SELECT time , close
FROM PYPL
WHERE close > 200.0
"""
​
​
# Using the query, read the data from the database into a Pandas DataFrame
pypl_higher_than_200 = pd.read_sql_query(query, con=engine)
​
# Review the resulting DataFrame
pypl_higher_than_200
​
time	close
0	2020-08-05 00:00:00.000000	202.920
1	2020-08-06 00:00:00.000000	204.090
2	2020-08-25 00:00:00.000000	201.710
3	2020-08-26 00:00:00.000000	203.530
4	2020-08-27 00:00:00.000000	204.340
5	2020-08-28 00:00:00.000000	204.480
6	2020-08-31 00:00:00.000000	203.950
7	2020-09-01 00:00:00.000000	208.920
8	2020-09-02 00:00:00.000000	210.820
9	2020-09-03 00:00:00.000000	205.070
10	2020-10-12 00:00:00.000000	201.500
11	2020-10-13 00:00:00.000000	207.730
12	2020-10-14 00:00:00.000000	203.660
13	2020-10-15 00:00:00.000000	203.170
14	2020-10-16 00:00:00.000000	204.540
15	2020-10-19 00:00:00.000000	200.050
16	2020-10-20 00:00:00.000000	201.960
17	2020-10-21 00:00:00.000000	213.060
18	2020-10-22 00:00:00.000000	203.880
19	2020-10-23 00:00:00.000000	203.040
20	2020-10-27 00:00:00.000000	200.440
21	2020-11-05 00:00:00.000000	204.590
22	2020-11-06 00:00:00.000000	202.720
23	2020-11-23 00:00:00.000000	200.820
24	2020-11-24 00:00:00.000000	206.000
25	2020-11-25 00:00:00.000000	214.380
26	2020-11-27 00:00:00.000000	211.320
27	2020-11-30 00:00:00.000000	214.200
28	2020-12-01 00:00:00.000000	216.520
29	2020-12-02 00:00:00.000000	212.660
30	2020-12-03 00:00:00.000000	214.680
31	2020-12-04 00:00:00.000000	217.235
Step 2: Find the top 10 daily returns for PYPL by completing the following steps:
-  Write a SQL statement to find the top 10 PYPL daily returns. Make sure to do the following:

    * Use `SELECT` to select only the “time” and “daily_returns” columns.

    * Use `ORDER` to sort the results in descending order by the “daily_returns” column.

    * Use `LIMIT` to limit the results to the top 10 daily return values.

- Using the SQL statement, read the data from the database into a Pandas DataFrame, and then review the resulting DataFrame.
# Write a SQL SELECT statement to select the time and daily_returns columns
# Sort the results in descending order and return only the top 10 return values
query = """
SELECT time, daily_returns
FROM PYPL
ORDER BY daily_returns DESC
LIMIT 10
"""
​
# Using the query, read the data from the database into a Pandas DataFrame
pypl_top_10_returns = pd.read_sql_query(query, con=engine)
​
# Review the resulting DataFrame
pypl_top_10_returns
​
time	daily_returns
0	2020-03-24 00:00:00.000000	0.140981
1	2020-05-07 00:00:00.000000	0.140318
2	2020-03-13 00:00:00.000000	0.138700
3	2020-04-06 00:00:00.000000	0.100877
4	2018-10-19 00:00:00.000000	0.093371
5	2019-10-24 00:00:00.000000	0.085912
6	2020-11-04 00:00:00.000000	0.080986
7	2020-03-10 00:00:00.000000	0.080863
8	2020-04-22 00:00:00.000000	0.075321
9	2018-12-26 00:00:00.000000	0.074656
Analyze the Fintech ETF Portfolio
For this part of the assignment, you’ll build the entire ETF portfolio and then evaluate its performance. To do so, you’ll build the ETF portfolio by using SQL joins to combine all the data for each asset.

Complete the following steps:

Write a SQL query to join each table in the portfolio into a single DataFrame. To do so, complete the following steps:

Use a SQL inner join to join each table on the “time” column. Access the “time” column in the GDOT table via the GDOT.time syntax. Access the “time” columns from the other tables via similar syntax.

Using the SQL query, read the data from the database into a Pandas DataFrame. Review the resulting DataFrame.

Create a DataFrame that averages the “daily_returns” columns for all four assets. Review the resulting DataFrame.

Hint Assuming that this ETF contains equally weighted returns, you can average the returns for each asset to get the average returns of the portfolio. You can then use the average returns of the portfolio to calculate the annualized returns and the cumulative returns. For the calculation to get the average daily returns for the portfolio, use the following code:

etf_portfolio_returns = etf_portfolio['daily_returns'].mean(axis=1)
You can use the average daily returns of the portfolio the same way that you used the daily returns of a single asset.

Use the average daily returns in the etf_portfolio_returns DataFrame to calculate the annualized returns for the portfolio. Display the annualized return value of the ETF portfolio.

Hint To calculate the annualized returns, multiply the mean of the etf_portfolio_returns values by 252.

To convert the decimal values to percentages, multiply the results by 100.

Use the average daily returns in the etf_portfolio_returns DataFrame to calculate the cumulative returns of the ETF portfolio.

Using hvPlot, create an interactive line plot that visualizes the cumulative return values of the ETF portfolio. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.

Step 1: Write a SQL query to join each table in the portfolio into a single DataFrame. To do so, complete the following steps:
- Use a SQL inner join to join each table on the “time” column. Access the “time” column in the `GDOT` table via the `GDOT.time` syntax. Access the “time” columns from the other tables via similar syntax.

- Using the SQL query, read the data from the database into a Pandas DataFrame. Review the resulting DataFrame.
# Wreate a SQL query to join each table in the portfolio into a single DataFrame 
# Use the time column from each table as the basis for the join
query = """
SELECT * FROM GDOT
INNER JOIN GS ON GDOT.time = GS.time
INNER JOIN PYPL ON GDOT.time = PYPL.time
INNER JOIN SQ ON GDOT.time = SQ.time;
"""
​
# Using the query, read the data from the database into a Pandas DataFrame
etf_portfolio = pd.read_sql_query(query, con= engine)
​
# Review the resulting DataFrame
etf_portfolio
​
time	open	high	low	close	volume	daily_returns	time	open	high	...	close	volume	daily_returns	time	open	high	low	close	volume	daily_returns
0	2016-12-16 00:00:00.000000	24.41	24.7300	23.9400	23.980	483544	-0.023218	2016-12-16 00:00:00.000000	242.80	243.1900	...	39.320	7298861	-0.005564	2016-12-16 00:00:00.000000	14.29	14.4700	14.2300	14.3750	4516341	0.017339
1	2016-12-19 00:00:00.000000	24.00	24.0100	23.5500	23.790	288149	-0.007923	2016-12-19 00:00:00.000000	238.34	239.7400	...	39.450	3436478	0.003306	2016-12-19 00:00:00.000000	14.34	14.6000	14.3000	14.3600	3944657	-0.001043
2	2016-12-20 00:00:00.000000	23.75	23.9400	23.5800	23.820	220341	0.001261	2016-12-20 00:00:00.000000	240.52	243.6500	...	39.740	2940991	0.007351	2016-12-20 00:00:00.000000	14.73	14.8200	14.4100	14.4900	5207412	0.009053
3	2016-12-21 00:00:00.000000	23.90	23.9700	23.6900	23.860	249189	0.001679	2016-12-21 00:00:00.000000	242.24	242.4000	...	40.090	5826704	0.008807	2016-12-21 00:00:00.000000	14.45	14.5400	14.2701	14.3800	3901738	-0.007591
4	2016-12-22 00:00:00.000000	23.90	24.0100	23.7000	24.005	383139	0.006077	2016-12-22 00:00:00.000000	241.23	242.8600	...	39.680	4338385	-0.010227	2016-12-22 00:00:00.000000	14.33	14.3400	13.9301	14.0400	3874004	-0.023644
...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...	...
994	2020-11-30 00:00:00.000000	55.87	56.0899	53.1100	53.550	361004	-0.043750	2020-11-30 00:00:00.000000	232.05	235.0000	...	214.200	8992681	0.013629	2020-11-30 00:00:00.000000	213.00	213.5400	200.2300	210.9800	10485040	-0.007153
995	2020-12-01 00:00:00.000000	54.00	54.2500	52.0007	53.790	546792	0.004482	2020-12-01 00:00:00.000000	231.96	234.8704	...	216.520	9148174	0.010831	2020-12-01 00:00:00.000000	212.56	212.9500	200.5000	203.0000	9911165	-0.037823
996	2020-12-02 00:00:00.000000	53.20	53.7900	50.9400	52.320	479868	-0.027328	2020-12-02 00:00:00.000000	232.08	238.1300	...	212.660	6414746	-0.017827	2020-12-02 00:00:00.000000	200.13	204.0596	195.1300	202.1100	9968056	-0.004384
997	2020-12-03 00:00:00.000000	52.48	54.1600	52.0200	53.760	474175	0.027523	2020-12-03 00:00:00.000000	237.29	238.8500	...	214.680	6463339	0.009499	2020-12-03 00:00:00.000000	207.00	208.6900	204.0500	205.5300	6497836	0.016921
998	2020-12-04 00:00:00.000000	53.87	54.1900	53.0850	53.860	83596	0.001860	2020-12-04 00:00:00.000000	237.70	239.6400	...	217.235	2118319	0.011901	2020-12-04 00:00:00.000000	206.29	208.9500	203.5800	207.6164	2820542	0.010151
999 rows × 28 columns

Step 2: Create a DataFrame that averages the “daily_returns” columns for all four assets. Review the resulting DataFrame.
# Create a DataFrame that displays the mean value of the “daily_returns” columns for all four assets.
etf_portfolio_returns = etf_portfolio["daily_returns"].mean(axis=1)
​
# Review the resulting DataFrame
etf_portfolio_returns
​
0     -0.007038
1     -0.001216
2      0.008567
3     -0.001004
4     -0.008243
         ...   
994   -0.014635
995   -0.003990
996   -0.006288
997    0.011246
998    0.009108
Length: 999, dtype: float64
Step 3: Use the average daily returns in the etf_portfolio_returns DataFrame to calculate the annualized returns for the portfolio. Display the annualized return value of the ETF portfolio.
# Use the average daily returns provided by the etf_portfolio_returns DataFrame 
# to calculate the annualized return for the portfolio. 
annualized_etf_portfolio_returns = etf_portfolio_returns*252
​
# Display the annualized return value of the ETF portfolio.
display(annualized_etf_portfolio_returns)
​
0     -1.773496
1     -0.306518
2      2.158814
3     -0.252987
4     -2.077206
         ...   
994   -3.688025
995   -1.005606
996   -1.584645
997    2.834002
998    2.295281
Length: 999, dtype: float64
Step 4: Use the average daily returns in the etf_portfolio_returns DataFrame to calculate the cumulative returns of the ETF portfolio.
s
# Use the average daily returns provided by the etf_portfolio_returns DataFrame 
# to calculate the cumulative returns
etf_cumulative_returns = (1+etf_portfolio_returns).cumprod()
​
# Display the final cumulative return value
etf_cumulative_returns.tail()
#final cumulative return value is 4.418250
994    4.374534
995    4.357078
996    4.329679
997    4.378371
998    4.418250
dtype: float64
Step 5: Using hvPlot, create an interactive line plot that visualizes the cumulative return values of the ETF portfolio. Reflect the “time” column of the DataFrame on the x-axis. Make sure that you professionally style and format your visualization to enhance its readability.
