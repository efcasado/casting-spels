## Location, Location, Location

The first command we'd want to have is a command that tells us about the location we're standing in. What do we need to do? Perhaps if we start with describing all places, we can work towards one place. This may sound a little backwards, but Lisp is very good with lists, so let's try it!

We can get there in stages by plying with our new game state and record fucntions. Getting the player location is super-easy:

```lisp
> (state-player state)
living-room
```

What about a place's description? Well, that burried a few more levels deep in our game state. Let's take a look. Let's refresh our memories about the fields defined in the records we will be accessing:

```lisp
> (fields-state)
(objects places player)
> (fields-map)
(living-room garden attic)
> (fields-place)
(description exits)
```

Let's imagine our location is in ``living-room`` (which, indeed, it is...).

![](images/living_room.jpg)

To get the ``description`` field, we'll need a ``place`` record; to get the place, we'll need a specific element of the ``places`` field of the ``state`` record. Let's do it:

```lisp
> (place-description
    (car
      (state-places state)))
```
```lisp
"You are in the living-room of a wizard's house. There is a wizard snoring loudly on the couch."
>
```

Hey, that wasn't so bad! And we got to use our old friend ``car`` :-) But how do we turn this into a function? Let's start with seeing if we can get a description for *all* places:

```lisp
> (lists:map
    (lambda (x)
      (place-description x))
    (state-places state))
```
```lisp
("You are in the living-room of a wizard's house. There is a wizard snoring loudly on the couch."
 "You are in a beautiful garden. There is a well in front of you."
 "You are in the attic of the wizard's house. There is a giant welding torch in the corner.")
```

Wow! How did we do that? Well, there are a few new things here. This function uses another common *functional programming* technique: the use of *Higher Order Functions*. This means that the ``map`` function in the Erlang standard library's ``lists`` module is taking another function as a parameter so that they can call them themselves.

But what function? Good question! This is and example of the Function with No Name, or *anonymous functions*. *Anonymous functions* don't use ``define``; instead, you use the ``lambda`` form. *Anonymous functions* are useful for doing a task that you don't want to bother writing a function for (or to wrap something that's not a function ...).