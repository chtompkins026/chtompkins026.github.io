---
layout: post
title:      "The Highs & Lows of the Rails <> JavaScript Project  "
date:       2019-04-24 21:20:41 +0000
permalink:  the_highs_and_lows_of_the_rails_javascript_project
---


Just to repeat… I am an avid fan of all fantasy sports. I have literally done all my projects on some aspect of a fantasy sports site, and decided to continue building out certain features of a fantasy sports site using rails and javascript. For this project, I wanted to continue building on certain points of my rails project in unit 3. The concept is rather simple, but I am continuing to add functionality to concepts started back in the CLI project. Similar to the rails project, the core items I build out are a database, models, controllers, and views. Where this project differs, is that I use javascript and jQuery to render comments, teams, and players in various parts of the app. There were some ups and downs but for the main part this project was very fun to build out. 

Just to note, you can find my Rails <> JavaScript project in the link below. This might be helpful so you can actually follow allong with what I am actually talking about! 

# https://github.com/chtompkins026/active-serializer-project



I. DB Migration 
I created five tables that I migrated into a SQL database: comments, players, teams, players_teams (join table), and users. The comments table contains the title, description, and user_id. The players table contains the following fields: name, position, nba_team, points, and team_id (for the user’s team). The next table is a join table: player_teams. In my last project, I had it so that players belonged to a league, but could be a part of many leagues. In this project, since the point was to focus more on our javascript skills, I decided to change the relationships so that a player could belong to many teams and a team could have many players. I accomplish this using my player_teams table. The point here is that a user can use this app to keep track of his or her various fantasy sports teams. In this case, a user most certainly could have the same players on his or her team. The next table to highlight is the teams table. The table includes name, total_points, user_id, and league_id. Note, I actually have yet to incorporate this functionality, but the goal with adding total_points was to be able calculate how many points a team is projected to accumulate based on who the user added to his or her team. The last table is the users table, that has name, password_digest, email, and various fields for Omniauth. 

II. Models & Serializers
The project has five models and five serializers. The models are pretty straight forward. Starting with user, I have the user having a secure password, many comments, teams along with several validations. I also added in a couple omniauth methods, giving the user the flexibility of either logging in via the standard username and password, or using Github credentials to log in to the app. Next, I have a team model. The team has many players through player teams (the join table) and belongs to a user. If you look over in the player model, you will see a similar relationship, which allows for us to use the player_team join table. In the player model, I do have a sort_by_player scope that allows the app to sort players by their projected points. Lastly, I have a comments model, which belongs to a user. I also included a sort_by_comment scope method so I could organize the comments by id. Overall, the buildout of the models was pretty seamless. I found learning about the various validations and scopes to be interesting and I am thrilled that I was able to use them in this project!  Since we did this in the rails project, I didn’t find this to be as cumbersome. 

Next, you will see that I also created five serializers. The serializers are pretty straightforward, as they correspond to the models mentioned above. The only serializer that is somewhat different is the comment_author serializer, which allows me to render the author of the comments via JSON. I found this aspect of the project rather fascinating and will continue to develop my skills in this area. 
	
III. Controllers 
I built out 7 controllers: applications, players, users, comments, omniauth, sessions, and teams. The application controller sets the stage for the other controllers. It holds four methods but also links out to two helper pages: sessions and users. I use them throughout the project. The four methods on the application controller are similar to the ones used in both my rails and sinatra project: user_exists?, current_user, user_check, and require_login. The most interesting controller build out was the omniauth controller. For me, this was the most difficult part of the assignment. I spent some time researching how to incorporate Omniauth into my project and best practices. I decided to create a single controller that handles a user logging in via Omniauth. There are only three methods in the controller: a create method, omni? and a private from_omniauth method. The omni method simply checks to see if the user is coming in from an omniauth login. The second private method takes the information and finds the user if he/she exists OR if the user is new, creates a new account for the user view a .first_or_initialize.tap method. I found this method to be very interesting and I am so happy I was able to use it in this project. Lastly, the public method, create, setst the session user_id to the current user and logs the user in to the app. Another aspect of the project that of course was new, was rendering JSON! For example, in the Teams controller, I render JSON in index, show, next_team and create. This obviously was the goal of the entire assignment, and I enjoyed learning and implementing this into my project. I don’t think this was too difficult. Where I ran into some trouble was implementing javascript and jquery in the views and js files. 


IV. Views 
I structured this app with six folders. The view folders include a layouts, comments, players, sessions, teams, and users. The most complicated view page to build out was the teams show and index page (Team Show page - screen shot below). Here, using jQuery and Javascript, I am taking a player who has already been created in the database, and associating him with the team. This is happening without the page being rendered all thanks to the power of javascript and jQuery. What was tricky here was learning how to immediately append this player to the end of the table, without breaking any of the HTML. I had to read a few stack overflow explanations and went through some trials and error, but finally got this to work! I am definitely most proud of this page. 

Another area of the project that is definitely new is the comments section. Similar to the functionality mentioned in the show page, I implemented the ability to create a comment, preview it, while also in the backend appending that new comment to the main comment board (screen shot below). I also had a little fun with the css styling here. 

Lastly, another complicated page that uses javascript and jQuery is on the Team Index Page. Here, a user can use every team created in the top half of the page. On the bottom half of the page, a user can scroll through each team’s roster without having to refresh the page. This shows a has_many relationship between the team and players. This definitely took a little time to master, but I am glad that it works. 


V. Overall 
Overall, I found this project to be a lot of fun. As you can see, I am passionate about both coding and fantasy sports. Any project that combines both of these interests is a win for me. What was challenging here was getting the javascript and jquery to actually work. I find javascript more difficult than Ruby, in that it’s very fickle when it comes to syntax. One missing semicolon or missing curly brace will break the entire code, and it takes longer to debug in my opinion. That being said, I know this project just scrapes the surface of the power of javascript and I look forward to learning more as I continue in the course. 

Thank you for reading this! 

