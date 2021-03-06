# **Into the Online World: Human or Bot?**

**Dataset used**: cresci-stock-2018

**Description**: Automated accounts that act in coordinate fashion. Labels and user objects.

**Citation:** Cresci, S., Lillo, F., Regoli, D., Tardelli, S., & Tesconi, M. (2019). Cashtag Piggybacking. *ACM Transactions on the Web,* *13*(2), 1-27. doi:10.1145/3313184

[[Download dataset here!](https://botometer.osome.iu.edu/bot-repository/datasets/cresci-stock-2018/cresci-stock-2018.tar.gz)]



## For quick use

### Results only

Results of our findings can be found in the `results` folder.



### Classification only

If you would like to jump straight into classification between bot and human accounts, follow the steps in **experiments 1, 2, and 3**. Filtering is not required as we have already generated the filtered dataset for you.



## Understanding our filtered dataset

**User based classification:** 10470 users; 5363 bots, 5107 humans *(51.2%/48.8%)*

**Tweet based classification by tweet:** 1068218 tweets; 30428 bots, 1037790 humans  *(2.8%/97.2%)*

**Tweet based classification by user:** 3662 users; 1016 bots, 2646 humans *(27.7%/72.3%)*



## Filter

Filtering of datasets should be done in this particular order:
1. `filter (remove deleted, suspended accounts).py`
2. `filter (create dataset for user based classification).py`
3. `filter (create unfiltered dataset for tweet based classification).py`
4. `filter (create dataset for tweet based classification).py`



If you would like to skip step 3, extract `twint results.csv` from `unfiltered dataset/twint results.rar`.



## Experiment 1: Compare between types of algorithm
There are two types of classification that we are employing:
1. user based classification
2. tweet based classification
   - by tweet
   - by user



### Experiment 1.1: User-based classification

Follow steps 1 and 2 of **filter** if you would like to obtain the dataset from scratch.



Run `classification.py` to get results.



To switch to user based classification:

**Line 12:** `dataset = pd.read_csv("filtered dataset/user based classification.csv")`

**Line 88:** `plt.suptitle("User Based Classification", fontweight = "bold", fontsize = "x-large", x = 0.51, y = 0.99)`



### Experiment 1.2 and 1.3: Tweet-based classification

Follow steps 1, 3 and 4 of **filter** if you would like to obtain the dataset from scratch.



To switch to tweet based classification *by tweet*:

**Line 12:** `dataset = pd.read_csv("filtered dataset/tweet based classification (by tweet).csv")`

**Line 88:** `plt.suptitle("Tweet Based Classification (By Tweet)", fontweight = "bold", fontsize = "x-large", x = 0.51, y = 0.99)`



Run `classification.py` to get results.



To switch to tweet based classification *by user*:

**Line 12:** `dataset = pd.read_csv("filtered dataset/tweet based classification (by user).csv")`

**Line 88:** `plt.suptitle("Tweet Based Classification (By User)", fontweight = "bold", fontsize = "x-large", x = 0.51, y = 0.99)`



## Experiment 2: Compare within best type of algorithm

If you took a sneak peek at our results or have already done experiment 1, you might already know that user based classification that uses tree-based algorithms like random forest classifier has the best performance.



### Experiment 2.1: User based classification (comparing between tree-based algorithms)

Run `classification (user based classification, tree-based).py` to get results.



## Experiment 3: Optimization of algorithm

### Experiment 3.1: Randomized search for hyperparameter tuning

Run `classification (user based classification, random forest, hyperparameter tuning, RandomizedSearchCV).py` to get results.



### Experiment 3.2: Time-scoring analysis where one hyperparameter is changed while the rest kept constant at default values

Run `classification (user based classification, random forest, time-scoring analysis).py` to get results.



### Experiment 3.3: Exhaustive search for hyperparameter tuning

Run `classification (user based classification, random forest, hyperparameter tuning, GridSearchCV).py` to get results.



### Experiment 3.4: Precision-recall trade-off for hyperparameter-tuned algorithm

Run `classification (user based classification, random forest, hyperparameter tuned, precision recall trade-off).py` to get results.



## Debugging

Debugging is used as last resort in case of certain errors, generally during filtering. For manual debugging of `filter (create unfiltered dataset for tweet based classification).py`, use `debugger.py`. It is **recommended** to save the output in IDLE for future reference. Debug logs are stored in `debug log.csv`.



After manual debugging, use `debug checker.py` to check for additional results scraped from Twitter during debugging. See comments in `debug checker.py` for more information.



To remove rows from `unfiltered dataset/twint results.csv`, use [Delimit](http://www.delimitware.com/index.html)'s extract function.

> Filter to apply when extracting rows: `$4 <> user_id`

Change `user_id` to the user_id of the user that you would like to delete.



To add rows to `unfiltered dataset/twint results.csv`, copy and paste from `debug log.csv`.



## Comments

- When we did tweet based classification by tweet, we found that the f1 measure is very low. Hence, we switched to average of all tweets made by user during the same 100-day period.
- We also note that our dataset is not large enough to sieve out the specific names of hashtags and cashtags in tweets and description etc as it may result in higher bias and an inaccurate algorithm.
- In the future we might add NULL values to accounts that do not tweet to `filtered dataset/tweet based classification (by tweet).csv`, as we note that there are a large number of bots that do not tweet when comparing our datasets for user based classification and tweet based classification.