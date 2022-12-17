# Single-Integer Representation of the Path Taken to Draw an n-Pointed Star
---

This is a super-obvious thing but I thought it was cool because I independantly discovered it (I haven't searched for if this is written about because I'm not in any math theory circles and wouldn't know what to begin searching for)

This only works for stars you can construct via vertex connection.

If you label the points on a star based on how you draw them (starting with 1 (whatever you set that as, for a 5 pointed star I chose the top-most point), ending at n points) you can represent every other variation of path to draw that star (in two dimensions) with a single integer. I wanted these operations to be able to be single-lines of Python code and here's my first attempt at that.

```python
def path(value, points):
    return [
        (i + abs(value) - (value > 0)) % points + 1 
        for i in range(
                        points - 1 if value < 0 else 0, 
                        -1 if value < 0 else points, 
                        -1 if value < 0 else 1
                      )
    ]

def compress(values):
    return values[0] * (
        int(values[1] == path(values[0], len(values))[1]) * 2 - 1
    )

print(compress([3, 4, 5, 1, 2])) # 3
print(compress([3, 2, 1, 5, 4])) # -3

print(path(3, 5)) # [3, 4, 5, 1, 2]
print(path(-3, 5)) # [3, 2, 1, 5, 4]
```

I represent the path taken around each point as the sign of the integer, clockwise for positive, counter-clockwise for negative (look at how you teeter along the top-most point for a more intuitive understanding of this, falling to the left when you draw is counter-clockwise and vice versa)

The integer's absolute value is equal to the number of point you start with, the number of times you have to shift the list of points in the path by -1 or 1 (depending on the way you rotate around the points).

I got inspired by a Twitter post asking people how they draw their stars, and people commented on how much variation there was. I wanted to see how much variation there was (I think this is 20 different paths for a regular star polygon with 5 points "by connecting one vertex of a simple, regular, p-sided polygon to another, non-adjacent vertex and continuing the process until the original vertex is reached again" [1])

Side note my definitions and whole premise might be wrong! If you can create a star with a path that doesn't follow the logic here, but my brain and gut tell me that it isn't possible (something with the angles being the same meaning you have to go to the same point every time time) (my rude brain says what if there was a way to create a star where >2 points share a line so that going forward with one angle you could choose two separate points, I'd love to know if there's some weird technicallity where that can happen even if it seems super unlikely)

This also works for compressing the path taken around the degenerate cases, "stars" with points less than 5 (quadrilaterals, triangles).

---
Additional media

![](https://pbs.twimg.com/media/FkMkv0qXkAMesDo?format=png&name=900x900)

---
Source(s)

[1] https://en.wikipedia.org/wiki/Star_polygon#Construction_via_vertex_connection
