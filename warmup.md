## Data model warmup

Spend a few minutes thinking about the *data model* for your final project. While you may or may not use a SQL database for your project, it's still helpful to understand the structure and relationship of your data.

### Define your objects

First, list out the major "nouns" for your project. For instance, if it's a movie database, you might have:

```
Movie
Director
Actor
...
```

You should end up with at least 3, possibly as many as 10. Pick one (or at most two) "central" objects.

### Define your major fields

For each of your objects, decide what the major fields are, and their type:

```
Movie
. title (str)
. running time (int, minutes)
. theatrical release date (date)
. mpaa rating (choice: R, G, PG, PG-13...)

Director
. name (str)
. birthday (date)
. deathday (date)
```

### Define your relationships

For each of your objects, define how they relate to the others. You only need to define the relationship one way:

```
Movie
. has a director
. has many actors

Director
. has zero or more awards
```
