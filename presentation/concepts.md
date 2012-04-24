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

## Blocks

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
    
      def ingredients
        yield self if block_given?
      end
    end
    
    cookie = ChocolateChipCookies.new
    
    cookie.ingredients do |c|
      c.ingredient "white sugar", 1
    end

!SLIDE

## Doing it cleanly 

    @@@ Ruby
    def using
    
      connection = Service.open(HOST,USER,PASS)

      yield connection if block_given?

      connection.close
      
    end
    
    using do |connection|
      connection.query "for big data"
    end
    
!SLIDE

## Doing it safely

    @@@ Ruby
    def safe_using

      begin
        connection = Service.open(HOST,USER,PASS)

        yield connection if block_given?

        connection.close
      rescue => exception
        warn "There was an error #{exception}"
      end
      
    end
    
    safe_using do |connection|
      connection.query "for even bigger data"
    end



!SLIDE

## Doing it responsively

    @@@ Ruby
    def find_me_all_things_that_are_equal_to(this_thing)
      
      all_things.map do |thing|
        
        yield thing if block_given? and thing == this_thing
        
        thing if thing == match_me
        
      end.compact
        
    end
    
    matches = find_me_all_things_that_are_equal_to "myself"
    
    find_me_all_things_that_are_equal_to "myself" do |a_match|
      # change this match
    end
    
        
!SLIDE

## Block Argument instead of `yield`

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

## `instance_eval`

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

!SLIDE

## `instance_eval` what?

    @@@ Ruby
    class ChocolateChipCookies
      def ingredient(name,amount,preparation_details = {})
        # implementation
      end

      def ingredients(&block)
        ingredient "white sugar", 1
      end
    end

    cookie = ChocolateChipCookies.new

    cookie.ingredients do
      
    end