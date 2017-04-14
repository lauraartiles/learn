# Swift Notes
## Resources
Swift interview questions: https://www.raywenderlich.com/110982/swift-interview-questions-answers

Ray Wenderlich: https://www.raywenderlich.com/category/swift

## Value type vs. reference types

**Value types** keep a unique copy of their data, while **reference types** share a single copy of their data.
Swift represents a reference type as a class. This is similar to Objective-C, where everything that inherits from NSObject is stored as a reference type. Closures are also reference types.
There are many kinds of value types in Swift, such as `struct`, `enum`, and `tuple`s.
### Reference type example:
```swift
class Dog {
  var wasFed = false
}

let dog = Dog()
let puppy = dog

puppy.wasFed = true

dog.wasFed     // true
puppy.wasFed   // true
```

**Note:** `puppy` and `dog` both point to the exact same memory address.
### Value type example:
```swift
struct Cat {
  var wasFed = false
}

var cat = Cat()
var kitty = cat
kitty.wasFed = true

cat.wasFed        // false
kitty.wasFed      // true
```

**Note:** the kitty variable received a _copy_ of the value of cat instead of a reference.

### Mutability:
`var` and `let` function differently for reference types and value types.

For **reference** types, let means the ***reference*** must remain constant. In other words, you can’t change the instance the constant references, but you can mutate the instance itself.

For **value** types, let means the ***instance*** must remain constant. No properties of the instance will ever change, regardless whether the property is declared with `let` or `var`.

It’s much easier to control mutability with value types. To achieve the same immutability/mutability behavior with reference types, you’d need to implement immutable and mutable class variants such as `NSString` and `NSMutableString`.
#### When to use a value type
- Comparing instance data with == makes sense
- Copies should have independent state
- The data will be used in code across multiple threads

#### When to use a reference type
- Comparing instance identity with === makes sense
- You want to create a shared, mutable state

**Further reading:**
- https://www.raywenderlich.com/112027/reference-value-types-in-swift-part-1
- https://developer.apple.com/swift/blog/?id=10

## Automatic Reference Counting (ARC)
### How it works

Every time you create a new instance of a class, ARC allocates a chunk of memory to store information about that instance. This memory holds information about the type of the instance, together with the values of any stored properties associated with that instance.

To make sure that instances don’t disappear while they are still needed, ARC tracks how many properties, constants, and variables are currently referring to each class instance. ARC will not deallocate an instance as long as at least one active reference to that instance still exists.

### Defining a capture list:

- Define a capture in a closure as an `unowned` reference when the closure and the instance it captures will always refer to each other, and will always be deallocated at the same time
- Define a capture as a `weak` reference when the captured reference may become `nil` at some point in the future.
  - Weak references are always of an optional type, and automatically become `nil` when the instance they reference is deallocated.

## Delegation:

Delegation is a very important use of protocols. It’s a way to implement “blind communication” between a View and it’s Controller.

### How it plays out:
1. A View declares a delegation protocol (i.e. what the View wants the Controller to do for it)
2. The View’s API has a weak delegate property whose type is that delegation protocol
3. The View uses the delegate property to get/do things it can’t own or control on it’s own
4. The Controller declares that it implements the protocol
5. The Controller sets self as the delegate of the View by setting the property in #2 above
6. The Controller implements the protocol (probably has optional methods in it)
