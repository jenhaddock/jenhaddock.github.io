---
layout: post
title:  "CLI Project: The Tour de France"
date:   2017-08-09 02:15:44 +0000
---


When I was looking for ideas for this project I asked myself "what interests do I have that make me different than the typical programmer?" And since I spent way too much of the month of July watching the Tour de France, I thought it was good to get something educational out of all that time.  Thus, my 2017 Tour de France CLI App was born.

The first order of business was finding something to build a class on.  The Tour de France has 21 stages with multiple attributes per stage which makes them perfect to be handled as a class.  The website I decided to scrape was http://www.letour.com/le-tour/2017/us/overall-route.html which has a great table listing each stage, the date of the stage, the type of stage, start town, finish town, distance and a link providing more details. 

When I started my actual programming, I started with the CLI.  I asked myself, what would a user want to see when looking at a Tour de France app? When considering my users, I decided to add options to view specific types of stages for those users familiar with how grand tours work and another option to view all stages for those users who may not be used to the stage formats of grand tours. 

```
      Welcome to the 2017 Tour de France
-----------------------------------------------
Which type of stages would you like to see?
1. All Stages
2. Time Trial Stages
3. Flat Stages
4. Hilly Stages
5. Mountain Stages
6. Exit
```

When an option is selected, a list will be displayed with each matching stage and the date of the stage:
```
Which hilly stage would you like more info on? (Type exit to leave or menu to return)
3. Monday, July 3rd
5. Wednesday, July 5th
8. Saturday, July 8th
14. Saturday, July 15th
15. Sunday, July 16th
```

When an individual stage is selcted, all of the stage's attributes will be displayed:
```
Stage: 8
Type: Hilly
Date: Saturday, July 8th
Start Town: Dole
Finish Town: Station des rousses
Distance: 187.5 km
Details: http://www.letour.com/le-tour/2017/us/stage-8.html
Would you like to see more stages? (Y/N)
```

The user can then decide whether to go back to the menu to see more information or to exit. 

Upon exit I let the user know exactly where I'll be next July:
```
See you at the 2018 Tour de France!
```

Some of the safeguards I put in place were:
On the main menu I verify the user selects an option of 1-6 or the menu will reprint,
I make sure the user selects a valid stage of 1-21 or they will get a message saying we only have 21 stages, and
I make sure the user enters a numeric value on the menu screen or the menu will reprint.

The process of scraping a foreign website, where part of the attribute names were in French, presented some interesting challenges when trying to intuitively figure out element names.  But overall, the scraping process was able to be done using the element inspector. 

I greatly enjoyed combining two things I love: programming and cycling.  I loved being able to design the program myself with no barriers to what I could create. 


