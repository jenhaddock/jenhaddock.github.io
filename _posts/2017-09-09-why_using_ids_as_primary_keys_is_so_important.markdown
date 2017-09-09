---
layout: post
title:  "Why using IDs as Primary Keys is so important"
date:   2017-09-09 21:13:36 +0000
---


As developers we understand why it's important to have primary keys on our tables.  We must have a way to distinguish each record so we can access it when needed.  For our examples at Flatiron, active record creates the id field as our primary key for us.  As we graduate Flatiron, there will be some of us who will be designing tables outside of active record.  This will require us to define tables and their fields on our own.<br>

Let's say we're writing an application for a city's business license tracking software.  Each business license has a number that is 6 digits long and each business license must be unique.  We know we're going to have files for master license information, fees for each license, transactions for each license and notes for each license.  Each file will join to the master license information file.  We know at some point a customer is going to call in and say there is an issue with fees for a license and we're going to need to access the fees table for that particular license. So we open up the fees table to look for license 000001 and ugh, it's not there!  We first have to go to the master license table, find license 000001, find what the license_id is for that license AND then look up the fees in the fees table.  It's annoying.  Our initial reaction may be to use the license number itself for the unique field for the license instead of a random id number.  All of our join tables can reference the license number and everything will still be tied together. Sounds great, right?  Maybe not...<br>

One of our sites decides they don't want their project numbers to be 6 regular numbers.  Instead of 000001 they want them to be 170001 so they know that license was done in 2017.  Ok, we can change that.  But wait - all of our join tables reference that number.  It's ok, there's only three tables.  So we write a program to update all of those tables and join fields and everything is great  <br>

Fast forward and we're growing our customer base.  To accomate some of our new customers, we've added files for renewal information that link to our master license file.  Now another customer wants to change their license numbers.  That's fine, we already have a program to do that for them.  So they run that program and...where did their renewal information go?  That's right, we forgot to add that new file to our program and it now references license numbers that no longer exist. <br>

This is why having ids that do not tie to what your user sees is so important.  Had we used generated ids instead of using the license number, we could change our license number in our license master file, and all of our joins would be unaffected by the change. <br>

While generated ids may at times take us longer to access information, they preserve the link between our tables when we decide key information needs to be changed. 
