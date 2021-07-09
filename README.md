# Variable Scope

## Learning Goals

- Understand the differences between variable scope in Ruby and JavaScript
- Use local variables and global variables

## Introduction

In this lesson, we'll introduce the concepts of method scope and variable scope.

## Variable Names and Scope

Naming variables is hard, but it is important. We need our code to be as
descriptive as possible. Any other developer reading over one of our programs
should be able to understand what our code does. A big part of this is having
variable (and method) names that are sensible and descriptive.

## What is Scope?

Methods in Ruby create their own scope. "Scope" refers to the areas of your
program in which certain data is available to you. **Any local variable created
outside of a method will be unavailable inside of a method. In addition, local
variables created inside of a method (i.e. in between the `def` and `end`
keywords of a method) 'fall out of scope' once you're outside the method.**

Let's take a look at the following example:

```rb
name = "Joe"

def greeting(name)
   puts "Hello, #{name}"
end
```

In this code snippet, we have a variable, `name`, set equal to a string,
`"Joe"`. Then we define a method, `#greeting`, that takes in an argument of
name. Are the `name` variable that is set equal to `"Joe"` and the `name`
variable we are using as a parameter (or argument) for our `#greeting` method
definition the same? Let's see.

If we call our greeting method in the following way:

```rb
greeting("Sophie")
```

What do we expect to be outputted to the terminal?

In this case, the above method invocation would `puts` out `Hello, Sophie` to
the terminal. It is true that we are setting a variable, `name`, equal to
`"Joe"` in this code snippet. But we are not using _that_ variable anywhere else
in our code. The `name` argument of the `#greeting` method is just a
placeholder. It means: when we call the `#greeting` method with an argument of,
say, `"Sophie"`, set the variable `name` _inside of the method_ equal to that
string argument.

The `name` variable inside of the `#greeting` method is different from the
`name` variable that we set equal to `"Joe"` outside of the method. The
`#greeting` method has its own scope, and variables inside of it don't know
about variables outside of it and vice versa.

## Method Scope in Ruby

Think of a method as a castle. The `def` and `end` keywords are like the gates
that keep out the barbarian hordes, dragons, etc. Let's take a look:

```rb
evil_monster = "Bowser"

def princess_peaches_castle
  puts "#{evil_monster} is trying to kidnap Princess Peach!"
end
```

We've defined the variable `evil_monster` _outside_ of the method,
`princess_peaches_castle`. Then, we try to call on the `evil_monster` variable
inside that method. Watch what happens when we invoke the method:

```rb
princess_peaches_castle
#=> NameError: undefined local variable or method `evil_monster' for main:Object
```

The `evil_monster` variable is out of scope for this method. The method can't
access it **unless we pass it in as an argument**.

In JavaScript, scope rules would allow us to use a variable in the outer scope
from our function:

```js
const evilMonster = "Bowser";

function princessPeachesCastle() {
  console.log(`${evil_monster} is trying to kidnap Princess Peach!`);
}
```

This is a key difference between Ruby and JavaScript: in Ruby, **local variables
are only available within the scope of the method they are defined in**.

If we define our method to accept an argument, we can pass our variable into the
method and the method will be able to operate on/use that variable. Let's take a
look:

```rb
evil_monster = "Bowser"

def princess_peaches_castle(evil_monster)
  puts "#{evil_monster} is trying to kidnap Princess Peach!"
end

princess_peaches_castle(evil_monster)
#=> "Bowser is trying to kidnap Princess Peach!"
```

The method call, which happens outside the method itself, has access to our
`evil_monster` variable. We can therefore make the value stored in
`evil_monster` available to `princess_peaches_castle` by passing it as an
argument when we call the method. So now Mario can start his adventure.

So far, we've seen that variables defined outside of methods are not available
inside methods (unless we pass them in as arguments). This works the other way
around as well: variables defined inside of methods are not available outside of
those methods. Let's take a look.

If we define the following method to include a local variable:

```rb
def practicing_method_scope
  im_trapped_in_the_method = "You can't access me outside this method!"
end
```

Trying to access that variable elsewhere in our program, _outside of this
method_, will raise the following error:

```rb
im_trapped_in_the_method
#=> NameError: undefined local variable or method `im_trapped_in_the_method' for main:Object
```

## Variable Types

So far, we've encountered one type of variable in Ruby: local variables. They're
called "local" because they don't ever leave the scope they're defined in. There
are other types of variables in Ruby as well, which can be defined using
different naming conventions:

- Local variables: must start with a lowercase letter or an underscore (\_): `name = "Lucy"`
- Global variables: must start with a dollar sign ($): `$name = "Lucy"`
- Instance variables: must start with an at symbol (@) `@name = "Lucy"`)
- Class variables: must start with two at symbols (@@) (`@@name = "Lucy"`)

We'll discuss instance variables and class variables later along with Object
Oriented Programming, but global variables can be useful to see how Ruby treats
different variable types with regards to their scope.

For example, we could use a global variable to make the `$evil_monster`
available everywhere in our code:

```rb
$evil_monster = "Bowser"

def princess_peaches_castle
  puts "#{$evil_monster} is trying to kidnap Princess Peach!"
end
```

You should **almost never** need to use global variables in your code. Having a
lot of global variables makes your code unpredictable and challenging to debug,
so you should reserve them for special cases (like application-wide
configuration).

## Conclusion

Remember: A local variable defined inside a method can't leave that method. It
is not available to your program outside of the method. A local variable defined
outside of a method can only be made available to the code inside the method if
you pass that variable in to the method as an argument.
