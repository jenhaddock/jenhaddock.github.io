---
layout: post
title:  "Sinatra Project: Fantasy Football Roster "
date:   2017-09-09 20:29:45 +0000
---


For my Sinatra project I created a (very) simplified fantasy football roster app.  This app has three models: users, teams and players.  Teams belong to users and users can have many teams.  Players belong to teams and teams have many players.  Users will have many players through teams.  

Users are required to create user accounts with a name, email and password.  <br>
![](http://imgur.com/hWxr453.png)<br>
![](http://imgur.com/6UWlFqC.png)<br>


We will not create a user account that has the same name as an existing user.  In order to implement validation that all user signup fields are populated and that a user is not creating a user with a duplicate name, I used rack flash to display error messages when this validation is not met.<br>
![](http://i.imgur.com/4fTMbbU.png)<br>
![](http://i.imgur.com/kU09gLW.png)<br>

Once a user is properly logged in, they will be able to see a list of the teams they have already created.<br>
![](http://i.imgur.com/nwzdI55.png)<br>

On this page they will also be able to create a new team.  For my project I created a seed file with player names so we would have a list of players to chose from. In a real life example, we would need to scrape the NFL's player page to get a complete list.  For simplicity sake, I kept our list to one page and greatly limited the players we could select.<br>
![](http://i.imgur.com/QeKlYy9.png)<br>

One we've made our selections and create our team, we will see a show page for our new team.<br>
![](http://i.imgur.com/wUnwSEG.png)<br>

You can see in our address bar that we're using slug logic to pull up the team page. I'm using the same logic to search for user names in my user controller. <br>

If we chose to edit our team, you'll see I'm using two loops to load the players.  First, I load the players already assigned to the team.  Then I load all other available players.  I made this decision for aesthetic reasons.  In a real life example, we would be scrolling through hundreds of players.  Having to scroll through all players and trying to catch just the ones that were selected would not be very user friendly for this particular app. This design lets the user get a view of their team before making changes. <br>
![](http://i.imgur.com/wwbp5sI.png)<br>

Let's take note of the players selected for Second Team: Cam Newton, Eddie Lacy, Travis Kelce. If we try to create another new team you will notice those players are not available for selection.<br>
![](http://i.imgur.com/gRF2Uha.png)<br>

The design of fantasy football limits players to belong to only one team.  In order to prevent one user from stealing another's user player, this app will not even display players that already belong to another team (even if that team is your team).  To accomplish this, I used an if statement inside my loop to load players:
```
  Available Players: <br>
    <%Player.all.each do |player|%>
      <%if player.team_id == nil%>
        <input type="checkbox" name="team[player_ids][]" id="<%=player.id%>" value="<%=player.id%>"><%=player.name%> - <%=player.position%> - <%=player.pro_team%><br>
      <%end%>
    <%end%>
```

Users are only allowed to edit their teams and users must be logged in before adding or editing any teams.  Users will be allowed to view other user's teams through an index page.  This page displays all teams along with the user they are associated with.<br>
![](http://i.imgur.com/JxVmu68.png)<br>

For my model design, I created three controllers.  The application controller handles the index and homepage. The user controller handles all login, signup and logout actions.  The team controller handles creating and editing teams. <br>

While this project was a very simplied version of fantasy football, it makes me appreciate the complex nature of the sites and apps I use online.  I can see how much validation and thought goes into even the simpliest apps. This project definitely makes me think through what goes into developing the apps I use on a daily basis. 

