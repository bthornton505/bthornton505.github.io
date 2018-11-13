---
layout: post
title:      "To Render or to Redirect, that is the Question..."
date:       2018-11-13 21:43:48 +0000
permalink:  to_render_or_to_redirect_that_is_the_question
---

In this blog post I will be covering different topics in regards to rendering and redirection within a Sinatra app. These are two very important concepts to understand when buidling web applications and a solid understanding of the difference can save any developer from quite the headache. 

### What is rendering? 

Before we talk about rendering we need one very important thing to happen, which is basically a user needs to type in a specific website and hit enter. This starts a chain reaction which involves sending a HTTP Get request to a server. This is where rending takes place because once the server gets this specific request it needs to find the controller action in the app and render a view that is associated with the Get request. Once the server finds the matching view to render, it responds by rendering the HTML that is inside the view and giving the user the content they requested.

### How do you render a view in Sinatra?

Rendering a view in Sinatra is rather simple. When creating routes in your controllers you need to have views that will be associated with the action you want to accomplish. These views will contain HTML code and erb that will help build content that you want a user to see. When you want a user to sign up you will have a view associted with a Get request for /signup. 

```
get '/signup' do 
    erb :'users/signup'
  end 
```

A user will click a Sign Up button which will be associated with this route. To then render the signup.erb you declare the render with `erb :'users/signup'` and this will go to your views directory and then find the users directory which will contain a signup.erb file. 

```
<h1>Start managing your aquarium today!</h1>
<h2>Sign Up:</h2>


<form action="/signup" method="POST">
  <p><input type="text" name="username" placeholder="username" required></p>
  <p><input type="email" name="email" placeholder="email" required></p>
  <p><input type="password" name="password" placeholder="password" required></p>
 
  <button class="btn btn-primary" type="submit">Sign Up</button>
</form>
```

The HTML and erb code found inside that file will then be sent back to the client and rendered as a legit webpage. The cool thing is that you can have this route render any specific view that you want it to, which gives you the freedom to create a specific experience for the user. 


### What is redirection? 
	
Rendering is great and all but users want to be able to input some data and see their results on the otherside. This is where redirection comes into play. As developers we not only create the Get routes but we also create Post routes (or Put, Patch, or Delete) and these are necessary to persist data to our database. Redirection is concerned about telling the browser it needs to make a new request to a different location and so it allows the user to see these changes that they have made after submitting a form to the server or basically after any changes they have made. 


### How do you redirect in Sinatra?

Sinatra is a domain specific language and because of this it gives us a ton of methods. Redirect is one of those methods and it's what allows us to send users to a new view that can contain the content they just persisted to the database. 

Once a user is given the signup view which includes a form, they are able to enter their specific info and create an account. When the form is submitted to the server, the Post request then handles creating this user. It then has the ability to validate this info and redirect the user to either the updated view or the current view because it did not pass validations. 

```
post '/signup' do
    @user = User.create(:username => params[:username], :email => params[:email], :password => params[:password])
    
    if !@user.valid?
      flash_error(@user)
      redirect to '/signup'
    end
    
    session[:user_id] = @user.id 
    redirect to "/users/#{@user.slug}"
  end 
``` 

Once validations pass, the user is redirected to their profile with this line of code, `redirect to "/users/#{@user.slug}"`.
Now what is actually happening here when we write the redirect method is it will make sure our application responds with the status code 303 and adds a location header to the response which means it adds the new route to the end of the URL. This could look like http://localhost:4567/users/bthornton and this would be our new profile page that we are given after the Post request was sent to the server and returned to us with the redirect method. 

There is another redirect inside this controller action that takes place during the validation. If a users input in a submitted form fails the validation this line of code `redirect to '/signup'` will actually send the user back to the /signup URL which is a route already created inside the controller. The application will see this error which sends the user back to this page, and it renders a fresh view that contains the same form they tried to submit. 


### Are you able to access variables on a view if they are declared in the controller action that will render a view? 


The answer is Yes. Here's why: 

When creating an application you need a way to pass data into your views. This can be done a couple of different ways but a very common way is to use instance variable in the controller route that renders a view. It would look something like this: 

```
get '/users' do 
    @users = User.all 
    erb :'/users/all_users'
  end 
```

What this @users variable allows us to do is show all the users once the view has been rendered. Our template would look like this: 

```
<h1>Checkout other CrazyFish tanks!</h1>
<br>
<% @users.all.each do |u| %>
  <ul>
    <li>
      <h3><a href="/users/<%= u.slug %>"><%= u.username %></a></h3>
    </li>
  </ul>
<% end %>
```

Because we declared the instance variable in the route that renders the view, Sinatra makes this variable available to us in the view. Now we can use this varialbe to show the user specific data that we feel is important to them. If we had not declared the variable and still plugged it into the view, the app would not have recognized the instance variable and failed to render the view. 


### Are you able to access variables set in a controller action after redirecting to another controller action? 

The answer to this is no. Here's why:

The big thing to understand here is that HTTP is a stateless protocol. This means that the connection between the browser and the server is lost once the transaction ends. We must take this into consideration when redirecting because the application treats this as a brand new HTTP request and in turn wipes out the original instance variable that was declared in the original create controller action. 

### To Summarize

Rendering and Redirection are a crucial aspect of building a web application. It allows developers to build dynamic websites that can create a unique experience for individual users. When to use each of them can get very tricky in the process of creating these applications but reading more about them can help us to use them in the proper scenarios. Hope you enjoyed this article and good luck fellow developers!



