---
layout: post
title:      "Farmers Markets Galore CLI  Gem"
date:       2018-08-09 13:01:48 +0000
permalink:  farmers_markets_galore_cli_gem
---


Finally! I feel like it took forever to get to this point but after countless hours of learning Ruby, I am able to create my first application. The funny part of getting to this point is that you completely forget that this is probably going to be the hardest thing you've had to since starting the program... at least if you're a newbie like me. I'm coming with no prior coding experience so this is my first stand alone application that I have created all on my own. 

Well let me tell you that it has been a lot of fun but also a total pain in the ass haha. The video walkthroughs were a huge help to finding an architecture that could be useful for my application and really got the ball rolling for me. Then I hit a dreaded wall... 

Let me back track alittle before I continue. I recently moved to Denver, CO and my wife and I really enjoy farmers markets, so after some brain storming this seemed like a useful idea for an application because we don't know all of them yet. The idea was for an application to print out the top 11 farmers markets in the Denver area. Then you could select a market and it would give you the name, when it took place, and a description of the market. Okay back to the wall...

I hit this stupid wall. My application is printing out the first market from my website and it gives me all the information when I select it, it lets me re-visit the list, and it lets me exit. This is great and all but my application is missing ten markets which are vital to application. I realize I need to iterate of the data being scraped by Nokogiri but every attempt of this results in a broken application. I try binding.pry everywhere imagineable until I find the spot that lets me know my class variable containing the required instances is completely empty. AWESOME. This is great cause I found the problem but no matter what I tried I couldn't seem to change this return value. 

I spent two days somewhat depressed cause I had felt so close to finishing my project ahead of schedule but was defeated. I decided to do some reseach and then realized there was a refactoring video provided by flatiron and had Avi going over anti-patterns. This was my breakthrough. Watching him go through this persons application made me realize I had made a lot of these mistakes. I was forcing one specific class to do too much. I decided it was only right for me to move my scraping methods into their own class and let the class I had overloaded be focused with storing data for the individual markets. I had to make some small changes to my CLI class and finally my program was doing what I wanted. THANK GOD! 

Unfortunately I wan't completely out of the woods yet. I still had issues with CLI, specifically issues with my #market_menu method which used if conditionals to allow the user to interact with the application. At first this bug felt like a minor issue but the more I tried to figure out the issue the more I realized I had no idea how to fix it. After a lot of debuggin using pry I realized what the issue was and finally pinpointed where it was taking place. I simply needed a conditional that could check the value of a string so that the terminal could print out what I wanted. 

All in all this had been a really fun project to work on and finally seeing my program work is an amazing feeling. It may be a simple application at the beginning of a hopefully long career but if this is how it feels to create something, then I could definitely get used to this!
