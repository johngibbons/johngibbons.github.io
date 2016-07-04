---
layout: post
title:  "Notes on Ruby String Manipulation"
date:   2014-05-15 12:59:51 -0700
categories: ruby strings
---

This is primarily a personal reference for Ruby string manipulation, but hopefully someone else finds it useful as well.

Retrieve the `n`th character using the `[]` notation:

```ruby
>> string = "Follow along with Ruby string manipulation."
=> "Follow along with Ruby string manipulation."

>> string[5]
=> "w"
```

Adding a second argument `m` outputs the number `m` of characters starting at the first argument `n`:

```ruby
>> string[7, 10]
=> "along with"
```

A range can also be used, with `n..m` inclusive of the `m` or `n...m`  exclusive `m`:

```ruby
>> string[7..11]
=> "along"

>> string[7...12]
=> "along"
```

Negative indices start from the right:

```ruby
>> string[7..-15]
=> "along with Ruby string"

>> string[23..-1]
=> "string manipulation."
```

Grab substrings by inputting a string search, will return nil if not present in the string:

```ruby
>> string["Ruby"]
=> "Ruby"

>> string["Java"]
=> nil
```

`slice()` works the same way, with `slice!()` destructively modifying the string:

```ruby
>> string.slice!("along with ")
=> "along with "

>> string
=> "Follow Ruby string manipulation."
```

Use `[]=` to set part of a string to a new value:

```ruby
>> string["Ruby"] = "Javascript"
=> "Javascript"

>> string
=> "Follow along with Javascript string manipulation."

>> string[-1] = "!"
=> "!"

>> string
=> "Follow along with Ruby string manipulation!"
```

Addition with strings using `+` generates a new string and leaves the original untouched:

```ruby
>> "a" + "b"
=> "ab"

>> str = "hello"
=> "hello"

>> str + " world!"
=> "hello world!"

>> str
=> "hello"
```

Use `<<` to permanently add a string to the original:

```ruby
>> str = "hello"
=> "hello"

>> str << " world!"
=> "hello world!"

>> str
=> "hello world!"
```

We can also combine strings using interpolation, which is non-destructive:

```ruby
>> str = "hello"
=> "hello"
 
>> "#{str} world!"
=> "hello world!"

>> str
=> "hello"
```
