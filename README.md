# HOV-AV_paper
This repository contains the analysis work of Hella's HOV lanes for AV paper. 


## 26th July 2022

Figured out a good way to store the large data files without copying them several times. And also load them from one place regardless of whatever notebook I will be working on. 

Also, knocked Fan Zuo for help and he came over and explained the results files data headers clearly and narrated through one agent's entire day.  For my personal visualization, it is important for me to just look at the dep_time and trav_time values. 


Explored the `Counter` subclass from `collections`. 


## 2nd August 2022

Wanted to find out the actual population.  Tried to do it from the counter.  Because it gives the number of trips for each agent. But I couldn't figure out a way to find the 'len' of a counter object. 

Actually it would be easier to just find the number of unique values in the ID column. 

https://www.geeksforgeeks.org/how-to-count-distinct-values-of-a-pandas-dataframe-column/



## 4th August 2022

Calculated the modal split. 


Calculated the average travel time  and distance for base scenario. 

Now do it for S1 scenario. 


## 5th August 2022

Trying to redo everything so far in a clean manner. 

Can I plot the ridership?

First, how do I see what kind of variable a variable is? Sol: Use `type(variable)`

Ok, plotted some bar charts. 

Now how do I see the quick increase decrease difference between the two scenarios?


## 9th August 2022

TODO:   Check the difference between two scenarios above. 

But first  - let's finish the notebook. 

Opened a new notebook to do clean analysis and add my stuff.

Original notebook is only going to be used for Hella's work exploration and my draft ideas. 


----------

Tried to generate CSV files from XML files for Scenario 2 and 3.  Hella gave me a Python notebook she received from Ding, which does this conversion. 

However, the entire thing took so long!  I think I waited for 1.5 hours.  Hella had mentioned, on Desktop it took about 20 minutes. 

Anyway will take the files generated by Hella before. 

However I think I had developed the correct process. It was only my laptop which is not powerful enough. 

Process for future: 

1. Download xml.gz files. 
2. Extract using 7-zip. Will get xml file. 
3. Modify the path names in the Python notebook (both for the input xml files and the output result.csv and score.csv files)
4. Run it

-------


Loaded all scenarios. Doublechecked that they are distinct. The first 6 ([ 0:5] ) entries gave all same.  But then did [10:25] index, got different results. 

Visualized modal split for all. 

Got rid of unnecessary legend.  https://www.geeksforgeeks.org/how-to-remove-the-legend-in-matplotlib/




Now plotted all together to see the difference. Unfortunately some issues

* only base is different
*  S1 , S1MP, S3, S3MP all same.  S2 and S2MP different just because the modes are in different order. 




--------

LINK LEVEL ANALYSIS

1.  Collect the linkstats files for each scenario - 
2.  Extract gz files to get the txt files. 
3. Load them 
4. Reduce the dataframe sizes by keeping only the avg values and getting rid of the max and min values. 
5.  Get rid of the rows representing transit links. 



TODO:  Understand the headers and the units for each header.  Why are the min, avg, max same for travel times? 


 here are 154 columns/ headers! Wow! First some basic link characteristics, then hour wise 'HRS' and travel times.
 <strike>
 The MP files then must have less stuff.
 But they still have 154. Why? 
 Ask Hella. 
 </strike>
Hella explained that MP scenarios are run for all 24 hours, but the capacities are changed to AV level only for the Morning Peak hours. 

<strike>TODO:  Ask Hella - where does the 'pt' public transport tag come from?
Probably in the first column - saw some labels.  ALthough not specifically pt. </strike>


## 10th August

Let's start today by removing transit links. Done. 

Now rewriting code in an efficient way. 


How do I view a chunk of data in a dataframe? 
Use iloc
https://sparkbyexamples.com/pandas/how-to-slice-columns-in-pandas-dataframe/


~~Did  `linkstats_S1MP_major.iloc[:, 50:55]     # 6 to 11 pm  Travel Time`
Showed values. But then why is this for Morning Peak only? 
TODO: Ask Hella - the definition of MP scenario~~


Tring to do strikethroughs. This seems helpful https://stackoverflow.com/questions/41395000/strikethrough-code-in-markdown-on-github

Now we will find average volume by hour. 


TODO:  Ask Hella.  Is HRS really volume.  ANd is TRAVELTIME really speed.  What are the units. 


TODO: Ask Hella/ Farnoosh 
ISSUE - The index issue - why does `iloc[:, 32:56]` works but if I do `iloc[:, 56]`, it says out of bounds?


Calculated new dataframes that holds mean hourly volumes and mean hourly speed over 24 hours for each scenario. 

Let's take a look at it graphically. 

How do I change the x-ticks to make them clearer? 

This should be helpful in the future: https://stackoverflow.com/questions/12945971/pandas-timeseries-plot-setting-x-axis-major-and-minor-ticks-and-labels

FOr the time being let's just make it vertical

Also helpful: https://stackoverflow.com/questions/44813601/how-to-set-x-axis-values-in-matplotlib-python 
But having trouble defining 'x'

## 11th August 2022

Figured out the problem with the mode order for scenario 2 in modal split calculation.  Basically, counter item is a dictionary item and it follows insertion order.  
In Scenario 2 probably - that particular mode came first. 

We can reindex. https://stackoverflow.com/questions/46890972/swapping-rows-within-the-same-pandas-dataframe

This reindexing didn't work.  It switches the indexes all right but turns values into NaN


Hella working with me in office.  
* Figuring out FID  -  It's an unique identifier in the shape file. 
* We figured out the units of all the headers in the Linkstats file. 




## 24th September 2022

Added scenario description details. 

## 25th September 2022

Reread the above. 


Goal is to solve the reindexing issue of 'ridership' data.  So that the ridership info for all scenarios have the modes in the same order. 

Instead of trying to use reindexing strategies for the troublesome scenarios which didn't work earlier, we will simply use sorting of rows is alphabetical order for ALL scenarios. 


Sorting is learned from https://chrisalbon.com/code/python/data_wrangling/pandas_sorting_rows_dataframe/


## 26th September

Loaded link data for all 7 scenarios.


Clean up max and min values ( keep only avg). And remove public transit info.  The first cleanup removes columns.  Second cleanup (public transit removes rows). 

Set aside data for major links by keeping only the links with freespeed 9m/s and higher.  QUESTION: Won't this be same for all scenarios? Is it necessary to do eat for each scenario? Just have an index of links where freespeed in 9m/s and higher? 

Wait, what is that freespeed? It will change with capacity, right?

Checked the generated 'major' link dataframes.  Exact same number of rows for all 7 scenarios.  So we could have just used the index of base and applied it for all (TODO WHEN TIME). 



## 5th October

Set up original copy of Hella's analysis.  Her 'f4' naming was getting very confusing with my 'S1', 'S1_MP' namings in the Walkthrough notebook. 

Just running each cell slowly and deliberately took half and hour. 


NOTE: Instead of rename the link column in all the different scenario dataframes (7+7=14 dataframes), why don't I just rename the borough file's ID to LINK and then match that ?  Yes, we can! 

I think I found the origin of error for which the graphs weren;t showing any different scenario to scenario for linkstat analysis! Was loading S1 and S1MP for S2,S3 and their MPs respectively! No wonder :/ 

PROBLEM:  Want to extract gz file to get txt files.  According to previous notes about, use 7-zip. But when I select gz file, 'Extract' option doesn't come automatically.  
SOLUTION: Open the 7-zip program explicitly and  extract the gz file from there. 

Graphs look promising now. 

## 6th October

Continuing to make volume_compare dataframe of each borough.  


UNITS

Volume:  vehicles/hour
Travel time :  in hours

[Source: MATSim Book 2016] 


Check whether 7:31 is indeed volume 32:56 is indeed travel time. Both ranges (substraction) gives 24.   Tried things like: `StatIsland_S3.iloc[1:5, 7:31]`.  Yes, both ranges are correct. 


PROBLEM
Trying to figure out whether there is a 'search and replace' option in firefox.  So far no good answer :/ https://superuser.com/questions/463342/how-can-i-search-and-replace-in-firefox

Better query was 'find and replace in jupyter'. Showed me a 'find and replace' option under edit. But it does 'replace all' :/  No way to do a few replacement

SUGGESTION IDEA for Jupyter


## 12th October

Downloading graphs for Hella - borough-wise.  Need a smarter way to do this. 


