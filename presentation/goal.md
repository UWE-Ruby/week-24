!SLIDE

# Goals

!SLIDE

A DSL that has some of the features of a language you are already familiar like 

* RSpec
* Rake
* Capistrano



!SLIDE

An entirely new DSL that supports some features like:

    @@@ruby
    Chef.recipe "Chocolate Chip Cookies" do
  
      ingredient "butter", 1.cup, "softened"
      ingredient "white sugar", 1.cup
      ingredient "eggs", 2

      preheat oven 350.degrees 

      instruction "Cream together the butter, ... smooth."

      serves 4.dozen, "cookies"

    end