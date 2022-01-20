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

![Original_Thomas_Data](https://user-images.githubusercontent.com/95836718/150241420-c0d7dba0-5ae5-4237-ae18-6649a10e25c2.png)

Once we run the school analysis when replacing all the values in the 9th graders from Thomas High School to *NaN* it will show this:

![Thomas_Uncalculated](https://user-images.githubusercontent.com/95836718/150241615-2ab90748-9936-4269-a8f8-ecc5df94ae07.png)

There is something wrong with this metrics. If we follow the story this data is telling us, Thomas High School is underperforming academically because a whole grade did not passed any of the two classes. This is not true, even if the school board decides to fail the whole grade this has nothing to do with their academic performance or the teaching methods of the teachers in regards to the topics. To avoid this and tell a correct story we need to substract the ammount of 9th graders from the total students of Thomas High School with the next lines of code:

> thomas_hs_students=school_data_complete_df.loc[school_data_complete_df["school_name"]=="Thomas High School"].count()["Student ID"]

> thomas_hs_students_df=school_data_complete_df.loc[school_data_complete_df["school_name"]=="Thomas High School"]

> thomas_hs_new_students=thomas_hs_students-thomas_9th_graders

Once we have this number, we can recalculate the metrics and they will look like this:

![Thomas Updated](https://user-images.githubusercontent.com/95836718/150242822-12284afb-85e7-4751-87a1-d73bf447757b.png)

- **How does it affect Thomas High School performance regarding other schools?
