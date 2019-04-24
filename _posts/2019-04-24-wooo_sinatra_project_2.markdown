---
layout: post
title:      "WOOO Sinatra! Project 2 "
date:       2019-04-24 21:16:32 +0000
permalink:  wooo_sinatra_project_2
---


I am an avid fan of Fantasy Football. My parents and some of my friends would argue I am too big of a fan sometimes. In my opinion, there is no such thing! For this project, I wanted to continue building on what I learned in the CLI project so I decided to build a site where users could create an account and create/read, update, edit, and destroy players on a table through Active Record. The project is rather simple, but is going to be the core of where I will be able to integrate my CLI application I built in the previous project. As in any standard sinatra project, the core items I build out are a database, models, controllers, and views. There were some ups and downs but for the main part this project was very fun to build out. 

DB Migration 
I created two tables that I migrated into a SQL database: users and players table. For now, the user has a username, email and password (password_digest), while the players table has a name, team, position, and a user_id I can then associate with its user. The creation and migration of the database was pretty straightforward. 

Models 
The project has two models: user and player model. You probably guessed it, but the associations for this are the user has many players and the players have one user. I thought about this for a while and felt that this was the cleanest way of building the site. In Fantasy Football, a user has a team which has a set number of players per position. Yes, the players technically belong to the user’s team, but isn’t that team actually just the user? I decided to skip the team aspect of this and just associate each player the user creates to his or her user_id. A user CAN have any player on his or her team, but can not have duplicate players. I originally had it so that once a user created a player, no one else could have that player on his or her team, but realized I would want this site to run more for an individual user rather than one league. In a league, that other format would make total sense, right? There is one league with multiple teams and each team has a set number of players. In this format, OF COURSE once a user adds a player to his or her team, that player should be unavailable to the other teams in the league. But that is not the purpose of this site. The purpose of this site was to create a center for users to be able to track players that were either on their team or even just players they wanted to keep tabs on. 

In order to achieve this goal, I looked up and implemented various validations for both the player and user model. I am very excited about the player’s validations. In order to prevent duplicative players from being added on to a certain user’s page, but NOT preventing them from adding a duplicative player in the SQL database I added a validation that looked at the uniqueness of the player’s name but under the scope of the user_id. I even learned that you can put in a custom message if there happens to be an error, which helped me keep my code DRY later on when building out my controllers. I also added a validation of the format of a player’s name to make sure users could not add random symbols and characters into the player’s name field and lastly added a validation just to check for the presence of all the fields required for a player to be created. In my users model, I added in three validations. The first validation just checks for the presence of all the required fields. The second checks to see if the email inputted by the user is an actual email (with an @ etc.) and lastly to make sure the email and username have not already been taken by a previous user. 

Overall, the buildout of the models was pretty seamless. I found learning about the various validations to be interesting and I am thrilled that I was able to use them in this project! 

III. Controllers 
I built out 3 controllers: applications, players, and users controller. The application controller inherits from Sinatra and basically sets the stage for the other two controllers. It holds my two helper methods that we are pretty familiar with here at Flatiron: logged_in and current_user. Next, I built a users controller which handles the signups, logins, and logouts that a user will want to do with our site. The players controller handles the creating, editing/updating, and deleting of every player a user would be doing in his or her personal site. 

My only struggle through this was both finding interesting ways to keep the code DRY. I used a couple helper methods that we learned in the course and also used the object.valid? That is available because we used validation in our models. I found this to be the most exciting part of building out the application since it was something new. Thank you Bonus! 

IV. Views 
I structured this app with two folders. The folders include a players and users folder. These two folders handle the creating, editing and showing of players/users. The two main pages are the index (root page) and of course a layout page. The index page is just the home page a user sees when they first go on the application. However, the most interesting visible part of the application is on the layout page. Every view page implemented in the app is actually rendered or yielded on the layout.erb file. The layout contains my navigation bar you can see below, but then yields whatever form is being rendered by the controller. This A) keeps the code DRY, but also more organized in my opinion. I also implemented some logic in the layout page so that based on whether or not a user was logged in, he or she would see different options in the navigation bar. As you can also see in the shot below, I added some css to style and structure my HTML. I found this to be pretty challenging and for the sake of time left some of the forms looking a little wonky so I could move on to making sure the functionality works. I will fix this part soon don’t worry! 

V. Overall 
Overall, I found this project to be a lot of fun. As you can see, I am passionate about both coding and fantasy football. Any project that combines both of these interests is a win for me. As mentioned above, the most challenging aspect of this project was just thinking through how I wanted a user to actually interact with the app and just getting various views to look/ function the way I intended them to while keeping the code DRY. 

Thank you for reading this! 

