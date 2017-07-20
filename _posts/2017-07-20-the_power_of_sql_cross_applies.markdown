---
layout: post
title:  "The power of SQL Cross Applies "
date:   2017-07-20 04:06:41 +0000
---


For me, one of the more complicated aspects of SQL was grasping the power of what the cross apply command can accomplish.  In short, cross applies are used when you want to join multiple results from one table to one result in another table.  
Say you have a table of phone numbers.  You may have one table formatted as:
```
id	customer_id	 cell_phone		home_phone		work_phone		alt_phone   	spouse_phone
1		1            111-1111		  111-1112		  111-1113		  111-1114		111-1115
2		2            222-2222		  222-2223		  222-2224		  222-2225		222-2226	
3		3            333-3333		  333-3334		  333-3335		  333-3336		333-3337
4		4            444-4444		  444-4445		  444-4446		  NULL	        444-4447
```

But say you want to insert these values into a table formatted as:
```
id   customer_id    phone_type   phone_number
```

Each row in our first table will result in multiple rows in the second.  We can not only insert the phone numbers into the new table, but we can also associate a correct phone_type for each with one statement when we use a cross apply.

```
INSERT INTO table2 (
   customer_id,
   phone_type,
   phone_number
) VALUES (
  table1.customer_id,
  results.new_phone_type,
  results.new_phone_number
)
  FROM table1 
  CROSS APPLY (VALUES ('CELL', cell_phone),
                      ('HOME', home_phone),
                      ('WORK', work_phone),
                      ('ALT', alt_phone),
                      ('SPOUSE', spouse_phone)
                      ) [results] (new_phone_type, new_phone_number)
    WHERE new_phone_number IS NOT NULL 
```

Let's break this down.  In our cross apply we're defining two fields in our values section.  For our example, those values are the phone type that exists in the second table but not the first, and the value from our first table that we want associated with each of those phone types.  So we're able to take the partial information we have from the first table and fill in the information we're missing to complete the second table. We create a value entry for each of the new types we're defining.  We then alias the cross apply table as [results] and then define what those fields should be called.  This allows us to reference those values in our insert statement like we would any other table.

A key to cross applies is that we want to keep our cross apply as simple as possible. We know the customer_id field is static across both tables.  Because of that, we can keep it out of the cross apply.  If you find yourself repeating a value over and over, it does not need to be in your cross apply. 

This is a very simplistic example, but you can see how powerful cross applies can be when applied to large databases.
