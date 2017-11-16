---
layout: post
title:      "Open Enrollment Rails App"
date:       2017-11-16 00:45:51 -0500
permalink:  open_enrollment_rails_app
---


I approached this project wanting to focus on user experience and creating a project with a good flow. Because of this, I wanted a topic I was experienced with.  Being the end of the year, the idea of creating an app to handle open enrollment for employment deductions came to mind.  

I began by laying out my models: Users, Deductions, Dependents and Deduction Details (this is my join table).  

My next step seemed easy enough: create a sign up/sign in page to create the user objects.  I created a simple homepage with links to my sign up options.

![](https://i.imgur.com/zp1UTA3.png)

Like most apps, all we need to sign up is an email and a password.

![](https://i.imgur.com/ALjipei.png)

This is where things got interesting for me.  When I planned out my deduction types, I created two types: flat and percentage.  A flat deduction is the same for every user (health insurance for example).  A percentage deduction is something a user can customize (like 401K deductions).  To accomplish this, we need to know a user's salary.  But wait, we're creating the user on sign up.  Do we want to ask them their salary on the sign up page?  That didn't seem user friendly to me. What if a user tries to sign up with an existing user email address?  Our validation will instruct them to sign in but if the salary they entered differs from what was originally entered on sign up, which do we use?  I had to find a solution. 

I briefly toyed with the idea of creating an Employee model.  A user would have to link to an employee record.  Because this would be a one to one relationship, this didn't seem like a good option to me either.  I finally settled on creating a boolean value on the user record called setup_complete.  When a user is created, the email and password will be filled in and the setup_complete flag will be set to false.  Users will be required to complete a setup page which will set this flag to true.  Until the setup_complete flag is set to true, users will be restricted to the user setup page.

To get fully setup, users will need to enter dependents and select deductions.  When I thought of going through this process myself, I asked, would I want to enter my dependents on one page and then go to another page to select my deductions?  Of course not - I'm too lazy for that. Therefore, I created one setup page that encompasses the missing user fields we need, the dependent fields and the deduction selection options. 

![](https://i.imgur.com/PLm78yV.png)

You'll notice the links on the header only include an option to sign out while setup is not complete. You'll also notice that users have an option to be set as an admin.

Once I complete the setup process, I'm taken to a user show page.

![](https://i.imgur.com/MU8IvLA.png)

You'll now notice I have options to edit my deductions and edit my dependents in my header links. 

Editing my deductions created an interesting issue.

![](https://i.imgur.com/OucIDum.png)

Unselecting a deduction does not remove it from the user.  To get around this, in my update method, I first remove all deductions from a user.  I then completely re-add them from the options selected on this form. 

Editing dependents is pretty straight forward.

![](https://i.imgur.com/oarCmdb.png)

I can add new dependents or remove any dependents that have grown up and gotten their own jobs. 

I setup myself up as a non-admin user.  When I log in as an admin, you'll notice I have a few more options in my header links.

![](https://i.imgur.com/RhiyXBw.png)

Admins are able to see a user index of all users and their deduction totals and add or edit deduction codes.

![](https://i.imgur.com/R4Zh5G0.png)

From the index page, admins can see each user's show page.

![](https://i.imgur.com/SfbLJSc.png)

Editing deductions is also a pretty straight forward process.

![](https://i.imgur.com/1OOEXPL.png)

![](https://i.imgur.com/9dZhZrG.png)

![](https://i.imgur.com/BdPkoWB.png)

I did add validation to each admin only method to ensure the user is an admin before rendering the view.  This ensures non-admin users cannot manually type in a path they do not have access to.  If they try this, they will be redirected to their show page. 

While I did run into some issues I had not encountered in our labs, in the end my app accomplished what I wanted it to.  As an end user, I am happy with the flow and feel like it is an easy app to navigate. 

