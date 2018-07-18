---
layout: post
title:      "The Wonderful World of Arrays"
date:       2018-07-18 20:55:18 +0000
permalink:  the_wonderful_world_of_arrays
---


Array, arrays, arrays. They are everywhere! This, however, is not a bad thing. In the short amount of time that I have been coding, I have realized that arrays are a very crucial part of programming. Let me explain... cause I'm sure you're wondering why is that Brenden?

Arrays are a very simple data structure which can hold any type of data in list form. This means you can store anything from strings, integers, other arrays, hashes, and even a mix of all of these (this is not recommended, but still doable). The beauty of this data structure is that there are many ways to access it from within your methods or functions and manipulate them to create more complex code, but before you start manipulating the data there are some basic rules you should know to help you understand this structure.

Like I mentioned earlier, arrays can store anything from strings, integers, other array, hashes, and even a mix of all of these (still not recommended). It is much wiser to keep your arrays populated with one kind of element. Arrays are declared by listing variable names or literals separated by commas (,) and wrapped in square brackets []. To create an array within Ruby you can call it two different ways: new_array = [] or new_array = Array.new. 

Another very important aspect about arrays is how you can select each individual element. Normally when you make a list you start at 1 but in programming the computer starts at 0. In arrays these numbers are referred to as the index. So your first element in an array would be accessed with an index of 0 or array[0]. The brackets are how you would refer to the specific index you want to access. Once you have created your magical array, it is time to use it whever need be! 

Now lets talk about how you can maniuplate arrays since you have a grasp of the basics. There are a ton of methods you can call on arrays and you can see all of them at [https://ruby-doc.org/core-2.4.1/Array.html](http://), but for the sake of not completey boring you, I'm going to show you a couple that I find enjoyable and very useful. 

##### I'll start with a couple basic methods

The Shovel Method

This is pretty simple method which allows you to add an element to the *end* of an array.

```
my_array = ["cat", "dog", "mouse"]

my_array << " bird" 
=> ["cat", "dog", "mouse", "bird"]
```


The .Pop Method 

This method allows you to remove an element from the *end* of an array.

```
my_array = ["cat", "dog", "mouse", "bird"]

my_array.pop
=> "bird"
```

These are just some simple methods that allow you to add and remove elements from your array. Now I'll show you a couple more advanced methods that let you do some fun stuff to your array. 

The .Each Method

This is a method that allows you to iterate over each individual element within your array and pass a block of code on those specific elements.

```
animals = ["cat", "dog", "mouse", "bird"]

def zoo_animals(animals)
   animals.each do |animal|
     puts "We have #{animal}'s in the zoo!"
   end
end 
=> "We have cat's in the zoo!"
=> "We have dog's in the zoo!"
=> "We have mouse's in the zoo!"
=> "We have bird's in the zoo!"
```

I know there are some more complex concepts in this code but just know that the .each method is very useful when needing to work on each individual element within your array. 

The .Sort Method

I recently learned this method and it kinda blew my mind! This method is similar to .each except that when it iterates over your array, it's actually comparing two elements within the array and arranging them in the order that you define within your block of code. 

```
numbers = [4, 8, 10, 2, 14, 3]

def numbers_ascending(numbers)
   numbers.sort 
end 
=> 2, 3, 4, 8, 10, 14
```

This is possible because the .sort method uses something called the spaceship operator (<=>). So when you you add the .sort method to your array it is comparing the first two elements on its first iteration and placing them in the proper order. With the spaceship operator this would like like a <=> b. 

As you can see there are a lot of different things you can do with arrays. There are quite a few more methods you can call on arrays to manipulate them in all kinds of ways and the internet is your best friend when it comes to discovering the countless options. I hope this article has explained some basics and even showed you some cool advanced methods you can use on your coding journey!




