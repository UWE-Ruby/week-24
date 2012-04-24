!SLIDE quote

# Concepts

!SLIDE quote

## Monkeypatching

    @@@ Ruby
    class Fixnum
      def cup
        self
      end
    end

!SLIDE quote

## Module Monkeypatching

    @@@ Ruby
    module Measurements
      def cup
        self
      end
    end
    
    class Fixnum
      include Measurements
    end

!SLIDE quote

## Class Methods

    @@@Ruby
    class ChocolateChipCookies

      def self.ingredient(name,amount,preparation_details)
        # implementation
      end

      ingredient("white sugar", 1.cup,:prepare => 'with love', 
        :serve => 'with kindness')

    end

!SLIDE quote

## Methods

Parentheses can be optional

    @@@ Ruby
    def ingredient(name,amount,preparation_details)
      # implementation
    end

    ingredient("butter", 1.cup, "softened")
    
    ingredient "butter", 1.cup, "softened"

!SLIDE quote

## Methods

Optional Parameters

    @@@ Ruby
    def ingredient(name,amount,preparation_details = "")
      # implementation
    end

    ingredient "white sugar", 1.cup
    

!SLIDE quote

## Methods

Trailing Hash Arguments

    @@@ Ruby
    def ingredient(name,amount,preparation_details = {})
      # implementation
    end

    ingredient "white sugar", 1.cup, :prepare => 'with love', 
      :serve => 'with kindness'
    
!SLIDE

## Block Arguments

    @@@ Ruby
    class ChocolateChipCookies
      def ingredient(name,amount,preparation_details = {})
        # implementation
      end
    
      def ingredients
        yield self if block_given?
      end
    end
    
    cookie = ChocolateChipCookies.new
    
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

      def ingredients(&block)
        block.call(self) if block
      end
    end

    cookie = ChocolateChipCookies.new

    cookie.ingredients do |c|
      c.ingredient "white sugar", 1
    end
    
!SLIDE

## instance_eval

    @@@ Ruby
    class ChocolateChipCookies
      def ingredient(name,amount,preparation_details = {})
        # implementation
      end

      def ingredients(&block)
        self.instance_eval(&block) if block_given?
      end
    end

    cookie = ChocolateChipCookies.new

    cookie.ingredients do
      ingredient "white sugar", 1
    end
    