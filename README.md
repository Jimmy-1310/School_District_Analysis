# School_District_Analysis

## Overview of the Project
During this module, we were taks with the challenge of getting the school district metrics. This metrics consisted of average scores, percentage of students that passed the subject, and the overall passing percentage. To do this, we used two CSV files that contained information about the schools in the district and the students of this schools. The analysis needed to be done to the whole distict, to each individual school and also analysing the perfermance based on syze, type, and population of students. 

After this, we found that that the 9th grade students at Thomasn High School cheated on their tests. Although we do not know the extend of this dishonesty and how many students actually cheated, the school board decided to eliminate the scores and run the analysis again. We can not make the grades equal to 0, because that would change the story we are trying to tell. If we did this, the story the data will tell is that the 9th grade students of the school did not learnt anything and failed their tests, which is probably not true. To avoid this we are simply going to ignore them and recalculate any average or percentage affected.

For this challenge we learn and used how to create virtual enviroments, how to use a jupyter notebook and all the benefits it has as a developing tool; Lastly we used the pandas library to calculate the metrics in an easier and simplier way.

## Results

- **How is the district summary affected?**
The original district summary looked a bit like this:

![original_district_metrics](https://user-images.githubusercontent.com/95836718/150239647-f193e8ad-b51e-44e2-8bff-358def938b36.png)

Before calculating the new district metrics we need no adress a discrepancy. If we used the same code and methos as the original, we will see very differents metrics. We first need to recalculate the total ammount of students withouth the 9th graders from Thomas High School. To get the total count of 9th graders can be retrieved and count it with the loc function:

> thomas_9th_graders=school_data_complete_df.loc[(school_data_complete_df["school_name"]=="Thomas High School") & (school_data_complete_df["grade"]=="9th")].count()["Student ID"]

Now we can susbtract this number from the total student count. I did this by creating a new variable to hold this number to not affect the original variable and total student count. This was done with the purpouse of showing the complete ammount of students (including the 9th graders) instead of completele ignoring the 9th graders from all DataFranes. Once we susbstract this number, we can continue with our analysis and our new district summary will look like this:

![school_district](https://user-images.githubusercontent.com/95836718/150239994-736b2e57-cfec-4441-8d37-ae8a1519ff9c.png)

The average remained overall the same and the percentages were reduced but not in a significant way. We can see that the metrics remainec all in all the same without any significant change

- **How is the school summary affected?**
For this section, we can focuse specifically in the Thomas High School row, because the rest of the DataFrame remained untouched. The original Thomas High School row looked like this:

![thomas_original](https://user-images.githubusercontent.com/95836718/150277159-0ffd5bc9-b896-4183-adf3-25a22ade74fc.png)


Once we run the school analysis when replacing all the values in the 9th graders from Thomas High School to *NaN* it will show this:

![Uncalculated Thomas Data](https://user-images.githubusercontent.com/95836718/150277197-de99cda4-69ec-4bf9-ac4e-b79671f2f379.png)

There is something wrong with this metrics. If we follow the story this data is telling us, Thomas High School is underperforming academically because a whole grade did not passed any of the two classes. This is not true, even if the school board decides to fail the whole grade this has nothing to do with their academic performance or the teaching methods of the teachers in regards to the topics. To avoid this and tell a correct story we need to substract the ammount of 9th graders from the total students of Thomas High School with the next lines of code:

> thomas_hs_students=school_data_complete_df.loc[school_data_complete_df["school_name"]=="Thomas High School"].count()["Student ID"]

> thomas_hs_students_df=school_data_complete_df.loc[school_data_complete_df["school_name"]=="Thomas High School"]

> thomas_hs_new_students=thomas_hs_students-thomas_9th_graders

Once we have this number, we can recalculate the metrics and they will look like this:

![calculated_thomas_data](https://user-images.githubusercontent.com/95836718/150277231-53f58092-5c0b-43a8-8408-29e6f43e7e2b.png)

- **How does it affect Thomas High School performance regarding other schools?**
In the original analysis we can see that Thomas High School is ranked as the second best performing school in the district.

![top5_original](https://user-images.githubusercontent.com/95836718/150273171-a5739e51-0bbe-41dc-b53c-8ddaeee51b77.png)

Analysing and reviewing the Thomas High School data without recalculating, it is easy to see how its performance will be damage. It would not be as bad to be in the bottom 5, but it certainly would not be on the top 5 performing schools. With the correction data we can see that there is no significat difference to the analysis.

![top5](https://user-images.githubusercontent.com/95836718/150273409-a506f6b1-0d07-4861-a7a5-ced6cbe911a0.png)

- **How does it affect the Math and Reading scores by grade.**
For the original performance by grade we got the next result:
**Math Score**

![mathscores_grade_original](https://user-images.githubusercontent.com/95836718/150274084-1c2d386b-5800-4415-b47c-03f2a0b7de97.png)

**Reading Score**

![redingscores_grade_original](https://user-images.githubusercontent.com/95836718/150274114-06f2e87a-32c4-46fc-903e-31d4e2311c4d.png)

To update it, we can not add a "0" as the score for the 9th graders of Thomas High School, because that will be telling a different story than the reality. For this we are going to supplement the values with a *Nan (Not a Number)* so the outcome will be as follows:

**Math Scores**

![math_scores_bygrade](https://user-images.githubusercontent.com/95836718/150274395-8aec8214-2fc5-466e-82d2-303dc80d8da9.png)

**Reading Scores**

![readingscores_by_grade](https://user-images.githubusercontent.com/95836718/150274442-1b1acd07-70ca-42c3-b2ac-09964d24a721.png)

We can see how their grades were replaced with a NaN.

- **How does it affected the scores by school spending**
The original scores were:

![spending_original](https://user-images.githubusercontent.com/95836718/150274569-150cafe1-59c3-4be3-b322-e739a597ab7f.png)

Because we calculate the percentages and data with by getting the means of each bin in the updated school summary dataframe, there will not be any significant difference in the outcomes. 

![spending](https://user-images.githubusercontent.com/95836718/150274674-f50fb572-fcfe-4d6d-99cf-41554ac5f1e4.png)

- **How does it affect the scores by school size**
The original score were:

![size original](https://user-images.githubusercontent.com/95836718/150274799-dfc393d6-abba-4b53-bd66-6832de06e6aa.png)

The updated outcome was:



It is the same case as the score by spending, there is no significant decision to actually make a different decision or reconcider any previous analysis.

![size](https://user-images.githubusercontent.com/95836718/150274917-454218c4-8ac6-4668-8ccf-709e902cfd34.png)

- **How does it affect the scores by school type?**
The original outcomes was:

![type_original](https://user-images.githubusercontent.com/95836718/150275053-8c1f3090-0350-4bb6-82ff-cca4350f2207.png)

And as same as before, there will not be any major difference in the updated outcome:

![size](https://user-images.githubusercontent.com/95836718/150275035-39a5e83f-f0ab-4659-8816-95a85c7790f3.png)

## Summary

Changing the scores of the 9th graders of Thomas High School sure made the data tell a different story than the reality. Replacing the values to NaN created a discrepancy with the ammount of grades and the ammount of students that were being used to calculate percentages of students that passed. This changes affected the *total number of students* that were being used to calculate the district metrics, and also the *total number of students in Thomas High School* to calculate its metrics. Eventhough the numbers needed to be updated to change the metrics, the actual numbers of students still needed to be shown to paint the full picture with the data. Another change was the substitution of the 9th graders scores in Thomas High School with an NaN. This change can be seen in the math and reading scores by grades. Lastly, we can see some changes in the percentages in the analysis done by population, spending per student, and size. This changes are not that important because they do not vary more than 0.5 points. 

With this analysis updated, the school board can analyze and see the full picture of the district while also substitung the 9th graders score because of the situation. The dataset is ready to be analyze to then be used to determine important decisions that will help improve the quality of the schools and performance of the district.
