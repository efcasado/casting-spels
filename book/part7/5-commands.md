## Supporting Commands

```lisp
(defspel go (direction)
  `(progn
    (! ,(whereis 'game-server) (tuple 'go ',direction))
    '<-))

(defspel view ()
  `(progn
    (! ,(whereis 'game-server) (tuple 'view))
    '<-))

(defspel i ()
  `(progn
    (! ,(whereis 'game-server) (tuple 'inv))
    '<-))

(defspel take (item)
  `(progn
    (! ,(whereis 'game-server) (tuple 'take ',item))
    '<-))
```


```lisp
(view)
<-
>
You are in the living-room of a wizard's house. There is a wizard snoring loudly on the couch.
You see a whiskey-bottle on the ground. You see a bucket on the ground.
There is a door going west from here. There is a stairway going upstairs from here.

(go west)
<-
>
You are in a beautiful garden. There is a well in front of you.
You see a frog on the ground. You see a chain on the ground.
There is a door going east from here.
```