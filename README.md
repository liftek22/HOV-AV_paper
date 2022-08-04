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
