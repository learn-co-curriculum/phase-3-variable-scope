# Method Scope

## Objectives
1. Understand the concept of scope. 
2. Learn the scope of a method. 
3. Learn the scope of a local variable. 

## What is Scope?

Methods in ruby create their own scope. "Scope" refers to the areas of your program in which certain data is available to you. **Any local variable created outside of a method will be unavailable inside of a method. In addition, local variables created inside of a method 'fall out of scope' once you're outside the method.**

## Method Scope in Ruby

Think of a method as a castle. The `def` and `end` keywords are like the gates that keep out the barbarian hordes, dragons, etc. Let's take a look:

```ruby
evil_monster = "Bowser"

def princess_peaches_castle
  puts "#{evil_monster} is trying to kidnap Princess Peach!"
end
```

We've defined the variable `evil_monster` *outside* of the method, `princess_peaches_castle`. Then, we try to call on the `evil_monster` variable inside that method. Watch what happens when we invoke the method:

```ruby
princess_peaches_castle
  #=> NameError: undefined local variable or method `evil_monster' for main:Object
```

The `evil_monster` variable is out of scope for this method. The method can't access it **unless we pass it in as an argument**.

If we define our method to accept an argument, we can pass our variable into the method and the method will be able to operate on/use that variable. Let's take a look:

```ruby
evil_monster = "Bowser"

def princess_peaches_castle(evil_monster)
  puts "#{evil_monster} is trying to kidnap Princess Peach!"
end

princess_peaches_castle(evil_monster)
#> "Bowser is trying to kidnap Princess Peach!"

```

And now Mario can start his adventure.

So far, we've seen that variables defined outside of methods are not available inside methods (unless we pass them in as arguments). This works the other way around as well: variables defined inside of methods are not available outside of those methods. Let's take a look. 

If we define the following method to include a local variable:

```ruby
def practicing_method_scope
  im_trapped_in_the_method = "You can't access me outside this method!"
end
```

Trying to access that variable elsewhere in our program, *outside of this method*, will raise the following error:

```ruby
im_trapped_in_the_method
#=> NameError: undefined local variable or method `im_trapped_in_the_method' for main:Object
```

## Conclusion

Remember: A variable defined inside a method can't leave that method. It is not available to your program outside of the method. A variable designed outside of a method can only be made available to the code inside the method if you pass that variable in to the method as an argument. 
