---
tags:
  - rails
  - ruby
  - web-development
  - databases
slug: enum-active-record
date: 2016-11-25
---
Today at work I saw a really weird exception in prod. The code is in a Rails project using ActiveRecord and was something like this:

```
if some_things_fetched_from_db.any?
  some_things_fetched_from_db.first.a_method
else
  another_value
end
```

And the dreaded exception that makes every rubyist want to cry:

```
NoMethodError: undefined method `a_method' for nil:NilClass
```

![Confused face](fry-wtf.webp)

If there are `any?` of my things how can the first one be `nil`?

When I saw this I had to remind myself of the best debugging advice I ever got: There has to be a reason. Computers are just machines, they just follow instructions. If the code after `if` was executed, the condition before it *had* to be true. But `[nil].any?` is false, so what’s up?

It turns out calling `any?` on an `ActiveRecord::Relation` is not the same thing as calling `any?` on a regular ruby `Enumerable` thing. Who knew?

If you call `any?` on an active record relation without a block it just runs a `COUNT` on the collection of things it *would* return if it were to actually return any things, since `ActiveRecord::Relations` are lazy. They only ever *really* get stuff from the database when the data they represent is absolutely necessary. Until then they are just an object that *knows how* to fetch the things they were originally asked to fetch.

![Wtf gif](duh.gif)

This causes problems if the things that are supposed to be in the relation could possibly be gone by the time you need them. Unlikely, yes, but possible, obviously.

ActiveRecord’s lazy loading caused a race condition. So `[the_thing_i_thought_was_here].any?` returned true, but by the time `[the_thing_i_thought_was_here].first` was executed, `the_thing_i_thought_was_here` had been deleted by another job spawned by a callback running in another process accessing the same database. Because sometimes good people write bad code.

So, next time something looks impossible and makes no sense, remember:
1. Things are not always what they seem.
2. `ActiveRecord::Relation` s are lazy.

Happy coding!