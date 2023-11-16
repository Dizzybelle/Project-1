# Project-1
Project Title: Assessing Crash Data from Montgomery County Maryland
Team members: Jules Gikundiro, Isabelle Scrimsher, Matthew Pedroza, Tia Chesley, Brian Fitzpatrick

For our project we analyzed vehicle accident data from Montgomery County Maryland. The dataset we used 
is called “Crash Reporting – Drivers Data”, we downloaded the csv file for the data at 
(https://catalog.data.gov/dataset/crash-reporting-drivers-data).

The dataset is structured with each vehicle that was in an accident in a row, for a total of 168,157 
vehicles that were in accidents, and a unique identifier for each accident, for a total of 94601 
accidents. The date range for the data is from 2005 January 1 to 2023 November 1. The dataset includes 
the details of each accident with information such as the vehicle make, if the driver was at fault, 
the time of day the accident occurred, the speed limit, and if the driver was distracted. We had five 
questioned that we asked, with each member of the group answering a different question. Because of the 
format of the data, each group member cleaned the part of the data that they were using. The five 
questions we answered are:

      What make of car is most likely to get into a crash?
      What percent was the driver at fault?
      What time of day do the most crashes occur?
      Do more injuries occur when the speed limit is higher?
      Is there a time of day when drivers are more distracted?

Ananlysis of the results for each question:

Question: Do more injuries occur when the speed limit is higher?

	The files used to answer the question about speed and injuries are injuries_and_speed.ipynb 
	for the code, and the graphs are fig_speed_injury.png and fig_speed_injury_severity.png.
	The total number of vehicles in accidents that were included in the analysis to answer this 
	question was 163,502, the speed limit categories of 0, 70, and 75 were dropped for reasons explained 
	below. A total number of 29,939 injuries were included. Giving a percentage of 18.31 for vehicles that 
	were in an accident, and there was an injury in the vehicle. Because the data is by vehicle and not by 
	person, it is not known how many people were in a vehicle, making this a limitation of the data, but 
	also there is no reason to suspect that there would be different averages of people in a vehicle at 
	different speeds. The two most important columns from the dataset for answering this question are the 
	speed limit column, which gives the posted speed limit, and injury severity, which gives if there was 
	an injury or not as well as the injury severity. 
 
	The speed limit category had speed limits ranging from 0 to 75, in increments of 5, giving 16 
	different speed limits. The speed limit category was not labeled as mph, but given that these data are 
	from the US it can be assumed that speed limit is in mph. When an accident occurred in an area where 
	there was no posted speed limit, such as in a parking lot the speed was coded in the data as 0. 
	Accidents that occurred when the speed limit column was coded as 0 were not included in the analysis 
	because the question is asking about the relationship between speed limit and injuries. There were 
	only 6 accidents that occurred at a speed limit of 70, and only 1 accident that occurred at the speed 
	limit of 75. Therefore, both the 70 and 75 speed limit categories were dropped because there was not 
	enough data to assess the likelihood of an accident occurring at these speeds.
 
	The injury severity column included five categories, “no apparent injury”, “suspected minor 
	injury”, “possible injury”, “suspected serious injury”, and “fatal injury”. One of the limitations of 
	using these data to answer this question are the data mostly includes only what was suspected at the 
	time of the accident. Someone could have been coded as having no apparent injury when they did have an 
	injury, or someone could have been coded as having a possible injury when they did not have an injury. 
	This is a limitation because the question is asking about injuries not suspected injuries. However, it 
	can be assumed that many injuries from a car accident are obvious, therefore this category should be 
	largely representative of injuries that did occur. The data in the injury severity category were text, 
	therefore a column for each category in the injury column was created. Meaning five columns were 
	created, one for each of the five categories, and then the injury severity column was broken up into 
	five different dichotomous variables, coded at 1 if the event did occur, and 0 if it did not. For 
	example, for the possible injury category a 1 was included for a possible injury and a 0 for no 
	possible injury. A column was also created for if an injury occurred or not. This then allowed for the 
	groupby function to be used to count each type of injury by speed limit. From this dataframe the 
	percent of vehicles who were in an accident that had any type of injury was calculated, as well as the 
	percentages for each type of injury.
 
	The results do show that, in general, when the speed limit is higher there does tend to be a 
	greater likelihood on an injury. The graph titled “Speed Limit and % of Vehicles that had an Occupant 
	with an Injury” saved as fig_speed_injury.png shows this. This graph has speed limit (mph) on the x-
	axis and % of vehicles with an injury on the y-axis. Going from a speed limit of 5mph to 50mph, with 
	each 5mph increase the likelihood of injury increased. Going from a low of 4.87% vehicles having an 
	injury at 5mph, to a high of 26.37% of vehicles having an injury at 50mph. Therefore, these results 
	are supporting the conclusion that as speed limit increases the likelihood of an injury increases, 
	making a case for lower speed limits. At the speed limits of 55 mph, 60 mph, and 65 mph the likelihood 
	of injury is lower than at 50 mph, providing some evidence that the likelihood of injury might not 
	always increase with speed. However, only 71 accidents occurred at 60mph, and 57 accidents occurred at 
	65 mph, therefore these results could be from insufficient data. 3,870 accidents occurred at 55mph, 
	relatively close to the number that occurred at 50 mph (4,555). Thus, this is providing some, albeit 
	limited. that injury might not always increase with speed.
 
	This question of injury and speed was examined further by breaking down the severity of injury. 
	If all types of injuries, and particularly serious and fatal injuries are increasing with speed then 
	this is giving further evidence to support not only the conclusion that injuries in general increase 
	with speed, but all types of injuries increase with speed. The graph titled “Speed Limit and % of 
	Vehicles that had an Occupant with an Injury, by Injury Type” under fig_speed_injury_severity.png has 
	the breakdown of type of injury by speed limit. While there are relatively few occurrences for the 
	categories of “suspected serious injury” and “fatal injuries”, the likelihood of an injury occurring 
	in each of the four different injury categories does, in general, increase with speed. However, this 
	is the case going from 5 mph to 50 mph, and again there is a drop off at 55 mph.
 
	Overall, to answer the question, “Do more injuries occur when the speed limit is higher?” The 
	answer is yes, injuries are, for the most part, more likely to occur at higher speed limits.

Question: What make of car is most likely to get into a crash?

	After compiling all of the data with just the make of the cars in this set there was so much that the 
	percentages of each make were smaller than expected. 

	There were some notes that had the make name shortened (i.e. CHEV instead of CHEVY or HND instead of 
 	HONDA), so I made sure to match all of the names where I was able to catch it. After the top 10 of makes 
  	the percentages were so small that it was best to compile everything else under an “other” category 
   	which was piled together and labeled accordingly. 

	In the end, the answer came out to be that “Toyota” was the most likely make to get into a crash at 
 	18.6%. Given that Toyota is an incredibly common car found in the US this data is not surprising. The 
  	others following it are all makes also very common. 



