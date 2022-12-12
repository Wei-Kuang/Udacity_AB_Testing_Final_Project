# Udacity AB Testing Final Project
Udacity website has a new design and wants to improve user’s experience. This project aims at evaluating whether this new design can be effective in production. The project will go through experiment design and analysis to collect statistical evidences to make a reasonable decision to launch this new design or not. 


# Final Project Instructions
https://docs.google.com/document/u/1/d/1aCquhIqsUApgsxQ8-SQBAigFDcfWVVohLEXcV6jWbdI/pub

<img src="user_funnel_journey.jpg" height="700"> 

### Metirc List
<img src="Metric_List.jpg" height="350">

## 1. Metric Choice
List which metrics you will use as invariant metrics and evaluation metrics here. For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.

### Invariant Metrics 
* **Number of cookies (course pageviews) :** The course overview page is prior to the new change. Thus, this metric should be the same between control and experiment groups. 

* **Number of clicks (start free trial bottom):** This feature is prior to the new change. Thus, this metric should not change between control and experiment groups. 
	
* **Click-through-probability(clicks / course pageviews):**  Same reason. The click and course pageview are prior to the new feature, so there should be no change in this metric between the control and experiment groups. 


## 2. Variability
List the standard deviation of each of your evaluation metrics. For each of your evaluation metrics, indicate whether you think the analytic estimate would be comparable to the the empirical variability, or whether you expect them to be different (in which case it might be worth doing an empirical estimate if there is time). Briefly give your reasoning in each case.


## 3. Sizing
### Number of Samples vs. Power
Indicate whether you will use the Bonferroni correction during your analysis phase, and give the number of pageviews you will need to power you experiment appropriately. 

### Duration vs. Exposure
Indicate what fraction of traffic you would divert to this experiment and, given this, how many days you would need to run the experiment. Give your reasoning for the fraction you chose to divert. How risky do you think this experiment would be for Udacity?


## 4. Sanity Checks
For each of your invariant metrics, give the 95% confidence interval for the value you expect to observe, the actual observed value, and whether the metric passes your sanity check. 

## 5. Effect Size Tests
For each of your evaluation metrics, give a 95% confidence interval around the difference between the experiment and control groups. Indicate whether each metric is statistically and practically significant.

## 6. Sign Tests
For each of your evaluation metrics, do a sign test using the day-by-day data, and report the p-value of the sign test and whether the result is statistically significant.

## 7. Results Summary
State whether you used the Bonferroni correction, and explain why or why not. If there are any discrepancies between the effect size hypothesis tests and the sign tests, describe the discrepancy and why you think it arose.

## 8. Recommendation
Make a recommendation and briefly describe your reasoning.


## 9. Follow-Up Experiment
Give a high-level description of the follow up experiment you would run, what your hypothesis would be, what metrics you would want to measure, what your unit of diversion would be, and your reasoning for these choices.
