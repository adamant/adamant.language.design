# Ownership

## Reference Recovered Mutability

An interesting situation can occur.

```adamant
public Swap(a: ref var Point, b: ref var Point) -> void
{
    let t = move a; // TODO does this need to be move *a or something?
    a = move b;
    b = move t;
}

var a = mut new Point(1, 1) // a: ~own mut Point
var b = new Point(2, 2); // b: ~own Point
Swap(ref var a, ref var b);
```

No one can mutate the object originally referenced by `b`. Yet, the swap function which can't mutate the values of either of its arguments is able to move object referenced by `b` into `a` thereby allowing the calling code to mutate it. This seems counter intuitive at first. However, since both references own their objects, the swap is simply recovering the mutability through changing ownership.
