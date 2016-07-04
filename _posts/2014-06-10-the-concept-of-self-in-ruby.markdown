---
layout: post
title:  "The Concept of 'Self' in Ruby"
date:   2014-06-10 12:59:51 -0700
categories: ruby OOP
---

The concept of `self` in Ruby is an important one.  At any given point when a program is running, there is one and only one `self`.  Let's go over the various contexts that determine what `self` is:

```ruby
puts "Self is #{self}"
=> "Self is main"

class C
    puts "Self is #{self}"
    => "Self is C"

    def self.class_method
        puts "Self is #{self}"
        => "Self is C"
    end

    def inst_method
        puts "Self is #{self}"
        => "Self is c (instance of C)"
    end

    module M
        puts "Self is #{self}"
        => "Self is C::M (nested module M)"
    end
end

obj = Object.new
def obj.singleton_method
    puts "Self is #{self}"
    => "Self is obj (method receiver object)"
end

class D < C
end

D.class_method
=> "Self is D"
```

As you can see `self` changes whenever we see `class`, `module`, or `def`.  If within a class or module, `self` refers to the class or module.  Within any method, `self` refers to the object that called the method.  This means that within instance methods, `self` is referring to the instance it is being called on.

When a subclass calls a parent's class method, `self` is still referring to the subclass, not the superclass, because it is the object that called the method.

**So why should we care?**

Well, because being self comes with some privileges.

One is that any methods called without an explicit receiver default to `self`.  Here is an example:

```ruby
class C
   
    def x
        puts "I'm in C#x"
        y
    end

    def y
        puts "Now in C#y"
    end

end

c = C.new
c.x
=> "I'm in C#x"
   "Now in C#y"
```

You can see that the instance method `y` is being called without an explicit receiver.  Since `self` is an instance of `C` within `x`, this is equivalent to calling `self.y`, and `y` runs.  Note that if you also had a local variable named `y`, it would take precedence, so it is best to avoid naming variables and methods the same.

