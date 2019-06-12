# Ownership, Borrowing and Mutability

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

## Mutability is Distinct from Exclusive Access

In Rust, references are described as mutable and immutable. However, interior mutability and thread safe classes mean that an immutable reference may refer to an object that is actually mutable. In truth, Rust references would be better described as exclusive and shared.

In Adamant, mutability is about more than just exclusive access, though it is still somewhat coupled. This can be clearly seen in the fact that owned references can be mutable or immutable. It is also clear that the declaration of classes and structs as mutable or immutable has nothing to do with exclusive access. Though, immutable structs are much more likely to be copy types.

It is troubling that in Rust a lock-free queue would be held through immutable references yet one could call methods that mutated the queue even though they were not marked as mutating the object. Ideally, there would be a way to mark thread safe classes so that their mutability was correctly reflected, but it would then be considered safe to have multiple mutable references to it. There are potential issues with that however do to memory invalidation. In particular, assigning an enum struct to a different case could break a reference to a field in the struct (remember that it is possible to promote a reference to a variable to a reference to an interface it implements). A second common example is references to the elements of a list that would be invalidated when the list was resized. Note that both of these have the character of using references to members of objects and so it might be possible to have a scheme that ruled these out while still allowing for the safe cases.
