---
layout: post
title:      "Learning CSS... the highs and the lows "
date:       2019-04-24 20:49:34 +0000
permalink:  learning_css_the_highs_and_the_lows
---

Hi all, 

I have always been passionate about learning CSS. I have a background in design and just love putting together various projects in order to display my messaging in an aethetically pleasing way. I get my inspirations from a lot of different places, but ever since I started the FI program, I have been drawn towrads https://www.awwwards.com/. If you are not familiar with this site, it displays various sites around the world that demonstrate design, creativity and innovation on the internet. I usually tend to agree with the users who vote on these sites, as most of them are elegant and clean. I have tried to implement this is my projects, but have found out rather quickly that it is one thing to add some CSS to your project so it doesn't look vanilla, it is another to get sites to look like some of the sites I love on awwwwards.com. 

What I have learned so far in my initial studies of CSS is that it's very difficult to make beautiful sites just by going at it on your CSS pages. I have found using Flexbox and CSS Grid help organize your code and make it easier to control various divs/containers you are using in your code to control various objects on your page. 

Below, I am going to show a very simple example of CSS GRID to prove my point: 


```
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="../assets/style.css">
  <title>CSS Grid Implicit vs Explicit Grid Tracks!</title>
</head>

<body>
  <div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
    <div class="item">4</div>
    <div class="item">5</div>
    <div class="item">6</div>
  </div>

  <style>
    .container {
      display: grid;
      grid-gap: 10px; 
      grid-template-columns: 200px 400px; 
      grid-template-rows: 50px 100px; 
      grid-auto-rows: 500px; 
      grid-auto-columns: 100px; 
    }
  </style>
</body>

</html>
```

In the code above, there are six divs used to print out 1, 2, 3, 4, 5, 6 on separate lines. I added in the style on the same page just for the purpose of this demonstration, but here we are taking the main container div and displaying it as a grid. We are then adding a space (grid-gap) of 10px between each element/div. Next, we are adding in two columns. The first column is going to be 200px, and the other is 400px. For rows, we are adding in 50px for the first row and 100px for the second row. Anything after that overflows will have a row height of 500px and a column width of 100px. What this does is allow us to organize how we can shove these divs in each column. Right now, without specifiying specifically where they go, they will try to fit within each column and row available at first, and anything that doesn't fit will autoflow in the rows/columns. 

Anddddd that is the very basics of CSS grid. I find this is really helpful for organizing divs etc. and will definitely write another post on this topic. 

Till next time, 
Chris 
