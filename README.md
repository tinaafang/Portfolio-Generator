# CFM-Group-Assignment
Targeting the Safest Portfolio, with a Return on Investment as close as 0%.

# Input and Output
Input a csv file of tickers
Output a csv file that contains a diversified portfolio with minimum of 10 stock and maximum 20 of stocks, the weight of each stock lies in [(100/2n)%, 35%] where n is the number of stocks

# Algorithm
This program follows the step of filter, rank, group by correlations, assign weights, and finally generate the portfolio. 

The first step is to extract the tickers from the given csv file and filter through to discard any non US listed stock and any less active stocks.  (an average daily volume of at least 10,000 shares, based on the time interval of July 02, 2021 to October 22, 2021.) 

Next, we rank the tickers by the standard deviation of closing prices in the past three months and beta. The top 30 stocks are carried to the next step, where tickers are paired up based on their correlations. Starting from the first-ranking ticker, the program loops through the rest of the ticker bank to find the one that has the least correlation with the first-ranking ticker, then store the pair and continue the process starting from the second-ranking ticker and so on, until we have 10 pairs of these, and thus 10 portfolios with stocks that are least correlated. 

To determine the weights of each individual stock, we need to determine how each stock is weighted in its pair, and how each pair of portfolio is weighted in the final portfolio. For the former, the optimal weight is determined by iterating all possible weightings, where the range of the weighting is determined by another for loop. The latter is determined by scaling the portfolios with positive returns and negative returns. First, we determine the weight of posotive returns and negsative returns, call them positive weight and negative weight. Recall that each stock must make up (100/2n)% of the portfolio where n is the number of stocks. In this case, n = 20 and the mininal weight for each stock is 2.5%. The ideal solution is to reach a 50:50 ratio between these two and not violating the minimal weight requirement, and the weight allocated to each weight is just 0.5/the weight. If there is a conflict, the weight allocated would be weight = (minimal_weight*number of stocks with pos/neg weight) and the other weight would be 1-weight. 

Once the weights are determined, apply the weights of each pair of portfolio to get the final weight for each stock and build the final portfolio accordingly.


# Demo(How to Use)


# Framework/Toos
Yahoo Finance, pandas, concurrent.futures, matplotlib