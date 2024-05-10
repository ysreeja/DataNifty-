# DataNifty - NIFTY STOCK ANALYSIS : CLOUD ETL PIPELINE (USING AWS)

Problem Statement: The financial market, particularly in the domain of stock trading, is witnessing significant growth and evolution, with the Nifty stock index being a prominent player in the Indian stock market. With the advent of technology and increased access to financial data, there's a flourishing interest in leveraging data analytics and machine learning techniques for understanding and predicting stock price movements. The availability of granular data at 5-minute intervals from January 2015 to February 2022 provides a rich resource for conducting comprehensive analysis.

Business Flow Proposed: This project aims to construct a robust data pipeline for Nifty stock price analysis, leveraging both traditional OHLCV (Open, High, Low, Close, and Volume) data along with a suite of 55 technical indicators derived from this data. The data pipeline will facilitate the integration of diverse data sources, ensuring seamless access and processing of historical stock price information. By incorporating advanced analytics techniques, the pipeline will enable the extraction of actionable insights to inform trading strategies and investment decisions.

Analysis Dimensions:
• Trend Analysis: We can identify long-term, intermediate, and short-term trends in Nifty stock prices using moving averages, trendlines, and trend reversal indicators.
• Volatility Analysis: Also measure the volatility of Nifty stock prices using indicators such as Bollinger Bands, Average True Range (ATR), and historical volatility.
• Momentum Analysis: Can assess the momentum of Nifty stock prices using indicators like the Relative Strength Index (RSI), Moving Average Convergence Divergence (MACD), and Stochastic Oscillator.
• Volume Analysis: We can analyze trading volume patterns to identify periods of accumulation or distribution, using volume-based indicators such as On-Balance Volume (OBV) and Chaikin Money Flow.
• Pattern Recognition: We can also detect chart patterns such as triangles, flags, and head and shoulders patterns using pattern recognition algorithms.
• Correlation Analysis: Correlations can be explored between Nifty stock prices and various macroeconomic indicators, sectoral indices, and global market trends.
Strategic Insights: The analysis would be helpful for investors to understand the KPIs that are influencing the market trends. By establishing a comprehensive data pipeline for Nifty stock price analysis, this project aims to empower investors, traders, and financial institutions with actionable insights derived from robust data analytics techniques, ultimately enhancing decision-making processes, and maximizing returns on investment in the dynamic Indian stock market landscape. Also, we can identify optimal entry and exit points for trading positions based on trend, momentum, and volatility indicators. Market anomalies and abnormal trading patterns can be monitored for potential arbitrage opportunities or risk mitigation strategies. It will also help to adapt trading strategies accordingly and mitigate risk exposure.


Data Sources:
• https://www.kaggle.com/datasets/debashis74017/stock-market-data-nifty-100-stocks-5-min-data?select=BHARTIARTL_with_indicators_.csv
• https://www.kaggle.com/datasets/setseries/nifty50-stocks-dataset20102021/data

The pipeline can be broadly divided into 3 layers namely Landing Layer, Staging Layer, and Production Layer. We wanted to analyse the trends over the timeline of years, quarters and month.
Before creating the pipeline, we analysed our dataset. We had 50 CSV individual files separately for each stock over 7 years, we used PYTHON to do the initial pre-processing steps, by merging the data into 3 files: Yearly, Quarterly, and Monthly.

LANDING LAYER:
Initially, we created S3 buckets.
One for Source: source-stocks & One for Target: target-stocks.
After creating S3 buckets, the CSV files were uploaded to specific folders within the source bucket. Following this, to perform ETL and query the transformed data for analysis, we created source and target AWS Glue Databases using Amazon Athena. Then the data was loaded into the respective database with the help of AWS Crawlers. Crawlers automatically detect the schema of the files and create tables to store data in the database.

STAGING LAYER:
In AWS Glue, we set up a target database where all our cleaned and transformed data lands after our ETL jobs finish their work. This database is like a safe home for our data, making sure it's organized and ready to use for future analyses and applications.Now we create ETL jobs in GLUE as follows. In the ETL jobs, we have performed transformations and schema changes as per our requirements.

PRODUCTION LAYER:
Once the crawlers run successfully, we will be now able to query our tables in Athena. 

![image](https://github.com/ysreeja/DataNifty-/assets/163582984/113d7daa-d8e8-485c-8503-4bbcc13a89c8)

DASHBOARD INSIGHTS:
• Top 10 SMA: Showcases the Simple Moving Average (SMA) values of the top 10 companies. SMA is used to smooth out price data over a specified period by creating a constantly updated average price.
• Monthly Average Price Stats: Depicts the average closing and high prices of stocks monthly, illustrating price stability or volatility over the year.
• MOM Vs ROC: Compares the Momentum (MOM) and Rate of Change (ROC) of selected companies' stocks across months. MOM measures the speed at which prices are changing, while ROC measures the percentage change in price between the current price and the price a certain number of periods ago.
• Average Directional Moment - Conglomerate Stocks: Analyzes the Average Directional Movement Index (ADX) quarterly for conglomerate stocks, which indicates the strength of a trend.
• Moving Convergence: F&B: Tracks the Moving Average Convergence Divergence (MACD) over years for the Food & Beverage sector, signifying trend reversals and momentum.
• Pharma Sector: FastK Momentum Index: Displays the Stochastic Oscillator FastK metric for the pharmaceutical sector, showing momentum over time by comparing a particular closing price of a security to a range of its prices over a certain period.
