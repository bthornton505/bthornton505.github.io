---
layout: post
title:      "Please Don't REACT That Way..."
date:       2019-04-10 22:09:16 +0000
permalink:  please_dont_react_that_way
---


Where to start...

To be quite honest, React and Redux has seriously been kicking my butt. I consider myself a pretty resilient person, but these two technologies have seriously made me question why I decided to become a programmer in the first place. Maybe that's a bit extreme but I just needed to put that out there. 

Now don't get me wrong, it has also been a lot of fun to learn React and I really am excited to further develop my final project, but I'm still struggling with what seems like basic concepts. The process of learning to pass props to components and setting state feels like a wild goose chase at times. 

Then there's Redux...

Redux can seriously be a pain. It's a very high-level concept that when explained, makes a ton of sense, but when implemented into your React app really can get out of hand. It felt like there were 100 different pieces to connect and if one thing was connected wrong everything would break. Trying to build a CRUD app using Redux has been a huge challenge that I truly underestimated. 

One instance in the process of implementing Redux that drove me quite mad was the create and delete actions of a recipe. My rails api was setup perfectly and when the form was submitted, my server would fire and process everything correctly. However, when redirected to the list of recipes, it wouldn't update unless I refreshed the entire page (command+r is my new bestfriend). This bug sent me on a wild chase to find out why and I thought it had something to do with lifecycle methods (100% the wrong solution). After a couple days of research and with no questions answered, I reached out to my twitter followers for any kind of help. I was fortunate enough to get a Flatiron Alum to help and she discovered my reducer for create was all wrong. Finally got that working!

Even after that help, I still ran into the same issue with deleting recipes and it took me two days to realize I had forgotten one word in my reducer to filter through the recipes that didn't match the recipe being deleted. ONE WORD. 

I realize I've been ranting this entire time about how this final project has been giving me a run for my money, and I realize that life as a professional developer will only become more frustrating as I work on more complex systems. I really just needed to vent to the internet. This has been a huge challenge for me and currently my project isn't even finished but I will not be defeated by the code. 

It will REACT the way I want it to...
