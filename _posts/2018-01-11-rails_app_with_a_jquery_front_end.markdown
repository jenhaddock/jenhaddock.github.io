---
layout: post
title:      "Rails App with a jQuery Front End"
date:       2018-01-12 04:13:35 +0000
permalink:  rails_app_with_a_jquery_front_end
---


Before starting this project, I spent a good amount of time thinking about which of my models would a) allow me to meet the project requirements and b) made the most sense to the end user.<br>
I began by refactoring my user show page. Instead of automatically rendering a user's deductions and dependents, I added links for a user to click to see that information.  Once clicked, the models are rendered via jQuery without requiring a page refresh. <br>
![](https://i.imgur.com/bOY5J34.png)<br>
Prototypes were used to format the line items for each section to fit the formatting I was previously using.  The hardest part of this project for me was the deduction section on this page.  My project has a deduction code model and a deduction detail model.  The deduction detail model includes the user id and the deduction code id.  That's the model I need to access in the deduction show section.  However, the information I need to display is from the deduction code model. I realized I cannot call a jQuery request inside another jQuery request (or at least not the way I was trying to do this).  I got around this by creating a function that runs upon page load that creates an object of all deduction codes.  The jQuery request accessing deduction details can then reference this object to get details about the deduction code associated with the deduction detail record. <br>
I also added a Next User button for users that are set as admins.  This functionality also uses jQuery to load the page without a page refresh. <br>
Under the Edit Dependent link, I removed the Add Dependent button and intead allow the user to enter a new dependent directly on the screen.  Clicking the Create Dependent button immediately creates the record and renders that dependent to the screen without a page refresh. <br>
![](https://i.imgur.com/aoat35H.png)<br>
The videos included included in this lesson were very helpful as I worked on this project.  I recommend reviewing them before starting your project. 
