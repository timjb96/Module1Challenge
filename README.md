
# Project Overview
The goal of this analysis is to better understand how different Kickstarter Campaigns fared based on their launch dates and fundraising goals. Specifically, we will be looking at how campaigns for theater projects fared according to their launch date, and how specifically plays fared according to their goal amounts. This analysis could be used in order to better understand when a campaign should be launched, and how much its goal should be, in order to maximize its earnings. 
##Analysis and Challenges

This Analysis was done from general Kickstarter data, sourced from a variety of different project categories from late August 2009 to early March, 2017, and sorted into categories that describe fundraiser dates, success status, type of fundraiser, and donor metrics. As we wanted to specifically understand how project launch date and goal amount affected the potential success of a project, two analytical processes were applied. Prior to this, several extra columns were created, to determine parent category and subcategory, transition the unix timestamp date format to traditional date format, and to specify the years of the fundraisers. The date was converted using the following code:

=(((J2/60)/60)/24)+DATE(1970,1,1)


First, we examined the outcomes based on launch date. This was done by using excel to organize the raw data into a pivot table, filtered by parent category and year, and then months. The outcomes were selected as the columns, and the date was selected for the rows. The count of outcomes for specific outcomes was set as our values for this chart. Row labels were also grouped by month, to show us data by specific months. 

![Screen Shot 2022-09-16 at 10 12 54 AM](https://user-images.githubusercontent.com/112847821/190718486-b36530ff-7e83-461e-83b3-26f95384281b.png)

Screen Shot 2022-09-16 at 10.14.37 AM.png
This returned the following table:

![Screen Shot 2022-09-16 at 10 14 37 AM](https://user-images.githubusercontent.com/112847821/190718467-c6368725-060d-441d-9e15-78841ea550dc.png)

To visualize this data better, we then created the following chart:
![Theater_Outcomes_vs_Launch](https://user-images.githubusercontent.com/112847821/190718089-c24ede9e-9917-4fdf-a6de-eb1df9b1e55f.png)

This chart allows us to better interpret the outcomes of fundraisers for theater projects based on launch month. 
With our data visualization of Outcomes Based on Launch Date completed, we could move on to examining outcomes based on goals. To do this, we used the CountIf function within excel to count how many projects fell into which category of successes and failures based on what goal amount they launched their projects with. The following three codes formats were used to complete this from the table of raw data, to return respectively columns for successful, failed, and canceled projects in $5,000 dollar intervals. 

=COUNTIFS('Kickstarter Data'!$D:$D,"<1000",'KickstarterData'!$F:$F,"successful",'Kickstarter Data'!$R:$R,"plays")

This function counts the following, separated into its separate statements:
‘Kickstarter Data'!$D:$D,"<1000", counts the number of projects in the kickstarter data with goals (in Column D) that are less than $1000.
'KickstarterData'!$F:$F,"successful" counts the number of projects that show as successful in Column F
'Kickstarter Data'!$R:$R,"plays" counts the number of projects in the ‘play’ subcategory of theater. 
Combined into one statement, these three attributes combine to count the number of successful plays launched with a goal of under $1000. To delineate an intermediary range, a lower and higher bound goal range is implemented:

=COUNTIFS('Kickstarter Data'!$D:$D,">999",'Kickstarter Data'!$D:$D,"<5000",'Kickstarter Data'!$F:$F,"successful",'Kickstarter Data'!$R:$R,"plays")

with 'Kickstarter Data'!$D:$D,">999",'Kickstarter Data'!$D:$D,"<5000" being the two statements that determine the range- the full statement would return all successful projects in the ‘play’ subcategory with a launch goal between $1000 and $5000. 
This process was applied to the three conditions within the raw data column F, to count the successful, failed, and canceled projects in each range. These were then summed to determine the total project launch count for each interval, which was then used to calculate the percentage of each, which we visualized using a scatter plot with connected lines- the table and chart formed for this analysis can be found below:
![Screen Shot 2022-09-16 at 10 44 55 AM](https://user-images.githubusercontent.com/112847821/190718057-5b9d8fd3-56d0-4fdd-9dc4-19cc34a0dd9a.png)


![Outcomes_based_on_goals](https://user-images.githubusercontent.com/112847821/190717821-fe0ba6b0-5c4e-4cb7-b39f-bfe3932b4209.png)

The main challenges that I ran into during this analysis were some formatting issues, and a slight misinterpretation of the original instructions – I had missed the option to filter the CountIfs in the second analysis with sufficient enough conditions, and at first had the data filtered to not only include the subcategory of plays. 

## Results


### What are two conclusions you can draw about the Theater Outcomes by Launch Date?
May is the best time to launch a fundraiser, as that is when the greatest number of successes are, and greatest gap between successful and failed projects. December is the worst time of year to start a fundraiser, as the number of successful projects drop to its lowest point, and the smallest gap between successful and failed project count.  
###What can you conclude about the Outcomes based on Goals?
The lower your goal is, the more likely you are to succeed. However, there is a sweet spot for projects with a goal of $30,000-$40,000, where there is an increase in successes. 
###What are some limitations of this dataset?

The biggest limitation is that this dataset ends in 2017- as it is 5 years later, there is presumably a large amount of data that would have been uploaded by now, and would make our analysis more exact and specific. Especially due to world events in the past 5 years that have dramatically affected both the US economy and the economic standing of a number of possible donors, this dataset will not provide us the most up to date information on donor habits and patterns, as donor interest and donateable income may have changed significantly in a number of cases. Especially since theater/play performances are a primarily indoor activity, the recent pandemic could have drastically affected not just the metrics of theater based fundraisers, but the actual number of theater based fundraisers.
Another limitation is that this dataset is only for Kickstarter fundraising campaigns. If Louise wanted an exhaustive overview of fundraising data to form a strategy for future fundraisers, it would be helpful to also include data from other fundraising platforms such as GoFundMe and Patreon. Although these platforms are geared towards slightly different projects, the data could still be useful in understanding trends in how donors choose how much, when, and where to donate, and would provide an additional level of filtering. 
Additionally, the dataset does not have a 1:1 match for the dates included and the data for them- as it starts in late August 2009 and ends in March of 2017, the data sets for March, April, May, June, July, and August will not be as exact as the data sets for the other 6 months that had 8 years of data, as opposed to the 7 that March-August have making up their data set. As we are missing these six months, we must accept that the data for March, April, May, June, July, and August, may not be as accurate as the data and conclusions for the other 6 months. This does not represent a significant error or failure in our data, but should be noted still. 
### What are some other possible tables and/or graphs that we could create?



We could first examine other aspects of donations and factors that might
determine or contribute to success or failure of a fundraiser. We could examine donor count and donation size per donor to better understand how much an average donor gives at different times of year or in response to different goal amounts, or even by type of project. This would help to refine goal and launch information based on how many donors Louise could expect for a fundraiser. 
We could also create graphs comparing similar success metrics across different fundraiser categories, and chart trend lines that compared how theater fundraisers compared to photography fundraisers, or publishing, or music- we could use this to determine more generalized information about donor habits that would give us more context on how theater fundraisers perform. 





