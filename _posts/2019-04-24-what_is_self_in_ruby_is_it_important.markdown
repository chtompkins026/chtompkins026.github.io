---
layout: post
title:      "What is `self` in Ruby? Is it important?"
date:       2019-04-24 21:09:27 +0000
permalink:  what_is_self_in_ruby_is_it_important
---


Hi all, 

Let us talk about that crazy thing called self in Ruby. What is it and why is it significant? If you are familiar with JavaScript, it is the same thing as this. 

Since I have been programming in Ruby, I have become very familiar with self. It is unavoidable and rather interesting when you stop to think about the concept. When I first started out learning how to code, I felt as thought self was rather mind-boggling. When I added in a self, I would think it would produce one thing, but the next thing I know it would be something completely unrelated or, even worse, start producing errors in my Ruby methods! So, today I am going to write a very general blog post about what exactly is self and how I have personally used it in my projects. 

So Yeah… What the heck is self?
One thing you know from JavaScript and in Ruby is that everything is an object. Therefore, everything that we are creating (lines of codes) evidently will belong to an object, right??? So yeah, the keyword self refers to the object that owns the lines of code that you are currently writing. I looked at some other examples of people describing it and the one I like the best, in the following blog (https://www.jimmycuadra.com/posts/self-in-ruby/) 

The keyword self in Ruby gives you access to the current object – the object that is receiving the current message. To explain: a method call in Ruby is actually the sending of a message to a receiver. When you write obj.meth, you're sending the meth message to the object obj. obj will respond to meth if there is a method body defined for it. And inside that method body, self refers to obj. When I started with Ruby, I learned this pretty quickly, but it wasn't totally apparent when you might actually need to use self. I will outline the two most common use cases I've found for it.

Basically, self is a unique variable in Ruby that allows us to point to the object that owns the code you are currently executing. NEAT huh?! You might see this used in instance variables, methods, classes and modules. It is everywhere in Ruby and pretty essential. 

My Examples of Using the self Keyword
Boom, here are my examples of using self in various code I came across. Most of these examples are from my CLI project. Side note… spent a ton of time on the CLI project since I am pretty passionate about Fantasy Football. If you ever want to talk FF, let me know! 
Using Self Inside an Instance Method 
In the code below, build is an instance method. It belongs to the object we created via Team.new. The self here points to that specific object.

```
class Team
  def build 
    self
  end
end
```


Inside of a class method
For this example, reflect is a class method of Ghost. With class methods, the class itself "owns" the method. self points to the class.

```
class Scraper

    def self.create_players(link)
      doc = Nokogiri::HTML(open(link))
      players = doc.css('.player-row')

        players.each do |play|
          unless play.nil?
            name = play.css("input").attribute("data-name").text.nil? ? "N/A" : play.css("input").attribute("data-name").text
            position = play.css("input").attribute("data-position").text.nil? ? "N/A" : play.css("input").attribute("data-position").text
            team = play.css("input").attribute("data-team").text.nil? ? "N/A" : play.css("input").attribute("data-team").text
            opp = play.css("input").attribute("data-opp").text.nil? ? "N/A" : play.css("input").attribute("data-opp").text
            nlink = "https://www.fantasypros.com/nfl/players/" + play.css("a").attribute("href")
            Player.new(name, position, team, opp, nlink)
            end
          end
     end
```

Basically, the self here is referring to that scraper, and whenever I want to call it, I have to use Scaper first. Here is an example! 

```
module FantasyFootball
  class CLI
    LOOKUP_POSITIONS = ["flex","k","qb"]   #this is a constant
    POSITIONS = ["rb","qb","wr","te","flex","k"]
    #our menu is flexible because it is tied to the  array. If we wanted to add something in, then we just add it in
    #Everything with the CLI deals with input and output. Jumps to other classes for everything else

    attr_reader :selected, :ranker

    def send_link
      LOOKUP_POSITIONS.each_with_index do |pos, index|
        link = "https://www.fantasypros.com/nfl/rankings/#{LOOKUP_POSITIONS[index]}.php"
        Scraper.create_players(link)
      end
    end
```

There are other ways/reasons you would use self, but these are the two major ways I have used it so far in my time here at Flatiron. Hopefully this helps you a little bit. It definitely helped me! 

Till next time,
Chris 

