!SLIDE quote

# Concepts

!SLIDE

## Units

    @@@ Ruby
    16.ounces
    2.cups

!SLIDE quote

## Monkeypatching

    @@@ Ruby
    class Fixnum

      def ounces
        # vanity
        self
      end

      def cup
        # conversion to ounces
        self * 16
      end
    end

!SLIDE quote

## Sharing with Modules

    @@@ Ruby
    module Measurements
      def ounces
        self
      end
    end

    class Fixnum
      include Measurements
    end

    class Float
      include Measurements
    end

!SLIDE

## Defining Elements

    @@@ Ruby
    cookie.ingredient "butter", 1.cup, "softened"
    cookie.ingredient "semisweet chocolate chips", 2.cups

!SLIDE quote

## Optional Parentheses

    @@@ Ruby
    def ingredient(name,amount,preparation_details)
      # implementation
    end

    cookie.ingredient("butter", 1.cup, "softened")

    cookie.ingredient "butter", 1.cup, "softened"

!SLIDE quote

## Optional Parameters

    @@@ Ruby
    def ingredient(name,amount,preparation_details = "")
      # implementation
    end

    cookie.ingredient "butter", 1.cup, "softened"
    cookie.ingredient "white sugar", 1.cup


!SLIDE quote

## Trailing Hash Arguments

    @@@ Ruby
    def ingredient(name,amount,details = {})
      details # => { :prepare => 'with love', ...
    end

    ingredient "white sugar", 1.cup, :prepare => 'with love',
      :serve => 'with kindness'


!SLIDE quote

## Properties

    @@@ Ruby
    class CookieRecipe

      # You want this...
      ingredient "butter", 1.cup, "softened"
      ingredient "white sugar", 1.cup

    end


!SLIDE quote

## Class Methods

    @@@Ruby
    class ChocolateChipCookies

      # You should implement this...
      def self.ingredient(name,amount,preparation_details)
        # implementation
      end

      ingredient "butter", 1.cup, "softened"
      ingredient "white sugar", 1.cup

    end

!SLIDE

## Succinct Style

    @@@ Ruby
    cookie = ChocolateChipCookies.new
    cookie.ingredient "white sugar", 1

    # ... but maybe you prefer

    cookie.ingredients do |c|
      c.ingredient "white sugar", 1
    end

!SLIDE

## Block Arguments

    @@@ Ruby
    class ChocolateChipCookies
      def ingredient(name,amount,preparation_details = {})
        # implementation
      end
      
      # you should implement this...
      def ingredients
        yield self if block_given?
      end
    end

    cookie = ChocolateChipCookies.new

    cookie.ingredients do |c|
      c.ingredient "white sugar", 1
    end

## Without that annoying 'c'

    @@@ Ruby
    cookie = ChocolateChipCookies.new

    cookie.ingredients do
      ingredient "white sugar", 1
    end
    

!SLIDE

## `instance_eval`

    @@@ Ruby
    class ChocolateChipCookies
      def ingredient(name,amount,preparation_details = {})
        # implementation
      end

      def ingredients(&block)
        self.instance_eval(&block) if block?
      end
    end

    cookie = ChocolateChipCookies.new

    cookie.ingredients do
      ingredient "white sugar", 1
    end