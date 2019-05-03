---
layout: post
title:      "I Have a Form_For That! (Rails Forms)"
date:       2019-05-03 23:22:12 +0000
permalink:  i_have_a_form_for_that_rails_forms
---


The first time I was introduced to Ruby on Rails I was pretty blown away. It was the first programming framework that I learned and I have to say I somewhat fell in love. I had just learned how to build applications using Sinatra and thought it was a pretty awesome tool, but then I saw what Rails could do... 

One main feature of Rails that I really enjoyed using was the From Helpers. It allowed me to avoid writing out all the HTML to buld a form, and in turn gave me the ability to do more complex features. In this article I'm going to break down the different form helpers provided in Rails and even touch upon a new one that was launched in the Rails 5.1 release. 

## Basic Forms in HTML


Creating forms with HTML can be a nuisancce at times, especially when they are extra long with way too many input fields. They can get even trickier when you need the form to send data to a specific api endpoint or to be associated with a database model. Here's an html form to create a user:

```

<form class="new_user" id="new_user" action="/users" method="post">
    <label for="user_name">Name</label>
    <input type="text" name="user[name]" id="user_name">
    <br>
    <label for="user_password">Password</label>
    <input type="password" name="user[password]" id="user_password">
    <br>
    <input type="submit" name="commit" value="Create User" data-disable-with="Create User">
</form>

```

As you can see, writing all this out can get complex pretty quick. If you look closely at the form you can see that we are passing an action and method attribute to our form to create a new user. This is great and all but Rails is super picky when it comes to submitting forms. This particular form wouldn't make the cut when submitted. This is where Form helpers come to the rescue. 


## Form Helpers

When I first learned how to use Form helpers, I honestly couldn't believe what they did. As you saw from the previous form that we did, it takes some time and complexity to acheive. However, with form helpers this can be achieved with a lot less work and with quite a bit of "magic".

There's three different helpers that help us to bulid quick and useful forms in Rails, `form_tag`, `form_for`, and `form_with`. The last one, `form_with`, was introduced in the release of Rails 5.1 and essentially combines the former two helpers. 


### form_tag


The `form_tag` is the most basic of helpers and in turn does less "magic" for you. It will still build out the form for you but you will need to be more explicit when declaring url paths and is mainly used when the form is not attached to a Controller#action. Let's use a basic search form as an example:

```

<%= form_tag("/search", method: "get") do %>
  <%= label_tag(:q, "Search for:") %>
  <%= text_field_tag(:q) %>
  <%= submit_tag("Search") %>
<% end %>

```

This will generate the following HTML: 

```

<form accept-charset="UTF-8" action="/search" method="get">
  <input name="utf8" type="hidden" value="&#x2713;" />
  <label for="q">Search for:</label>
  <input id="q" name="q" type="text" />
  <input name="commit" type="submit" value="Search" />
</form>

```

As you can see, we are declaring the route  we want the form parameter to be passed to in the `form_tag`. You can see this taking place in the line `<%= form_tag("/search", method: "get") do %>` and you can also see we specify the http request. This is still pretty awesome and you can see that Rails takes care of a lot for us even in the basic form helper, but Rails has a more powerful version of this...

### form_for


Form_for is the real deal. This helper allows us to bind a form to an object, allowing us to create/edit an object. As we saw in the `form_tag` example, we had to be explicit in which url path to use for submitting the form parameters but `form_for` allows us to abstract this away. Here's an example:

```

<%= form_for @user do |f| %>

  <%= f.label :name %>
  <%= f.text_field :name %>
  
  <%= f.label :password %>
  <%= f.password_field :password %>
  
  <%= f.submit  %>

<% end %>

```

This will produce the same code we saw in our first example of an html form.

```

<form class="new_user" id="new_user" action="/users" accept-charset="UTF-8" method="post">
  <input name="utf8" type="hidden" value="✓">
	<input type="hidden" name="authenticity_token"
value="QPJXa5iS/XNvodHhpcwV5q42RoGFWsmZkwL3ATHFfeKqxZ8IQsLs1QjJvcrdO3BwCaOfQ4TxNLDD0b6VbxiACg==">

  <label for="user_name">Name</label>
  <input type="text" name="user[name]" id="user_name">
  <br>
  <label for="user_password">Password</label>
  <input type="password" name="user[password]" id="user_password">
  <br>
  <input type="submit" name="commit" value="Create User" data-disable-with="Create User">

</form>

```

You can see immediately how much cleaner this code looks using `form_for`. Honeslty it's a little mind blowing that such little code can create all that html but it really does! You can see in the first line of `form_for` that we are passing an instance variable of the user which will attach this form to that object. The other cool thing about passing in this variable is that Rails will look for the appropriate url path on it's on, compared to the `form_tag` where we had to explicitly tell it where to send the data.


### form_with

* Maybe talk about form_with and about it's usage
* Use code snippets for example

If you look at the [Ruby on Rails 5.1 Release Notes](https://edgeguides.rubyonrails.org/5_1_release_notes.html), there is a note that form_for and form_tag are unifying into form_with. This biggest benefit with this new helper is `form_with` can generate form tags based on URLs, scopes or models

Let's check it out!

#### form_with using URLs

Let's use the same example we used in `form_for` and apply it with `form_with` and just a URL:

```

<%= form_with url: user_path do |f| %>
   <%= f.label :first_name %>
   <%= f.text_field :first_name %>
   <%= f.label :last_name %>
   <%= f.text_field :last_name %>
   <%= f.submit %>
<% end %>

```

As you can see it is very similar to the `form_tag` where we specify a specific URL (`user_path`)

#### form_with using models

The really cool thing about `form_with` is that it can also be used for passing in model objects, similar to `form_for`.

```

<%= form_with model: @user do |f| %>
   <%= f.label :first_name %>
   <%= f.text_field :first_name %>
  
   <%= f.label :last_name %>
   <%= f.text_field :last_name %>
  
   <%= f.submit %>
<% end %>

```

This will create the same HTML that was produced from using `form_for`.

Our biggest benefit from `form_with` is that we no longer need to worry about deciding between `form_tag` and `form_for`. We have a nifty helper that allows us to do either job with just a switch in the first line of the declared form. 


## Conclusion


Rails form helpers are awesome and the new addition of `form_with` really brings together all the benefits of both `form_tag` and `form_for`. You now have a tool that will allow you to build a form based on whatever your needs. Whether its a search form or a form to persist data to your database, you can have it taken care of with Rails form helpers. 

I would also suggest going through the [ Rails Guides](https://guides.rubyonrails.org/form_helpers.html#basic-structures) to learn about making more complex forms. You have quite a bit of options from allowing a model to accept nested attributes, having nested attributes, and other form helpers to create custom input fields. There is so much to play around with when going through these docs so take advantage!

Happy Coding!
