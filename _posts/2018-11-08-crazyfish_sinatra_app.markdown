---
layout: post
title:      "CrazyFish Sinatra App"
date:       2018-11-08 21:32:12 +0000
permalink:  crazyfish_sinatra_app
---

When I read the requirement for this project I immediately knew what I was going to build. That might have been one of the best feelings I've had since starting this program! The CRUD application that I wanted to build was a fish management system. 

I am a fishtank enthusiast and realized the idea of creating a fishtank and adding fish to the correct tank would be the perfect CRUD idea. My application involved a user creating an account which would then allow them to create a fishtank based of the ones they currently owned and then add the fish into the corresponding tank. They could then update those tanks if they bought a new fish, moved the fish to a new tank, or even delete a fish if they had passed away or been sold. 

What really got me excited about the idea of this app was the potential for making it into a social media platform for hobbyists to follow friends and see their fishtanks and get updates on new fish they added. Maybe they would see a new fish they never knew about or be able to congratulate a friend on a new addition to their collection. This app would also be useful when visiting a fish store and a user wants to buy something new. They can go into the app and see what they currently own and where they could fit the new fish. 

The process of creating my Sinatra app was honestly a lot of fun. Before getting to this project I was having a tough time to really wrap my mind around the concepts but putting this together really solidified my ability to create REStful routes and customize my forms. I would say the toughest part of this project was designing my database and implementing validations for user inputs.

I decided to have three models that all had relationships and this made the process of creating my database tougher than the project required. I was not intimidated by this and after two days of planning out the relationships I eventually settled on the final migrations and it worked! These relationships got tricky when it came down to using attribute methods and figuring out how I could show the fish in a specific tank since fish belonged to fishtanks and not to a user. 

The other tough part was figuring out user validations and through googling I ended up at another fellow Learn.co students blog post specifically about validations. It was very useful and I learned that you could implement validations on both the client-side and server-side. You could do this by either placing them in the views, controllers, or models. I ended up placing validations on the client-side with an html5 tag of required at the end of my forms and I placed validations in the models which allowed me to use Rack Flash to display corresponding messages for user to see what went wrong. 

All-in-all this has been a really fun projec to work on. I actually have decided that this will be an application I will further develop for myself and maybe one day it will be popular amongs fishtank hobbyist! 
