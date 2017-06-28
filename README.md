# HackerEarth Machine Learning Challenge #2
### Predicting success on Kickstarter

Brief: https://www.hackerearth.com/challenge/competitive/machine-learning-challenge-2/

Dataset: https://he-s3.s3.amazonaws.com/media/hackathon/machine-learning-challenge-2/funding-successful-projects/3149def2-5-datafiles.zip

## Problem statements

Kickstarter is a community of more than 10 million people comprising of creative, tech enthusiasts who help in bringing creative project to life. Till now, more than $3 billion dollars have been contributed by the members in fuelling creative projects. The projects can be literally anything – a device, a game, an app, a film etc.

Kickstarter works on all or nothing basis i.e if a project doesn’t meet it goal, the project owner gets nothing. For example: if a projects’s goal is $500. Even if it gets funded till $499, the project won’t be a success.

Recently, kickstarter released its public data repository to allow researchers and enthusiasts like us to help them solve a problem. Will a project get fully funded ?

In this challenge, you have to predict if a project will get successfully funded or not.

## Input data description

There are three files given to download: train.csv, test.csv and sample_submission.csv The train data consists of sample projects from the May 2009 to May 2015. The test data consists of projects from June 2015 to March 2017.

<table>
<thead>
<tr>
<th>Variable</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>project_id</td>
<td>unique id of project</td>
</tr>
<tr>
<td>name</td>
<td>name of the project</td>
</tr>
<tr>
<td>desc</td>
<td>description of project</td>
</tr>
<tr>
<td>goal</td>
<td>the goal (amount) required for the project</td>
</tr>
<tr>
<td>keywords</td>
<td>keywords which describe project</td>
</tr>
<tr>
<td>disable communication</td>
<td>whether the project authors has disabled communication option with people donating to the project</td>
</tr>
<tr>
<td>country</td>
<td>country of project author</td>
</tr>
<tr>
<td>currency</td>
<td>currency in which goal (amount) is required</td>
</tr>
<tr>
<td>deadline</td>
<td>till this date the goal must be achieved (in unix timeformat)</td>
</tr>
<tr>
<td>state_changed_at</td>
<td>at this time the project status changed. Status could be successful, failed, suspended, cancelled etc. (in unix timeformat)</td>
</tr>
<tr>
<td>created_at</td>
<td>at this time the project was posted on the website(in unix timeformat)</td>
</tr>
<tr>
<td>launched_at</td>
<td>at this time the project went live on the website(in unix timeformat)</td>
</tr>
<tr>
<td>backers_count</td>
<td>no. of people who backed the project</td>
</tr>
<tr>
<td>final_status</td>
<td>whether the project got successfully funded (target variable – 1,0)</td>
</tr>
</tbody>
</table>

## Custom features

<table>
<thead>
<tr>
<th>Variable</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>goal_usd</td>
<td>goal converted to USD using historic exchange rate</td>
</tr>
<tr>
<td>keywords_len</td>
<td>length of keywords</td>
</tr>
<tr>
<td>keywords_count</td>
<td>number of keywords</td>
</tr>
<tr>
<td>name_len</td>
<td>length of project name</td>
</tr>
<tr>
<td>name_count</td>
<td>number of words in project name</td>
</tr><tr>
<td>desc_len</td>
<td>length of description</td>
</tr>
<tr>
<td>desc_count</td>
<td>number of words in description</td>
</tr>
<tr>
<td>name_capitals</td>
<td>number of uppercase letters in project name</td>
</tr>
<tr>
<td>name_digits</td>
<td>number of digits in the project name</td>
</tr>
<tr>
<td>name_digits_any</td>
<td>boolean indicating whether there are any digits in project name</td>
</tr>
<tr>
<td>desc_digits</td>
<td>number of digits in description</td>
</tr>
<tr>
<td>launched_at_weekday</td>
<td>day of week when the campaign was launched</td>
</tr>
<tr>
<td>deadline_weekday</td>
<td>day of week of campaign deadline</td>
</tr>

<tr>
<td>campaign_len</td>
<td>campaign length</td>
</tr>
</tbody>
</table>

## Conclusion

After experimenting with several algorithms (Naive Bayes, SVM) and selecting optimal features & parameters using `KBest` and `GridSearchCV` respectively, I settled on `AdaBoost` with thw following features:

```
['campaign_len'
 ,'keywords_count'
 ,'keywords_len'
 ,'name_count'
 ,'name_capitals'
 ,'desc_digits'
 ,'name_digits_any'
 ]
```

This led to a prediction score of `0.67484` on the test version of the dataset.

## Ideas for improvement

Seasonality is something that could be explored further. I found that the day of the week when the campaign starts or finishes play no role in the outcome, but longer-term seasonal fluctuations are likely. Could there be a downturn in funding around summer? or an upturn around the time when people get bonuses?
