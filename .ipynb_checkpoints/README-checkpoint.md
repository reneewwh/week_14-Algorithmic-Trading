# Machine Learning Trading Bot

![Decorative image.](Images/14-challenge-image.png)

Now, it's time to take what you've learned about machine learning and apply it to new situations. For this optional assignment, you'll create an algorithmic trading bot that learns and adapts to new data and evolving markets. Be sure to give it your all -- as the skills you hone will become powerful tools in your FinTech tool belt.

## Background

In this Challenge, you’ll assume the role of a financial advisor at one of the top five financial advisory firms in the world. Your firm constantly competes with the other major firms to manage and automatically trade assets in a highly dynamic environment. In recent years, your firm has heavily profited by using computer algorithms that can buy and sell faster than human traders.

The speed of these transactions gave your firm a competitive advantage early on. But, people still need to specifically program these systems, which limits their ability to adapt to new data. You’re thus planning to improve the existing algorithmic trading systems and maintain the firm’s competitive advantage in the market. To do so, you’ll enhance the existing trading signals with machine learning algorithms that can adapt to new data.

## What You're Creating

You’ll combine your new algorithmic trading skills with your existing skills in financial Python programming and machine learning to create an algorithmic trading bot that learns and adapts to new data and evolving markets.

In a Jupyter notebook, you’ll do the following:

* Implement an algorithmic trading strategy that uses machine learning to automate the trade decisions.

* Adjust the input parameters to optimise the trading algorithm.

* Train a new machine learning model and compare its performance to that of a baseline model.

As part of your GitHub repository’s `README.md` file, you will also create a report that compares the performance of the machine learning models based on the trading predictions that each makes and the resulting cumulative strategy returns.

## Files

Download the following files to help you get started:

[Unit 14 homework files](Starter_Code/Starter_Code.zip)

> **Note:** The provided CSV file contains OHLCV data for an MSCI&ndash;based emerging markets ETF that [iShares](https://www.ishares.com/us/products/268704/ishares-currency-hedged-msci-emerging-markets) issued. Investments in emerging markets make up an important aspect of a well-diversified investment portfolio. This is because the included equities have potentially higher long-term returns, even though they carry more risk.

## Instructions

Use the starter code file to complete the steps that the instructions outline. The steps for this Challenge are divided into the following sections:

* Establish a Baseline Performance

* Tune the Baseline Trading Algorithm

* Evaluate a New Machine Learning Classifier

* Create an Evaluation Report

### Establish a Baseline Performance

In this section, you’ll run the provided starter code to establish a baseline performance for the trading algorithm. To do so, complete the following steps.

Open the Jupyter notebook. Restart the kernel, run the provided cells that correspond with the first three steps, and then proceed to step four.

1. Import the OHLCV dataset into a Pandas DataFrame.

2. Generate trading signals using short- and long-window SMA values.

3. Split the data into training and testing datasets.

4. Use the `SVC` classifier model from SKLearn's support vector machine (SVM) learning method to fit the training data and make predictions based on the testing data. Review the predictions.

5. Review the classification report associated with the `SVC` model predictions.

6. Create a predictions DataFrame that contains columns for “Predicted” values, “Actual Returns”, and “Strategy Returns”.

7. Create a cumulative return plot that shows the actual returns vs. the strategy returns. Save a PNG image of this plot. This will serve as a baseline against which to compare the effects of tuning the trading algorithm.

8. Write your conclusions about the performance of the baseline trading algorithm in the `README.md` file that’s associated with your GitHub repository. Support your findings by using the PNG image that you saved in the previous step.

### Tune the Baseline Trading Algorithm

In this section, you’ll tune, or adjust, the model’s input features to find the parameters that result in the best trading outcomes. (You’ll choose the best by comparing the cumulative products of the strategy returns.) To do so, complete the following steps:

1. Tune the training algorithm by adjusting the size of the training dataset. To do so, slice your data into different periods. Rerun the notebook with the updated parameters, and record the results in your `README.md` file. Answer the following question: What impact resulted from increasing or decreasing the training window?

    > **Hint** To adjust the size of the training dataset, you can use a different `DateOffset` value&mdash;for example, six months. Be aware that changing the size of the training dataset also affects the size of the testing dataset.

[1] Output: 
Code adjustment #1 from original:
ohlcv_df=ohlcv_df[ohlcv_df.index.year.isin([2019, 2020])].copy()
As the first experiment, I have sliced the data from 2019 -2021, omitting years before 2019. The cumulative actual returns is lower than the cumulative strategy return, this potentially indicates the recent year's returns has been relatively optimistic, which uplifted the predictions of strategy returns. 
Please see plot <cumulative_plot_period_20192020.png>
![plot01.](../Plots/cumulative_plot_period_20192020.png)

Code Adjustment #2 from original:
ohlcv_df=ohlcv_df[(ohlcv_df.index.year ==2019) & ohlcv_df.index.month.isin([2,3,4,5,6,7])].copy()
In this second experiment, i have extracted only 6 months worth of data in 2019. The test data (aka July) looks really off - not only the actual returns are below of strategy returns (based on modeling), but as well as they go on different direction whihc looks like it has potential overfitting. 

Decreasing training window even though may potentially allow the model to become responsive to short-term changes, however based on the precision and recall score in the classification report, the accuruacy decreased significantly from the original. Perhaps it would be a better idea to test with increasing training window, and assess the overall f1_score to determine whether increasing training window is a good option.
Please see plot <cumulative_plot_2019_6m.png>


2. Tune the trading algorithm by adjusting the SMA input features. Adjust one or both of the windows for the algorithm. Rerun the notebook with the updated parameters, and record the results in your `README.md` file. Answer the following question: What impact resulted from increasing or decreasing either or both of the SMA windows?

[2]Output: 
(1)Code Adjustments:-
short_window = 10
long_window = 250
In this experiment, i have increased both the SMA windows by x2.5. the f1 score has decreased as reflected across precision and recall respectively. In the graph, from mid-2019 to early 2020 - the predictions were far off with large discrepencies between the two results. However, the trend picked back up afte march in terms of trend directions. However, the discrepency of the returns remain large. 
Please see plot <cumulative_plots_increasing_window>


(2)Code Adjustments:-
short_window = 80
long_window = 100
In this experiment, i have increased the short window closer to the long window. the f1 score further deteriorates - seem like it's the worst inptus out of the experiements i did.
Please see plot <cumulative_plots_close_window>

(3)Code Adjustments:-
short_window = 4
long_window = 250
In this experiment, i have increased the long window to 250, while maintaining the short window. the f1-score remains in the 60s (low score), and the discrepencies are much higher than the experiements made (1) in this section. Strategy returns' fluctuations tend to react 'less vividly' comparing to the actuals. 
Please see plot <cumulative_plots_4_250>


3. Choose the set of parameters that best improved the trading algorithm returns. Save a PNG image of the cumulative product of the actual returns vs. the strategy returns, and document your conclusion in your `README.md` file.

Date: 2018-2021
Short_window = 5
long_window = 300

the returns tend to react correponsidingly to the actual returns even though strategy returns are evaluated higher than the actuals. 
>cumulative_plot_period_20192020

Date: 2018-2021
Short_window = 1
long_window = 80

The strategy returns are slighlty underevaluated from end of 2020. however, they are still moving parallel direction. 


### Evaluate a New Machine Learning Classifier

In this section, you’ll use the original parameters that the starter code provided. But, you’ll apply them to the performance of a second machine learning
To do so, complete the following steps:

1. Import a new classifier, such as `AdaBoost`, `DecisionTreeClassifier`, or `LogisticRegression`. (For the full list of classifiers, refer to the [Supervised learning page](https://scikit-learn.org/stable/supervised_learning.html) in the scikit-learn documentation.)

2. Using the original training data as the baseline model, fit another model with the new classifier.

3. Backtest the new model to evaluate its performance. Save a PNG image of the cumulative product of the actual returns vs. the strategy returns for this updated trading algorithm, and write your conclusions in your `README.md` file. Answer the following questions: Did this new model perform better or worse than the provided baseline model? Did this new model perform better or worse than your tuned trading algorithm?

### Create an Evaluation Report

In the previous sections, you updated your `README.md` file with your conclusions. To accomplish this section, you need to add a summary evaluation report at the end of the `README.md` file. For this report, express your final conclusions and analysis. Support your findings by using the PNG images that you created.

---

## Submission

* Use the started code provided to create the machine learning trading bot and host the notebook and the required files.

* Include a `README.md` file with your conclusions as requested.

* Submit the link to your GitHub project to Bootcamp Spot.

---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
