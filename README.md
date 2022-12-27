# Udacity AB Testing Final Project
Udacity website has a new design and wants to improve user experience. This project aims at evaluating whether this new design can be effective in production. The project will go through experiment design and analysis to collect statistical evidences to make a reasonable decision to launch this new design or not. 


# Final Project Instructions
Linke to the Final Project Description - https://docs.google.com/document/u/1/d/1aCquhIqsUApgsxQ8-SQBAigFDcfWVVohLEXcV6jWbdI/pub

<img src="user_funnel_journey.jpg" height="700"> 

# Hypothesis and expectation of this new feature
The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn't have enough time without significantly reducing the number of students to continue past the free trial and eventually complete the course. **If this hypothesis held true, Udacity could improve the overall student experience and improve coaches' capacity to support students who are likely to complete the course.**


The unit of diversion is a cookie, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.

# Metric List
<img src="Metric_List.jpg" height="350">

<img src="Metric_and_user_funnel.jpg" height="300"> 

## 1. Metric Choice
List which metrics you will use as invariant metrics and evaluation metrics here. For each metric, explain both why you did or did not use it as an invariant metric and why you did or did not use it as an evaluation metric. Also, state what results you will look for in your evaluation metrics in order to launch the experiment.

#### Invariant Metrics 
*The key is to find the steps **before the new feature**.

* **Number of cookies (page views) :** The course overview page is prior to the new feature. Thus, this metric should be the same between control and experiment groups. 

* **Number of clicks (start free trial bottom):** This metric is prior to the new feature. Thus, this metric should not change between control and experiment groups. 

* **Click-through-probability(=clicks/page views):**  Same reason. The click and course page view are prior to the new feature, so there should be no change in this metric between the control and experiment groups. 



#### Evaluation Metrics 
*The key is to identify the steps **after the new feature**. Thus, metrics which are related to "enrollment" or "payment" can be evaluation metric.*


* **Gross Conversion (=enrollment/click):** "enrollment" occurs after the new feature, and "click" (the denominator) is invariant, so this metric is movable and can be used as an evaluation metric. We expect that gross conversion to **go down** in the experiment, because *the design of this new feature is to divert less-committed people to the free course, instead of enrollment in the free trial. This causes less people to be in the "enrollment".

* **Net conversion (=payment/click):** "payment" occurs after this new feature, and "click" (the denominator) is invariant, so this metric is movable and can be used as an evaluation metric. We expect the net conversion to be **higher** in the experiment, because the new feature is supposed to select more committed people who are likely to stay in the free trail and make payment at the end. 

* **Retention (=payment/enrollment):** Both of "payment" and "enrollment" occur after this new feature. We expect the retention rate to be **higher** in the experiment, because the new feature is supposed to select more committed people who are likely to make payment. 


#### Bad Metrics
* **Number of user-ids (enrollment):** In the experiment, enrollment stage is after the new feature, but enrollment (count) may not be a good evaluation metric. The reason is that it's not good to use a pure count metric as the evaluation metric in the funnel process analysis. In the funnel process, the number of the counts for each step is conditioned to previous step. Thus, it's good to use rate or probability which is normalized, instead of a counting number.




## 2. Variability

**Summary of Variability**

The estimated variability is based on the page view = 5000. If the SE is large, then we might need to collect a huge amont of data in order to evaluate this this metric.

|Metric| Standard Error|
|---   |            ---|
|Gross Conversion|0.0202|
|Retention       |0.0549|
|Net Conversion  |0.0156|

> **Note:** Retention's SE is relatively large. In section "3. Sizing", We will check if we can collect enough data in order to have enought power to evaluate Retention.


**Question:** Do you expect the analytic estimates to be accurate? That is, for which metrics, if any, would you want to collect an empirical estimate of the variability if you had time?

> **My answer:** 
I would like to collect empirical estimates of variability for (1) **Gross Conversion** and (2) **Net Conversion**, because for these metrics, their unit of diversion is not the same as the unit of analysis. In such case, the analytic form of variability is usually underestimated (smaller than the truth). Thus, it's better to use bootstrap method to obtain the empirical estimate of the variability. 


|Evaluation metric | Numerator (unit of diversion) | Denominator (unit of analysis)  |
|------------------|-------------------------------|---------------------------------|
|Gross Conversion  | enrollment (user-id)          | click (cookie)                  |
|Retention         | payment (user-id)             | enroll (user-id)                |
|Net Conversion    | payment (user-id)             | click (cookie)                  |
>>

## 3. Sizing

#### My thinking process:  
1. I will compute the required sample size for each evaluation metric, based on the (1) baseline data, (2) minimally important difference (dmin) , (3) alpha = 0.05, and (4) beta=0.2.

2. On-line calculator will be a great tool for this task: https://www.evanmiller.org/ab-testing/sample-size.html

3. Convert the required "sample size" into required "page views" for both control and experiment groups.

4. Then, check if our system can reach the sample size in a short time (usually ~ 30 days). If a metric need more than 30 days to collect, we might need to drop it or re-design the experiment.

5. Based on the required page views, I will select the maximum page views among evaluation metrics.


#### Size  -  Gross Conversion 
* dmin = 0.01
* GC = n_enroll / n_click  = Probability of enrolling, given click  = 0.206250 (baseline)
* Required Sample Size in each group, N=25835 (using Online-calculator).
* Required n-click (two groups) = 2 * 25835 = 51670
* Then, we want to know how many page view can reach the number of required clicks.
* Based on the ratio, there will be 3,200 clicks among 40000 page views.
* Now, we need to have [2*25835 = 51,670] clicks, so  we need  (40000 * 51670) / (3200)  = 645,875 page views.



**Question:** Which evaluation metrics did you choose?

> **ANS:** (1) gross conversion and (2) net conversion

**Question:** Will you use Bonferroni Correction? 

> **ANS:** These evaluation metrics are highly correlated, so Bonferroni would be too conservative.

**Question:** How many page view that we need? 

> **ANS** 685,325



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
