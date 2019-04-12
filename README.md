# stats2_project2
<H2>Using Logistic Regression and other Models to predict Defaults</H2>

<i>Authors: Kito Patterson and Hayley Horn</i>

<b>INTRODUCTION</b>
Home Equity loans can be seen as an alternative to credit card debt because it leverages a secured asset.  Home equity lines of credit account for approximately 4% of debt among consumers(1). The value of 90+ day delinquencies is 2.23B in 2016(2).  In this study we seek to uncover factors that contribute to these defaults so that we can predict an applicant’s propensity to default. This could also benefit consumers, if they have high indicators for default, it could be an opportunity for consumer debt counseling or some other intervention to give them an opportunity to course correct before they find themselves in default. This research study dives into a collection of potential variables and delinquency on home equity loans. 
Our approach to this problem had three components. First, we performed EDA (LIST things) and reviewed the data gathered for data filtering, transformation, and feature analysis. Second, we ran the data through a (several) logistic regression models and determined which values had the highest probabilities of class membership. Next using the results of the logistic model as a baseline, we performed additional models to see if we could determine a predictor that performs better than the logistic regression model. (or is more accurate?)

<b>DATA DESCRIPTION </b>
The data set came from a book “Credit Risk Analytics: The R Companion, Scheule Roesch Baesens, 2017.”  (3) The data set called HMEQ contains anonymized characteristics, and delinquency information for 5,960 home equity loans.  A time period for this data is not provided.

The data dictionary can be found in Table x in the appendix. Below, Table 1 shows the summary statistics of the final data set, comprising of 5960 observations.

<TABLE DIR=LTR BORDER>
<CAPTION>Summary Statistics</CAPTION>
<TR>
<TD DIR=LTR ALIGN=LEFT>BAD</TD>
<TD DIR=LTR ALIGN=RIGHT>5960</TD>
<TD DIR=LTR ALIGN=LEFT>  </TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>1.00</TD>
<TD DIR=LTR ALIGN=LEFT>0.20</TD>
<TD DIR=LTR ALIGN=LEFT>0.40</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>LOAN</TD>
<TD DIR=LTR ALIGN=RIGHT>5960</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>1100.00</TD>
<TD DIR=LTR ALIGN=RIGHT>89800.00</TD>
<TD DIR=LTR ALIGN=LEFT>18596.01</TD>
<TD DIR=LTR ALIGN=LEFT>11170.30</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>MORTDUE</TD>
<TD DIR=LTR ALIGN=RIGHT>5442</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>2063.00</TD>
<TD DIR=LTR ALIGN=RIGHT>399550.00</TD>
<TD DIR=LTR ALIGN=LEFT>73765.40</TD>
<TD DIR=LTR ALIGN=LEFT>44460.41</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>VALUE</TD>
<TD DIR=LTR ALIGN=RIGHT>5848</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>8000.00</TD>
<TD DIR=LTR ALIGN=RIGHT>855909.00</TD>
<TD DIR=LTR ALIGN=LEFT>101778.25</TD>
<TD DIR=LTR ALIGN=LEFT>57390.44</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>REASON</TD>
<TD DIR=LTR ALIGN=RIGHT>5708</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=LEFT>#DIV/0!</TD>
<TD DIR=LTR ALIGN=LEFT>#DIV/0!</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>JOB</TD>
<TD DIR=LTR ALIGN=RIGHT>5681</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=LEFT>#DIV/0!</TD>
<TD DIR=LTR ALIGN=LEFT>#DIV/0!</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>YOJ</TD>
<TD DIR=LTR ALIGN=RIGHT>5445</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>41.00</TD>
<TD DIR=LTR ALIGN=LEFT>8.92</TD>
<TD DIR=LTR ALIGN=LEFT>7.57</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>DEROG</TD>
<TD DIR=LTR ALIGN=RIGHT>5252</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>10.00</TD>
<TD DIR=LTR ALIGN=LEFT>0.25</TD>
<TD DIR=LTR ALIGN=LEFT>0.85</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>DELINQ</TD>
<TD DIR=LTR ALIGN=RIGHT>5380</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>15.00</TD>
<TD DIR=LTR ALIGN=LEFT>0.45</TD>
<TD DIR=LTR ALIGN=LEFT>1.13</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>CLAGE</TD>
<TD DIR=LTR ALIGN=RIGHT>5652</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>1168.23</TD>
<TD DIR=LTR ALIGN=LEFT>179.76</TD>
<TD DIR=LTR ALIGN=LEFT>85.82</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>NINQ</TD>
<TD DIR=LTR ALIGN=RIGHT>5450</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>17.00</TD>
<TD DIR=LTR ALIGN=LEFT>1.19</TD>
<TD DIR=LTR ALIGN=LEFT>1.73</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>CLNO</TD>
<TD DIR=LTR ALIGN=RIGHT>5738</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.00</TD>
<TD DIR=LTR ALIGN=RIGHT>71.00</TD>
<TD DIR=LTR ALIGN=LEFT>21.30</TD>
<TD DIR=LTR ALIGN=LEFT>10.14</TD>
</TR>
<TR>
<TD DIR=LTR ALIGN=LEFT>DEBTINC</TD>
<TD DIR=LTR ALIGN=RIGHT>4693</TD>
<TD></TD>
<TD DIR=LTR ALIGN=RIGHT>0.52</TD>
<TD DIR=LTR ALIGN=RIGHT>203.31</TD>
<TD DIR=LTR ALIGN=LEFT>33.78</TD>
<TD DIR=LTR ALIGN=LEFT>8.60</TD>
</TR>
</TABLE>

<b>EXPLORATORY DATA ANALYSIS</b>
This as seen in the data dictionary, this data set contains fields with missing data

<b>Exploratory Analysis REQUIRED</b>

<h3>ADDRESSING OBJECTIVE 1:</h3>

<b>RESTATEMENT OF PROBLEM AND THE OVERALL APPROACH TO SOLVE IT REQUIRED</b>

<b>MODEL SELECTION REQUIRED</b>
		Type of Selection
			Any or all:  LASSO, RIDGE, ELASTIC NET,
			Stepwise, Forward, Backward 
			Manual / Intuition		

<b>CHECKING ASSUMPTIONS REQUIRED</b>
Lack of fit test
Influential point analysis (Cook’s D and Leverage)
		Residual Plots Optional  
			
<b>PARAMETER INTERPRETATION REQUIRED</b>
		Interpretation REQUIRED
		Confidence Intervals REQUIRED
	
<b>FINAL CONCLUSIONS from the analyses of Objective 1 REQUIRED</b>


 
<h3>Objective 2: 2-Way ANOVA</h3>

<b>ADDRESSING OBJECTIVE 2:</b>
Make sure it is clear how many models were created to compete against the one in Objective 1.  Make note of any tuning parameters that were used and how you came up with them (knn and random forest logistics)  Required


<b>MAIN ANALYSIS CONTENT REQUIRED</b>
	Overall report of the error metrics on a test set or CV run.  Also if the two best models have error rates of .05 and .045,  can we really say that one model is outperforming the other?  What other tools that we learned in the second half of this class that could help us get at that?

<b>CONCLUSION/DISCUSSION REQUIRED</b>
		The conclusion should reprise the questions and conclusions of objective 2 with recommendations of the final model, what could be done to help analysis and model building in the future, and any insight as to why one method outshined all the rest if that is indeed the case.  If they all are similar why did you go with your final model?

<b>APPENDIX REQUIRED</b>
	Well commented SAS/R Code Required
 	Graphics and summary tables (Can be placed in the appendix or in the written report itself.)


<b>REFERENCES</b>
1.	https://www.statista.com/statistics/944954/personal-debt-source-usa/
2.	https://www.statista.com/statistics/681709/value-of-90-delinquent-heloc-balances-usa/
3.	Data http://www.creditriskanalytics.net/datasets-private.html
4.	
 
<b>CODE:</b>



<b>possible reference </b>
https://jupyter.brynmawr.edu/services/public/dblank/CS371%20Cognitive%20Science/2016-Fall/Simple%20logistic%20regression.ipynb


https://git.generalassemb.ly/BAH-DC-1/logistic-regression/blob/master/logistic-regression-starter.ipynb <-yas


