# Objective-C Notes and stuff

### Resources

- http://cocoadevcentral.com/d/learn_objectivec/
- http://rypress.com/tutorials/objective-c/

### .h and .m files
The class **interface** is usually stored in the `ClassName.h` file, and defines instance variables and public methods.

The **implementation** is in the `ClassName.m` file and contains the actual code for these methods. It also often defines private methods that aren't available to clients of the class.

### + vs - before method name
A single dash before a method name means it’s an instance method. A plus before a method name means it’s a class method.

**init**
```objc
- (id) init {
 if ( self = [super init] ) {
   [self setCaption:@"Default Caption"];
   [self setPhotographer:@"Default Photographer"];
 }
 return self;
}
```
The second line essentially just asks the superclass to do its own initialization. The if statement is verifying that the initialization was successful before trying to set default values.

### Memory management
Objective-C’s memory management system is called reference counting. All you have to do is keep track of your references and the runtime does the actual freeing of memory.

In simplest terms, you alloc an object, maybe retain it at some point, then send one release for each alloc/retain you sent. So if you used alloc once and then retain once, you need to release twice.



### What is the use of `@property`?
`@property` offers a way to define the information that a class is intended to encapsulate. If you declare an object/variable using @property, then that object/variable will be accessible to other classes importing its class.

List of attributes of `@property`:
- atomic.
- nonatomic.
- retain.
- copy.
- readonly.
- readwrite.
- assign.
- strong.
- http://rypress.com/tutorials/objective-c/properties

### Weak self vs strong self:

**tl;dr**: A `strong` property is one where you increment the reference count of the object. A `weak` reference doesn't increment the reference count of the object.

More info on all that here:
- _Capturing Myself_: https://blackpixel.com/writing/2014/03/capturing-myself.html
- _What is the difference between strong, retain, nonatomic, etc in iOS?_ [Quora](https://www.quora.com/What-is-the-difference-between-strong-retain-nonatomic-etc-in-the-Objective-C-iOS-property)
