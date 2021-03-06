---
layout: docs
title:  "Range"
source: "core/src/main/scala/Range.scala"
---
## Range

`Range` represents a range [x, y] that can be generated by using discrete operations [Enum](enum).

## Supported Operations

- `start`: starting value of `Range`.
- `end`: ending value of `Range`.
- `toList`: returns all the values in the `Range` as a `List`.
- `contains(value)`: verifies `value` is within the `Range`.
- `contains(range)`: verifies `range` is within the `Range`.
- `toStreaming`: returns all the values in the `Range [start, end]`
- `reverse`: returns the reverted range `Range [end, start]`
- `-(other)`: Calculate the difference with `Range`.
	- It returns a tuple with the difference to the right and to the left of `Range`.
	- It basically calculates what is to the *left* of `other` that is in `Range` and what is to the *right* of `other` that is in `Range` (in both cases it does not include elements in `other`)
- toString: returns 
	
## Inverted Range

Note that if x > y and we create the range [x, y] it will be treated as the **inverted** range [y, x].
	
## Using Range

We can get the values from a range using **generate** or **toList** functions. 
We can also get the string representing the range in math notation. `Range(x, y)` is represented by **[x, y]** and `Range.empty` is represented by **[]** by using
`cats.Show`

```tut
import dogs._, cats._, cats.implicits._, dogs.syntax.all._, dogs.Range._
                                                                                                                                  
val range = Range(1, 10)
range.show

range.toStreaming.toList
```

We can get the inverted range using the **reverse** functions

```tut
range.reverse.show
```

Asking for **start** and **end** on a Range

```tut
range.start
range.end
```

Asking for a value within Range

```tut
range.contains(5)
```

Asking for a value that is not within Range

```tut
range.contains(20)
```

Asking for the difference between two Ranges returns 0, 1, or 2 result ranges

```tut
Range(10, 20).show
(range - Range(5, 9)).show
(range - Range(30, 40)).show
(range - Range(15, 18)).show
(range - Range (5, 30)).show
```

Creating an **inverted** range

```tut
val range = Range(50, 20)

range.toStreaming.toList
```

The reverse of a range should be its inverted range

```tut
val range = Range(20, 30)
range.show

val other = Range(30, 20)
other.show

range.reverse.toList == other.toList
```
