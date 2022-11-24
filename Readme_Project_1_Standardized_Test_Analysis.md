# Project 1: Standardized Test Analysis

## Background

ACT and SAT are standardized tests that many colleges and universities in the United States require for their admissions process. ACT or SAT score is used along with other materials such as grade point average (GPA) and essay responses to determine whether or not a potential student will be accepted to the university.

SAT has two sections of the test: Evidence-Based Reading and Writing and Math ([*source*](https://www.princetonreview.com/college/sat-sections)) whereas ACT has 4 sections: English, Mathematics, Reading, and Science, with an additional optional writing section ([*source*](https://www.act.org/content/act/en/products-and-services/the-act/scores/understanding-your-scores.html)). 

Both SAT and ACT have different score ranges, which are available on their websites:
* [SAT](https://collegereadiness.collegeboard.org/sat)
* [ACT](https://www.act.org/content/act/en.html)

There are states that require high school students to take standardized test for graduation. This requirement provides every student with a chance to take a college admissions test and encourages students to consider college to apply based on test score.([*source*](https://blog.prepscholar.com/which-states-require-the-act-full-list-and-advice)).


## Problem Statement

This project uses various methods of data analysis and visualization to analyze data from SAT and ACT college entrance exams in year 2017, 2018 and 2019. Hence, this project aims to tackle one central question: 

##### Does high state's participation rate in either ACT or SAT lead to higher test score in respective test?

### Contents:

- Data Import and Cleaning
- Exploratory Data Analysis
- Conclusions
- Recommendations


## Data Import, Cleaning & Exploratory Analysis

### Data Import

These are 6 datasets (from year 2017 to 2019) used to complete the analysis:
act_2017, act_2018, act_2019, sat_2017, sat_2018 and sat_2019


### Cleaning

Data was cleaned up (including fixing data issues and renaming columns' names to snake case) and then merged into new dataframes for analysis.

Below is a list of data issues found and cleaned up for analysis.
  - These rows: 'National', 'District of Columbia', are in ACT 2017 and ACT 2019 but not in ACT 2018. 
    'National' has been removed from modified datasets ACT 2017 and ACT 2019.
  - This row: 'District of columbia', is in ACT 2018 but not in both ACT 2017 and ACT 2019. 
    'District of columbia' has been renamed as 'District of Columbia' in modified dataset ACT 2018.
  - These 2 rows: 'Puerto Rico', 'Virgin Islands', are in SAT 2019 but not in SAT 2017 and SAT 2018. 
    These 2 rows have been removed from modified dataset SAT 2019.
  - These 4 columns: 'English', 'Math', 'Reading', 'Science', are in ACT 2017 but not in both ACT 2018 and ACT 2019.
    These 4 columns have been removed from modified dataset ACT 2017.
  - These 2 columns: 'Participation', 'Evidence-Based Reading and Writing', are in SAT 2017 and SAT 2018 but not in SAT 2019.
    These 2 columns have been removed from modified datasets SAT 2017 and SAT 2018.
  - These 2 columns: 'Participation Rate', 'EBRW', are in SAT 2019 but not in SAT 2017 and SAT 2018.
    These 2 columns have been removed from modified dataset SAT 2019.
  - Dataset ACT 2017 Science column has 1 outlier at 2.3.
    The outlier has been replaced as 20.2, which is its mean, in modified dataset ACT 2017.
  - Dataset ACT 2018 has 1 duplicate state: Maine, in row 20.
    Duplicate record has been removed from modified dataset ACT 2018.
  - Dataset SAT 2019 column Participation has unique character "-" in addition to "%".
    Both unique characters have been removed to amend Participation column datatype from object to integer.
  - Datasets ACT 2017, ACT 2018, ACT 2019, SAT 2017 and SAT 2018 column Participation has unique character "%".
    Unique character has been removed to amend Participation column datatype from object to integer.

Each merged dataframe's descriptions ([ACT Source](https://blog.prepscholar.com/act-scores-by-state-averages-highs-and-lows))([SAT Source](https://blog.collegevine.com/here-are-the-average-sat-scores-by-state/)) are in section Data Dictionary below. 

#### Data Dictionary

Merged dataframes combined_modified_act_2017_2018_2019:

|Feature                   |Type    |Dataset                |Description                                                                                                                                   |
|--------------------------|--------|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|**state**                 |*object*|ACT 2017, 2018 and 2019|All states in United States of America (exclude Puerto Rico and Virgin Islands).                                                              |
|**participation_act_2017**|*float* |ACT 2017, 2018 and 2019|Participation rate of the state in ACT for year 2017.                                                                                         |
|**composite_act_2017**    |*float* |ACT 2017, 2018 and 2019|Composite score for year 2017 is the average of four test scores: English, mathematics, reading, science; range from 1 (low) to 36 (high) and rounded to the nearest whole number.|
|**participation_act_2018**|*float* |ACT 2017, 2018 and 2019|The participation rate of the state in ACT for year 2018.                                                                                     | 
|**composite_act_2018**    |*float* |ACT 2017, 2018 and 2019|Composite score for year 2018 is the average of four test scores: English, mathematics, reading, science; range from 1 (low) to 36 (high) and rounded to the nearest whole number.|
|**participation_act_2019**|*float* |ACT 2017, 2018 and 2019|The participation rate of the state in ACT for year 2019.                                                                                     | 
|**composite_act_2019**    |*float* |ACT 2017, 2018 and 2019|Composite score for year 2019 is the average of four test scores: English, mathematics, reading, science; range from 1 (low) to 36 (high) and rounded to the nearest whole number.|


Merged dataframes combined_modified_sat_2017_2018_2019:

|Feature                   |Type    |Dataset                |Description                                                                                                                                   |
|--------------------------|--------|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|**state**                 |*object*|SAT 2017, 2018 and 2019|All states in United States of America (exclude Puerto Rico and Virgin Islands).                                                              |
|**participation_sat_2017**|*float* |SAT 2017, 2018 and 2019|The participation rate of the state in SAT for year 2017                                                                                      |
|**total_sat_2017**        |*float* |SAT 2017, 2018 and 2019|Total score for year 2017 is the sum of the two sections: evidence-based reading and writing section and math section; range from 400 to 1600.|
|**participation_sat_2018**|*float* |SAT 2017, 2018 and 2019|The participation rate of the state in SAT for year 2018.                                                                                     | 
|**total_sat_2018**        |*float* |SAT 2017, 2018 and 2019|Total score for year 2018 is the sum of the two sections: evidence-based reading and writing section and math section; range from 400 to 1600.|
|**participation_sat_2019**|*float* |SAT 2017, 2018 and 2019|The participation rate of the state in SAT for year 2019.                                                                                     | 
|**total_sat_2019**        |*float* |SAT 2017, 2018 and 2019|Total score for year 2019 is the sum of the two sections: evidence-based reading and writing section and math section; range from 400 to 1600.|


Merged dataframes combined_act_sat_2017_2018_2019:

|Feature                   |Type    |Dataset                |Description                                                                                                                                   |
|--------------------------|--------|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|**state**                 |*object*|ACT 2017, 2018 and 2019|All states in United States of America (exclude Puerto Rico and Virgin Islands).                                |
|**participation_act_2017**|*float* |ACT 2017, 2018 and 2019|Participation rate of the state in ACT for year 2017.                                                           |
|**composite_act_2017**    |*float* |ACT 2017, 2018 and 2019|Composite score for year 2017 is the average of four test scores: English, mathematics, reading, science; range from 1 (low) to 36 (high) and rounded to the nearest whole number.|
|**participation_act_2018**|*float* |ACT 2017, 2018 and 2019|The participation rate of the state in ACT for year 2018.                                                       | 
|**composite_act_2018**    |*float* |ACT 2017, 2018 and 2019|Composite score for year 2018 is the average of four test scores: English, mathematics, reading, science; range from 1 (low) to 36 (high) and rounded to the nearest whole number.|
|**participation_act_2019**|*float* |ACT 2017, 2018 and 2019|The participation rate of the state in ACT for year 2019.                                                       | 
|**composite_act_2019**    |*float* |ACT 2017, 2018 and 2019|Composite score for year 2019 is the average of four test scores: English, mathematics, reading, science; range from 1 (low) to 36 (high) and rounded to the nearest whole number.|
|**participation_sat_2017**|*float* |SAT 2017, 2018 and 2019|The participation rate of the state in SAT for year 2017                                                        |
|**total_sat_2017**        |*float* |SAT 2017, 2018 and 2019|Total score for year 2017 is the sum of the two sections: evidence-based reading and writing section and math section; range from 400 to 1600.|
|**participation_sat_2018**|*float* |SAT 2017, 2018 and 2019|The participation rate of the state in SAT for year 2018.                                                       | 
|**total_sat_2018**        |*float* |SAT 2017, 2018 and 2019|Total score for year 2018 is the sum of the two sections: evidence-based reading and writing section and math section; range from 400 to 1600.|
|**participation_sat_2019**|*float* |SAT 2017, 2018 and 2019|The participation rate of the state in SAT for year 2019.                                                       | 
|**total_sat_2019**        |*float* |SAT 2017, 2018 and 2019|Total score for year 2019 is the sum of the two sections: evidence-based reading and writing section and math section; range from 400 to 1600.|


### Exploratory Analysis

It is noted that:
- from year 2017 to 2019, mean, median and minimum of ACT participation and composite were on downward trend.
- from year 2017 to 2019, both mean and median of SAT participation have increased while its mean and median of total SAT scores have decreased. 
- In year 2017, Colorado and Minnesota had 100% participation rate in ACT but their participation rates have dropped in year 2018 in which Colorado participation rate dropped to 30% in year 2018. Similarly, in year 2018, both Missouri and South Carolina had 100% participation rate but their participation rates have dropped in year 2019.
- from year 2017 to 2019, for both ACT and SAT college entrance exams, there is a negative correlation between 
  - ACT composite and ACT participation; 
  - SAT total and SAT participation;
  - ACT participation and SAT participation; and
  - ACT composite and SAT total scores (negative correlation is weak as it is less than -0.5).


## Conclusions

It is noted that, from year 2017 to 2019, for both ACT and SAT college entrance exams, there is a negative correlation between 
- ACT composite and ACT participation; 
- SAT total and SAT participation;
- ACT participation and SAT participation; and
- ACT composite and SAT total scores (negative correlation is weak as it is less than -0.5).

#### Negative Correlation between ACT composite and ACT participation; and SAT total and SAT participation

This pattern exists and is consistent with external research ([*source*](https://blog.prepscholar.com/average-sat-and-act-scores-by-stated-adjusted-for-participation-rate)) on states' participation and scores whereby the scores are biased because a state’s with low participation in either ACT or SAT will only have the best students taking the exam. This makes the score artificially high. Likewise, if a state requires either ACT or SAT, it will have 100% participation but also include the worst exam takers who didn't study much and naturally not good at the exam, making the score artificially low.

#### Negative Correlation between ACT Participation and SAT Participation

This pattern exists and is consistent with external research ([*source*](https://blog.prepscholar.com/which-states-require-the-sat)) on states participation pattern in ACT or SAT whereby states that require all students to take only 1 exam, either ACT or SAT, as required by respective state, do not participate in another exam.

#### Negative Correlation between ACT Composite and SAT Total Scores

This pattern exists because according to external research ([*source*](https://blog.prepscholar.com/which-states-require-the-sat)), building on the negative correlation with participation rates, students taking the SAT and ACT exams differ systematically. Hence, average capability of a student taking one exam simply does not match the average student taking the other.

Hence, increasing state's participation rate in either ACT or SAT college entrance exams will not to lead an improvement in respective exam score.


## Recommendations

As study is based on past years data (from year 2017 to 2019) and there is bias in respective exam score, to sharpen analysis, it is recommended to incorporate additional data from year 2020 to 2022 and to adjust states' ACT or SAT scores by comparing the scores against other states with similar participation rates.
([*source*](https://blog.prepscholar.com/average-sat-and-act-scores-by-stated-adjusted-for-participation-rate))
