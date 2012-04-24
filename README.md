## Speaking Your Own Language

One of ruby's strongest features is its ability to be spoken with varying 
dialects. That ability allows for the language to be more flexible and fluent
in given circumstances compared to other languages.

### Exercise

The objective of the exercise is to define a domain specific language.

#### Domain

You are free to choose any domain. You are welcome to define a language that
parallels an existing language you are already familiar or you may define an
entirely new domain.

> The final product of the exercise is to be able to parse the language
  but it does not necessarily have to execute some code. So if the DSL
  you defined piloted a moon rover or moved a character in a virtual game
  world you do not need to develop the actual moon rover code or the 
  adapter to send the right commands to the game world.

#### Complexity

You are free to define how complex the language is and how extensive this
language changes Ruby's dialect.

> Within the exercise time you will likely not be able to completely define
  the language with all of the nuances you wish to include. So you should strive
  to complete what you would consider one entire feature or vertical slice. 
  This may mean you are only able to parse the launch sequence of your rover
  or the walk command for the game world character.


#### Goal

A DSL that has some of the features of a language you are already familiar like [RSpec](https://www.relishapp.com/rspec), [Rake](http://rake.rubyforge.org/), or [Capistrano](https://github.com/capistrano/capistrano/wiki).

An entirely new DSL that supports some of the features here:

```ruby
Chef.recipe "Chocolate Chip Cookies" do
  
  ingredient "butter", 1.cup, "softened"
  ingredient "white sugar", 1.cup
  ingredient "eggs", 2
  ingredient "vanilla extract", 2.tsps
  ingredient "all purpose flour", 3.cups
  ingredient "baking soda", 1.tsp
  ingredient "hot water", 2.tsps
  ingredient "salt", half.tsp
  ingredient "semisweet chocolate chips", 2.cups
  ingredient "walnuts", 1.cup, "chopped"
  
  instruction "Preheat oven to 350 degrees F (175 degrees C)."
  instruction "Cream together the butter, white sugar, and brown sugar until smooth."
  instruction "Beat in the eggs one at a time, then stir in the vanilla."
  instruction "Dissolve baking soda in hot water. Add to batter along with salt."
  instruction "Stir in flour, chocolate chips, and nuts."
  instruction "Drop by large spoonfuls onto ungreased pans."
  
  instruction "Bake for about 10 minutes in the preheated oven, or until edges are nicely browned."
  
  serves 4.dozen, "cookies"
  
end
```

[Original Recipe](http://allrecipes.com/recipe/best-chocolate-chip-cookies/)

### Exercise Retrospective


### Reading

* [Ruby Metaprogramming](http://pragprog.com/book/ppmetr/metaprogramming-ruby)

    > Chapter 3 - Wednesday: Blocks
    
* [What is a Domain Specific Language?](http://vimeo.com/40451457)

    > A video presentation by Kathy Van Stone at Pittsburgh Ruby Brigadge User
    Group

### Further Exercise

Within the short time allotted to the exercise you were likely only able to 
define the language or maybe one feature of the language done. With that as a
base, continue to build your language.

* Define the remaining features in your language specification

* Further refine the language that you defined to make it even more flexible,
  more like English or more verbose:

    > In the above example, that may be the ability to use the 
    singular `tsp` or `tsps`. This could also be defining more elements 

The use of an oven occurs often enough in cooking so it may be useful to have
its own element.

```ruby
Chef.recipe "Chocolate Chip Cookies" do
  
  # ...
  
  oven :preheat => 350.degrees 
  
end
```
You may implement the above and realize that it is not exactly the most English
friendly so you decide to try and implement.

```ruby
Chef.recipe "Chocolate Chip Cookies" do
  
  # ...
  
  preheat oven 350.degrees 
  
end
```

* Further refine the language to be less verbose:

    > In the above example, you may decide that some parts of the language
    are far too repetitive like the use of `ingredient` and `instruction`.
    
    
```ruby
recipe "Chocolate Chip Cookies" do
  
  ingredients do |add|
  
    add "butter", 1.cup, "softened"
    add "white sugar", 1.cup
    add "eggs", 2
    add "vanilla extract", 2.tsps
    add "all purpose flour", 3.cups
    add "baking soda", 1.tsp
    add "hot water", 2.tsps
    add "salt", half.tsp
    add "semisweet chocolate chips", 2.cups
    add "walnuts", 1.cup, "chopped"
    
  end
  
  instructions do |perform|
  
    perform "Preheat oven to 350 degrees F (175 degrees C)."
    perform "Cream together the butter, white sugar, and brown sugar until smooth."
    perform "Beat in the eggs one at a time, then stir in the vanilla."
    perform "Dissolve baking soda in hot water. Add to batter along with salt."
    perform "Stir in flour, chocolate chips, and nuts."
    perform "Drop by large spoonfuls onto ungreased pans."
  
    perform "Bake for about 10 minutes in the preheated oven, or until edges are nicely browned."
    
  end
  
  serves 4.dozen "cookies"
  
end
```

* If the language has a practical application, complete the implementation so
  that it is able to accomplished it's designed goal.

    > From the above example, you may have it:
    > 
    > Generate HTML output 
    > 
    > Defines multiple recipes you could have it combine all the ingredients and
    > create a shopping list with summed quantities of the all ingredients
    >
    > Post the recipe to a remote service
    