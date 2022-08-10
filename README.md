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

But first  - let's finite the notebook. 

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
 ~~The MP files then must have less stuff.
 But they still have 154. Why? 
 Ask Hella. ~~
 </strike>
Hella explained that MP scenarios are run for all 24 hours, but the capacities are changed to AV level only for the Morning Peak hours. 

~~TODO:  Ask Hella - where does the 'pt' public transport tag come from?
Probably in the first column - saw some labels.  ALthough not specifically pt. 


## 10th August

Let's start today by removing transit links. Done. 

Now rewriting code in an efficient way. 


How do I view a chunk of data in a dataframe? 
Use loc
https://sparkbyexamples.com/pandas/how-to-slice-columns-in-pandas-dataframe/


~~Did  `linkstats_S1MP_major.iloc[:, 50:55]     # 6 to 11 pm  Travel Time`
Showed values. But then why is this for Morning Peak only? 
TODO: Ask Hella - the definition of MP scenario~~


Tring to do strikethroughs. This seems helpful https://stackoverflow.com/questions/41395000/strikethrough-code-in-markdown-on-github





















