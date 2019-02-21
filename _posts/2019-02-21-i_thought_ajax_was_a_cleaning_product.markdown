---
layout: post
title:      "I Thought AJAX was a Cleaning Product?!"
date:       2019-02-21 16:20:35 -0500
permalink:  i_thought_ajax_was_a_cleaning_product
---


Ajax IS a cleaning product and was introduced in 1947 (thanks Wikipedia). It's a white powdery cleaner you see being used on bathtubs and whatnot, but that's not what we're here to talk about! Ajax is a web development technique that uses multiple technologies to  perform asynchronous Javascript functions. 

Now this may sound pretty fancy, it kind of is, but basically Ajax is a process that allows the client side to send requests in the background, or asynchronously, and retrieve data from the database and display information to users without ever refreshing the browser. This is a great benefit to users because now they are able to view data on a single webpage or view individual records without the browser locking up, which allows for a more enjoyable experience. This also adds overall efficiency to any application because this request sent in the background skips the processing that normally takes place on the backend. Ajax uses a technology called JQuery to send an HTTP request to an API endpoint provided by the backend, which then responds with a JSON object. What makes this faster is that JQuery returns raw JSON data which is then manipulated with Javascript code that is already loaded on the webpage. This is why the browser doesn't need to refresh and overall increases the speed of the application. 

This topic is pretty important right now in my coding journey because it is the subject of my fourth Flatiron project. After spending about a month learning Javascript and how to utilize Ajax, I was sent on my own to rework my previous Rails project with a JS (JavaScript) frontend. There were three main goals for this project. 

The first was the ability to view at least one index page without the page refreshing. I tackled this one first because it felt like the easiest one and for the most part it actually was. In my app, a user has an index page full of their expense reports and at the top they have the ability to search their reports by year. I decided this search feature would request JSON data using JQuery and filter out the reports by year. After watching a couple videos to give me an idea of how to start, I discovered that this process of creating Ajax requests was actually quite fun. 

Second task was to render at least one show page. This presented more of a challenge and had me tinkering for a few days to get it just right. My goal was to show an expense report and have a next button that allowed them to see the next report. Seemed simple enough but the issue I ran into, led me to restructure my database. I know that sounds like a lot of work, but some minor relationships needed to change and columns needed to be removed. These changes allowed me to utlilize Active Model Serializers properly and let me create the JSON object to render data the way I wanted. 

Last goal was to render a has-many relationship and be able to submit a form dynamically with Ajax. A comments form was a pretty straightforward solution to this requirement and I already had comments associated to expenses. This still forced me to restructure some of my backend and take advantage of Rails partials to make the add comment form. This was also the only Ajax post request that I had to make and this took some googling to get the proper syntax. 

Overall this project was a lot of fun. It was a great way to see how JavaScript is used to enhance applications and give the user a richer experience. The big picture lesson I learned would be that architecting an app to use two languages can be a real challenge. I wrote the orignal application completely in Rails and didn't realize the structure could possibly pose a challenge when introducing another language to manipulate data provided by my backend. Using JQuery and Javascript has given my a new appreciation for the work that goes into making an application both front and backend. 
