## Table of contents
* [Closures](#closures)
* [Enumerations](#enumerations)
* [Classes vs Structs](#classes-vs-structs)
* [Properties](#properties)
  - [Stored properties](#stored-properties)
  - [Lazy stored properties](#lazy-stored-properties)
  - [Computed properties](#stored-properties)
  - [Property Observers](#property-observers)
* [Extensions](#extensions)
* [Protocols](#protocols)
  - [Protocols as Types](#protocols-as-types)
  - [Delegation](#delegation)
  - [Adding Protocol Conformance with an Extension](#adding-protocol-conformance-with-an-extension)
  - [Collections of Protocol Types](#collections-of-protocol-types)
  - [Class-Only Protocols](#class-only-protocols)
  - [Protocol Composition](#protocol-composition)
  - [Checking for Protocol Conformance](#checking-for-protocol-conformance)
* [Optionals](#optionals)
* [Automatic Reference Counting(ARC)](#automatic-reference-countingarc)
* [Grand Central Dispatch](#grand-central-dispatchgcd)

## Closures

_Closures_ are self-contained blocks of functionality that can be passed around and used in your code.

Closures can capture and store references to any constants and variables from the context in which they’re defined. This is known as _closing_ over those constants and variables. Swift handles all of the memory management of capturing for you.

Global and nested functions are actually special cases of closures. Closures take one of three forms:
* Global functions are closures that have a name and don’t capture any values.
* Nested functions are closures that have a name and can capture values from their enclosing function.
* Closure expressions are unnamed closures written in a lightweight syntax that can capture values from their surrounding context.

They are often used for functional programming patterns, such as mapping and filtering arrays, and for asynchronous programming. They can also be passed as arguments to functions and can be returned from functions as well. Closures are a powerful and flexible feature of Swift, and they are used extensively in the language’s standard library and APIs. 
It can capture and store values from the surrounding scope, making it a powerful tool for processing and communicating functionality in Swift.

Closures in Swift can cause **memory leaks** when they capture a strong reference to a captured object or when they create a strong reference cycle. This typically happens when a closure captures self (the instance of a class) and the closure is stored as a property or captured by another object that has a strong reference to it.

Use a weak reference to `self` to avoid a strong reference cycle

## Enumerations

An _enumeration_ defines a common type for a group of related values and enables you to work with those values in a type-safe way within your code.

Alternatively, enumeration cases can specify associated values of _any_ type to be stored along with each different case value, much as unions or variants do in other languages. You can define a common set of related cases as part of one enumeration, each of which has a different set of values of appropriate types associated with it.

Enum syntax:
```swift
enum CompassPoint {
    // enumeration definition goes here
    case north
    case south
    case east
    case west
}
```

## Classes vs Structs

_Structures_ and _classes_ are general-purpose, flexible constructs that become the building blocks of your program’s code. You define properties and methods to add functionality to your structures and classes using the same syntax you use to define constants, variables, and functions.

Structures and classes in Swift have many things in common. Both can:
* Define properties to store values
* Define methods to provide functionality
* Define subscripts to provide access to their values using subscript syntax
* Define initializers to set up their initial state
* Be extended to expand their functionality beyond a default implementation
* Conform to protocols to provide standard functionality of a certain kind

##### Differences:
| Class  | Struct |
| ------------- | ------------- |
| reference type(stored on the heap)  | value type(stored on the stack) |
| supports inheritance  | does not support inheritance |
| mutable: let -> can use variables from struct even if they’re var  | immutable(constants)/true constant: let -> cannot use variables from struct even if they’re var |
| can be deinitialized | no need of deinitializers  |
| don't have initializers by default | have initializers by default  |

#### Structures and Enumerations Are Value Types

A _value_ type is a type whose value is copied when it’s assigned to a variable or constant, or when it’s passed to a function.

In fact, all of the basic types in Swift — integers, floating-point numbers, Booleans, strings, arrays and dictionaries — are value types, and are implemented as structures behind the scenes.

All structures and enumerations are value types in Swift. This means that any structure and enumeration instances you create — and any value types they have as properties — are always copied when they’re passed around in your code.

#### Classes Are Reference Types

Unlike _value_ types, _reference_ types are not copied when they’re assigned to a variable or constant, or when they’re passed to a function. Rather than a copy, a reference to the same existing instance is used.

Variables of a _reference_ type point to the same data; therefore, operations on one variable will affect the data specified by another variable.

#### Identity Operators

Because classes are _reference_ types, it’s possible for multiple constants and variables to refer to the same single instance of a class behind the scenes. (The same isn’t true for structures and enumerations, because they’re always copied when they’re assigned to a constant or variable, or passed to a function.)
It can sometimes be useful to find out whether two constants or variables refer to exactly the same instance of a class. To enable this, Swift provides two identity operators:
* Identical to (===)
* Not identical to (!==)

**Note** that _identical to_ (represented by three equal signs, or ===) doesn’t mean the same thing as _equal to_ (represented by two equal signs, or ==). Identical to means that two constants or variables of class type refer to exactly the same class instance. _Equal to_ means that two instances are considered equal or equivalent in value, for some appropriate meaning of equal, as defined by the type’s designer.

## Properties

_Properties_ associate values with a particular class, structure, or enumeration. Stored properties store constant and variable values as part of an instance, whereas computed properties calculate (rather than store) a value. Computed properties are provided by classes, structures, and enumerations. Stored properties are provided only by classes and structures.

Stored and computed properties are usually associated with instances of a particular type. However, properties can also be associated with the type itself. Such properties are known as type properties.

In addition, you can define property observers to monitor changes in a property’s value, which you can respond to with custom actions. Property observers can be added to stored properties you define yourself, and also to properties that a subclass inherits from its superclass.

You can also use a property wrapper to reuse code in the getter and setter of multiple properties.

#### Stored Properties

In its simplest form, a stored property is a constant or variable that’s stored as part of an instance of a particular class or structure. Stored properties can be either _variable_ stored properties (introduced by the `var` keyword) or _constant stored_ properties (introduced by the `let` keyword).

#### Lazy Stored Properties

A _lazy stored_ property is a property whose initial value isn’t calculated until the first time it’s used. You indicate a lazy stored property by writing the `lazy` modifier before its declaration.

Lazy properties are useful when the initial value for a property is dependent on outside factors whose values aren’t known until after an instance’s initialization is complete. Lazy properties are also useful when the initial value for a property requires complex or computationally expensive setup that shouldn’t be performed unless or until it’s needed.

```swift
class DataImporter {
    /*
    DataImporter is a class to import data from an external file.
    The class is assumed to take a nontrivial amount of time to initialize.
    */
    var filename = "data.txt"
    // the DataImporter class would provide data importing functionality here
}


class DataManager {
    lazy var importer = DataImporter()
    var data: [String] = []
    // the DataManager class would provide data management functionality here
}


let manager = DataManager()
manager.data.append("Some data")
manager.data.append("Some more data")
// the DataImporter instance for the importer property hasn't yet been created
```

The `DataManager` class has a stored property called `data`, which is initialized with a new, empty array of String values. Although the rest of its functionality isn’t shown, the purpose of this `DataManager` class is to manage and provide access to this array of String data.
Part of the functionality of the `DataManager` class is the ability to import data from a file. This functionality is provided by the `DataImporter` class, which is assumed to take a nontrivial amount of time to initialize. This might be because a `DataImporter` instance needs to open a file and read its contents into memory when the `DataImporter` instance is initialized.
Because it’s possible for a `DataManager` instance to manage its data without ever importing data from a file, `DataManager` doesn’t create a new `DataImporter` instance when the `DataManager` itself is created. Instead, it makes more sense to create the `DataImporter` instance if and when it’s first used.
Because it’s marked with the `lazy` modifier, the `DataImporter` instance for the importer property is only created when the importer property is first accessed, such as when its filename property is queried:

```swift
print(manager.importer.filename)
// the DataImporter instance for the importer property has now been created
// Prints "data.txt"
```

#### Computed Properties

In addition to stored properties, classes, structures, and enumerations can define _computed properties_, which don’t actually store a value. Instead, they provide a getter and an optional setter to retrieve and set other properties and values indirectly.

```swift
struct Point {
    var x = 0.0, y = 0.0
}
struct Size {
    var width = 0.0, height = 0.0
}
struct Rect {
    var origin = Point()
    var size = Size()
    var center: Point {
        get {
            let centerX = origin.x + (size.width / 2)
            let centerY = origin.y + (size.height / 2)
            return Point(x: centerX, y: centerY)
        }
        set(newCenter) {
            origin.x = newCenter.x - (size.width / 2)
            origin.y = newCenter.y - (size.height / 2)
        }
    }
}
var square = Rect(origin: Point(x: 0.0, y: 0.0),
    size: Size(width: 10.0, height: 10.0))
let initialSquareCenter = square.center
// initialSquareCenter is at (5.0, 5.0)
square.center = Point(x: 15.0, y: 15.0)
print("square.origin is now at (\(square.origin.x), \(square.origin.y))")
// Prints "square.origin is now at (10.0, 10.0)"
```

The `Rect` structure also provides a _computed property_ called `center`. The current center position of a `Rect` can always be determined from its `origin` and `size`, and so you don’t need to store the center point as an explicit `Point` value. Instead, `Rect` defines a custom getter and setter for a computed variable called `center`, to enable you to work with the rectangle’s center as if it were a real stored property.

#### Property Observers

Property observers observe and respond to changes in a property’s value. Property observers are called every time a property’s value is set, even if the new value is the same as the property’s current value.

You can add property observers in the following places:
* Stored properties that you define
* Stored properties that you inherit
* Computed properties that you inherit

You have the option to define either or both of these observers on a property:
* willSet is called just before the value is stored.
* didSet is called immediately after the new value is stored.

The example below defines a new class called `StepCounter`, which tracks the total number of steps that a person takes while walking. This class might be used with input data from a pedometer or other step counter to keep track of a person’s exercise during their daily routine.

```swift
class StepCounter {
    var totalSteps: Int = 0 {
        willSet(newTotalSteps) {
            print("About to set totalSteps to \(newTotalSteps)")
        }
        didSet {
            if totalSteps > oldValue  {
                print("Added \(totalSteps - oldValue) steps")
            }
        }
    }
}
let stepCounter = StepCounter()
stepCounter.totalSteps = 200
// About to set totalSteps to 200
// Added 200 steps
stepCounter.totalSteps = 360
// About to set totalSteps to 360
// Added 160 steps
stepCounter.totalSteps = 896
// About to set totalSteps to 896
// Added 536 steps
```

Property observers are useful for value change notifications. The ideal scenario is to use property observers when we need to add some logic or need to do user interface changes whenever there is a change in property value.

## Extensions

_Extensions_ add new functionality to an existing class, structure, enumeration, or protocol type. This includes the ability to extend types for which you don’t have access to the original source code.

Extensions in Swift can:
* Add computed instance properties and computed type properties
* Define instance methods and type methods
* Provide new initializers
* Define subscripts
* Define and use new nested types
* Make an existing type conform to a protocol

An extension can extend an existing type to make it adopt one or more protocols.

```swift
extension SomeType: SomeProtocol, AnotherProtocol {
    // implementation of protocol requirements goes here
}
```

Extensions can add computed instance properties and computed type properties to existing types. This example adds five computed instance properties to Swift’s built-in `Double` type, to provide basic support for working with distance units:

```swift
extension Double {
    var km: Double { return self * 1_000.0 }
    var m: Double { return self }
    var cm: Double { return self / 100.0 }
    var mm: Double { return self / 1_000.0 }
    var ft: Double { return self / 3.28084 }
}
let oneInch = 25.4.mm
print("One inch is \(oneInch) meters")
// Prints "One inch is 0.0254 meters"
```

## Protocols

A _protocol_ defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. The protocol can then be _adopted_ by a class, structure, or enumeration to provide an actual implementation of those requirements. Any type that satisfies the requirements of a protocol is said to _conform_ to that protocol.

#### Protocols as Types

Protocols don’t actually implement any functionality themselves. Regardless, you can use a protocol as a type in your code.

You can use it in many places like:
- As a parameter type or return type in a function, method, or initializer
- As the type of a constant, variable, or property
- As the type of items in an array, dictionary, or other container
- Because protocols are types, begin their names with a capital letter to match the names of other types in Swift (such as `Int`, `String`, and `Double`).

#### Delegation

_Delegation_ is a design pattern that enables a class or structure to hand off (or _delegate_) some of its responsibilities to an instance of another type. This design pattern is implemented by defining a protocol that encapsulates the delegated responsibilities, such that a conforming type (known as a delegate) is guaranteed to provide the functionality that has been delegated. Delegation can be used to respond to a particular action, or to retrieve data from an external source without needing to know the underlying type of that source.

```swift
protocol CallBackDelegate {
  func somethingHappened()
}

class Class1 {
  var delegate: CallBackDelegate?

  func doSomething() {
      delegate?.somethingHappened()
  }
}

class Class2: CallBackDelegate {
  func somethingHappened() {
      print("Something happened callback called")
  }
}

let class1 = Class1()
let class2 = Class2()
class1.delegate = class2
class1.doSomething()
// Prints "Something happened callback called"
```

#### Adding Protocol Conformance with an Extension

You can extend an existing type to adopt and conform to a new protocol, even if you do not have access to the source code for the existing type. Extensions can add new properties, methods, and subscripts to an existing type, and are therefore able to add any requirements that a protocol may demand.

```swift
protocol Growable {
  var age: Int? { get }
}

class Human {
  var name: String?
  var weight: Float?
}

extension Human: Growable {
  var age: Int? {
      return 10
  }
}

let humanObj = Human()
humanObj.age //Prints "10"
```

#### Collections of Protocol Types

Protocols can be used as a type to be stored in collection types like array or dictionary.

#### Class-Only Protocols

You can limit protocol adoption to class types (and not structures or enumerations) by adding the `AnyObject` protocol to a protocol’s inheritance list.

```swift
protocol SomeClassOnlyProtocol: AnyObject, SomeInheritedProtocol {
    // class-only protocol definition goes here
}
```

In the example above, `SomeClassOnlyProtocol` can only be adopted by class types.

#### Protocol Composition

It can be useful to require a type to conform to multiple protocols at the same time. You can combine multiple protocols into a single requirement with a protocol composition. Protocol compositions behave as if you defined a temporary local protocol that has the combined requirements of all protocols in the composition. Protocol compositions don’t define any new protocol types.

```swift
protocol Named {
    var name: String { get }
}
protocol Aged {
    var age: Int { get }
}
struct Person: Named, Aged {
    var name: String
    var age: Int
}
func wishHappyBirthday(to celebrator: Named & Aged) {
    print("Happy birthday, \(celebrator.name), you're \(celebrator.age)!")
}
let birthdayPerson = Person(name: "Malcolm", age: 21)
wishHappyBirthday(to: birthdayPerson)
// Prints "Happy birthday, Malcolm, you're 21!"
```

In this example, the Named protocol has a single requirement for a gettable String property called name. The Aged protocol has a single requirement for a gettable Int property called age. Both protocols are adopted by a structure called Person.
The example also defines a wishHappyBirthday(to:) function. The type of the celebrator parameter is Named & Aged, which means “any type that conforms to both the Named and Aged protocols.” It doesn’t matter which specific type is passed to the function, as long as it conforms to both of the required protocols.

#### Checking for Protocol Conformance

You can use the `is` and `as` operators described in _Type Casting_ to check for protocol conformance, and to cast to a specific protocol. Checking for and casting to a protocol follows exactly the same syntax as checking for and casting to a type:
* The `is` operator returns `true` if an instance conforms to a protocol and returns `false` if it does not.
* The `as?` version of the downcast operator returns an optional value of the protocol’s type, and this value is `nil` if the instance does not conform to that protocol.
* The `as!` version of the downcast operator forces the downcast to the protocol type and triggers a runtime error if the downcast does not succeed.


## Optionals

_Optionals_ are a convenient mechanism for handling situations where the value of a variable may be missing.

The _Optional type_ is an enumeration with two cases. `Optional.none` is equivalent to the nil literal. `Optional.some(Wrapped)` stores a wrapped value.

There are two ways to declare Optionals:

1. Optional (Optional<T>): An optional represents a value of type `T`, which can be either non-zero or nil. Declared by adding `?` after the data type (for example, `Int?` or `String?`). It allows you to explicitly indicate that a value may be missing.
2. Implicitly Unwrapped Optional (T!): An implicitly unwrapped optional represents a value of type `T`, which can also be either non-zero or nil. However, it differs from a regular optional in that it assumes that the value will be non-zero when accessed. Declared by adding `!` after the data type (eg `String!`). Used in situations where we are confident that the value will be non-zero and want to avoid having to expand the optional every time.

In order to use value of an optional, it needs to be _unwrapped_. There are several ways to do it:

1. If-statement
```swift
var someValue:Int?
        
if someValue != nil {
	print("It has some value \(someValue!)")
} else {
	print("doesn't contain value")
}
```

2. Optional Binding (if-let)
```swift
var someValue:Int?
       
if let temp = someValue {
	print("It has some value \(temp)") 
} else {
	print("doesn't contain value")
}
```

3. Guard statement
```swift
let someValue:Int? = 5
guard let temp = someValue else {
  return
}
print("It has some value \(temp)")
```

4. Nil-coalescing operator
```swift
var someValue:Int!
let unwrappedValue:Int = someValue ?? 5
print(unwrappedValue) //Prints "5"
```

5. Force unwrapping (!)

When you’re certain that an instance of Optional contains a value, you can unconditionally unwrap the value by using the forced unwrap operator
```swift
let number = Int("42")!
print(number) // Prints "42"
```

**Note** that unconditionally unwrapping a `nil` instance with `!` triggers a runtime error.

6. Optional chaining

_Optional chaining_ is a process for querying and calling properties, methods, and subscripts on an optional that might currently be `nil`. If the optional contains a value, the property, method, or subscript call succeeds; if the optional is `nil`, the property, method, or subscript call returns `nil`. Multiple queries can be chained together, and the entire chain fails gracefully if any link in the chain is `nil`.

```swift
something?.someValue?.someMethod()
```
If `nil` is encountered at any point in the above chain, the application does not crash - `nil` is returned instead.


## Automatic Reference Counting(ARC)

Swift uses _Automatic Reference Counting (ARC)_ to track and manage your app’s memory usage. ARC automatically frees up the memory used by class instances when those instances are no longer needed.

However, in a few cases ARC requires more information about the relationships between parts of your code in order to manage memory for you.

Reference counting applies only to instances of classes. Structures and enumerations are value types, not reference types, and aren’t stored and passed by reference.

#### How ARC works?

Every time you create a new instance of a class, ARC allocates a chunk of memory to store information about that instance. This memory holds information about the type of the instance, together with the values of any stored properties associated with that instance.

Additionally, when an instance is no longer needed, ARC frees up the memory used by that instance so that the memory can be used for other purposes instead. This ensures that class instances don’t take up space in memory when they’re no longer needed.

However, if ARC were to deallocate an instance that was still in use, it would no longer be possible to access that instance’s properties, or call that instance’s methods. Indeed, if you tried to access the instance, your app would most likely crash.

To make sure that instances don’t disappear while they’re still needed, ARC tracks how many properties, constants, and variables are currently referring to each class instance. ARC will not deallocate an instance as long as at least one active reference to that instance still exists.

To make this possible, whenever you assign a class instance to a property, constant, or variable, that property, constant, or variable makes a strong reference to the instance. The reference is called a _strong reference_ because it keeps a firm hold on that instance, and doesn’t allow it to be deallocated for as long as that strong reference remains.

#### ARC in Action

This example starts with a simple class called `Person`, which defines a stored constant property called `name`:

```swift
class Person {
    let name: String
    init(name: String) {
        self.name = name
        print("\(name) is being initialized")
    }
    deinit {
        print("\(name) is being deinitialized")
    }
}
```

You can now create a new Person instance

```swift
var reference1: Person?
var reference2: Person?
var reference3: Person?

reference1 = Person(name: "John Appleseed")
// Prints "John Appleseed is being initialized"
```

Because the new `Person` instance has been assigned to the `reference1` variable, there’s now a _strong reference_ from `reference1` to the new `Person` instance. Because there’s at least one strong reference, ARC makes sure that this Person is kept in memory and isn’t deallocated.

If you assign the same `Person` instance to two more variables, two more strong references to that instance are established:

```swift
reference2 = reference1
reference3 = reference1
```

There are now _three_ strong references to this single Person instance.

If you break two of these strong references (including the original reference) by assigning nil to two of the variables, a single strong reference remains, and the Person instance isn’t deallocated:
```swift
reference1 = nil
reference2 = nil
```

ARC doesn’t deallocate the Person instance until the third and final strong reference is broken, at which point it’s clear that you are no longer using the Person instance:
```swift
reference3 = nil
// Prints "John Appleseed is being deinitialized"
```

#### Strong Reference Cycles Between Class Instances

It’s possible to write code in which an instance of a class never gets to a point where it has zero strong references. This can happen if two class instances hold a _strong reference_ to each other, such that each instance keeps the other alive. This is known as a **_strong reference cycle_**.

Here’s an example of how a strong reference cycle can be created by accident. This example defines two classes called Person and Apartment, which model a block of apartments and its residents:
```swift
class Person {
    let name: String
    init(name: String) { self.name = name }
    var apartment: Apartment?
    deinit { print("\(name) is being deinitialized") }
}

class Apartment {
    let unit: String
    init(unit: String) { self.unit = unit }
    var tenant: Person?
    deinit { print("Apartment \(unit) is being deinitialized") }
}
```

This next code snippet creates a specific Person instance and Apartment instance and assign these new instances to the john and unit4A variables:
```swift
var john: Person?
var unit4A: Apartment?

john = Person(name: "John Appleseed")
unit4A = Apartment(unit: "4A")
```

Here’s how the strong references look after creating and assigning these two instances. The john variable now has a strong reference to the new Person instance, and the unit4A variable has a strong reference to the new Apartment instance:

![Reference Cycle](/Figures/Swift/figure1.png)

You can now link the two instances together so that the person has an apartment, and the apartment has a tenant. 

```swift
john!.apartment = unit4A
unit4A!.tenant = john
```
Here’s how the strong references look after you link the two instances together:

![Reference Cycle1](/Figures/Swift/figure2.png)

Unfortunately, linking these two instances creates a strong reference cycle between them. The Person instance now has a strong reference to the Apartment instance, and the Apartment instance has a strong reference to the Person instance. Therefore, when you break the strong references held by the john and unit4A variables, the reference counts don’t drop to zero, and the instances aren’t deallocated by ARC.

Here’s how the strong references look after you set the john and unit4A variables to nil:

![Reference Cycle2](/Figures/Swift/figure3.png)

#### Resolving Strong Reference Cycles Between Class Instances

Swift provides two ways to resolve strong reference cycles when you work with properties of class type: _weak_ references and _unowned_ references.

_Weak_ and _unowned_ references enable one instance in a reference cycle to refer to the other instance without keeping a strong hold on it. The instances can then refer to each other without creating a strong reference cycle.

Use a _weak_ reference when the other instance has a shorter lifetime — that is, when the other instance can be deallocated first. In the Apartment example above, it’s appropriate for an apartment to be able to have no tenant at some point in its lifetime, and so a weak reference is an appropriate way to break the reference cycle in this case. 

In contrast, use an _unowned_ reference when the other instance has the same lifetime or a longer lifetime. Use an unowned reference only when you are sure that the reference always refers to an instance that hasn’t been deallocated.
**Note** that if you try to access the value of an unowned reference after that instance has been deallocated, you’ll get a runtime error.

#### Strong Reference Cycles for Closures

A strong reference cycle can also occur if you assign a closure to a property of a class instance, and the body of that closure captures the instance. This capture might occur because the closure’s body accesses a property of the instance, such as `self.someProperty`, or because the closure calls a method on the instance, such as `self.someMethod()`. In either case, these accesses cause the closure to “capture” self, creating a strong reference cycle.

This strong reference cycle occurs because closures, like classes, are _reference_ types. When you assign a closure to a property, you are assigning a reference to that closure. In essence, it’s the same problem as above — two strong references are keeping each other alive. However, rather than two class instances, this time it’s a class instance and a closure that are keeping each other alive.

Closures in Swift can cause _memory leaks_ when they capture a strong reference to a captured object or when they create a strong reference cycle. This typically happens when a closure captures `self` (the instance of a class) and the closure is stored as a property or captured by another object that has a strong reference to it.

Use a weak reference to `self` to avoid a strong reference cycle.

## Grand Central Dispatch(GCD)

Multitasking allows us to run several tasks simultaneously. _GCD (Grand Central Dispatch)_ is the simplest way to achieve multitasking in iOS. We add tasks to dispatch queues which in turn gets executed on multiple threads simultaneously.

Every iOS application has a main thread, which is there to display user interface and listen to events. Complex computations may slow down the main thread and freeze the app. Here is where multithreading comes into play. We must move all the heavy lifting to a background thread, and then move the result back to the main. This describes the main pattern of work with Grand Central Dispatch.

#### Queues 

As mentioned before, GCD operates on _dispatch queues_ through a class aptly named DispatchQueue.We submit units of work to this queue and GCD will execute them in a _FIFO_ order (First In, First Out), guaranteeing that the first task submitted is the first one started.

Queues can be either _serial_ or _concurrent_.

* Serial queues guarantee that only one task runs at any given time. GCD controls the execution timing.We won’t know the amount of time between one task ending and the next one beginning

* Concurrent queues allow multiple tasks to run at the same time. The queue guarantees tasks start in the order we add them. Tasks can finish in any order and we have no knowledge of the time it will take for the next task to start, nor the number of tasks that are running at any given time.

GCD provides three main types of queues:

1. _Main queue_: runs on the main thread and is a serial queue.
```swift
DispatchQueue.main.async {
    self.view.backgroundColor = UIColor.red
}
```

2. _Global queues_: Concurrent queues that are shared by the whole system. There are four such queues with different priorities : high, default, low, and background. The background priority queue has the lowest priority and is throttled in any I/O activity to minimise negative system impact.
```swift
let globalQueue = DispatchQueue.global()
globalQueue.async {
    for i in 0 ..< 5 {
        print(“\(i)”)
    }
}
```

3. _Custom queues_: queues that you create which can be serial or concurrent. Requests in these queues actually end up in one of the global queues.
```swift
let concurrentQueue = DispatchQueue(label: “queuename”, attributes: .concurrent)
concurrentQueue.sync {
    print(“Executing concurrent queue”)
}

let serialQueue = DispatchQueue(label: “queuename”)
serialQueue.sync {
    print(“Executing serial queue”)
}
```

When sending tasks to the global concurrent queues, you don’t specify the priority directly. Instead, you specify a _Quality of Service (QoS)_ class property. This indicates the task’s importance and guides GCD in determining the priority to assign to the task.

Tasks running on main / UI thread are always at a high priority because they keep the app responsive, whereas tasks running on background thread are of least priority. Ultimately all tasks complete their execution but priority decides which one will be completed first.

* **User-interactive**: This represents tasks that must complete immediately in order to provide a nice user experience. Use it for UI updates, event handling and small workloads that require low latency. The total amount of work done in this class during the execution of your app should be small. This should run on the main thread.
* **User-initiated**: The user initiates these asynchronous tasks from the UI. Use them when the user is waiting for immediate results and for tasks required to continue user interaction. They execute in the high priority global queue.
* **Utility**: This represents long-running tasks, typically with a user-visible progress indicator. Use it for computations, I/O, networking, continuous data feeds and similar tasks. This class is designed to be energy efficient. This will get mapped into the low priority global queue.
* **Background**: This represents tasks that the user is not directly aware of. Use it for prefetching, maintenance, and other tasks that don’t require user interaction and aren’t time-sensitive. This will get mapped into the background priority global queue.


With GCD, you can dispatch a task either _synchronously_ or _asynchronously_.

A _synchronous_ function returns control to the caller after the task completes. You can schedule a unit of work synchronously by calling DispatchQueue.sync(execute:).

```swift
func syncWithSerialExecution() {
    let serialQueue = DispatchQueue(label: “queue1”)
    serialQueue.sync {
        for index in 0..<5 {
            print(“⚪️”, index)
        }
    }

    serialQueue.sync {
        for index in 0..<5 {
            print(“🔷”, index)
        }
    }
}

/*Prints 
⚪️ 0
⚪️ 1
⚪️ 2
⚪️ 3
⚪️ 4
🔷 0
🔷 1
🔷 2
🔷 3
🔷 4
*/
```

An _asynchronous_ function returns immediately, ordering the task to start but not waiting for it to complete. Thus, an asynchronous function does not block the current thread of execution from proceeding on to the next function. You can schedule a unit of work asynchronously by calling DispatchQueue.async(execute:).

```swift
func asyncWithSerialExecution() {
    let serialQueue = DispatchQueue(label: “queue1”)
    serialQueue.async {
        for index in 0..<5 {
            print(“⚪️”, index)
        }
    }
    
    serialQueue.async {
        for index in 0..<5 {
            print(“🔷”, index)
        }
    }
}

/*Prints
⚪️ 1
⚪️ 2
⚪️ 3
⚪️ 4
🔷 0
🔷 1
🔷 2
🔷 3
🔷 4
*/
```

#### Deadlock

A _deadlock_ is a situation in which two or multiple threads wait for each other indefinitely. Locks are a common cause in Swift in which a serial queue sync operation triggers another sync operation on the same queue.

Let’s use the above example to demonstrate a deadlock in code by creating an image fetcher:

```swift
final class ImageFetcher {

    /// Defaults to a serial queue.
    let lockQueue = DispatchQueue(label: "image-fetcher-lock-queue")

    private var imageCache: [URL: UIImage] = [:]

    func fetchImage(for url: URL, completion: @escaping (UIImage) -> Void) {
        lockQueue.async {
            let image = UIImage() // Imagine being a remotely fetched image.
            self.imageCache[url] = image

            DispatchQueue.main.sync {
                completion(image)
            }
        }
    }

    func hasCachedImage(for url: URL) -> Bool {
        lockQueue.sync {
            imageCache[url] != nil
        }
    }
}
```

The usage of these image fetcher methods determines whether a deadlock occurs or not. For example, you could start fetching an image and check for a cached image right after:

```swift
imageFetcher.fetchImage(for: imageURL, completion: { image in
    imageView.image = image
    self.hideLoadingIndicator()
})

if imageFetcher.hasCachedImage(for: imageURL) == false {
    showLoadingIndicator()
}
```

When there’s no cached image available, we’re showing a loading indicator as we’re expecting an image fetching request to start. While the code might look fine, it causes a deadlock to occur.

You can solve a deadlock by breaking synchronization in one of the places. In this example, it makes perfect sense to asynchronously dispatch back to the main thread after image fetching succeeds:

```swift
func fetchImage(for url: URL, completion: @escaping (UIImage) -> Void) {
    lockQueue.async {
        let image = UIImage() // Imagine being a remotely fetched image.
        self.imageCache[url] = image

        /// We're now dispatching using async.
        DispatchQueue.main.async {
            completion(image)
        }
    }
}
```

The best way to solve this would be to use async / await in combination with actors. However, that requires rewriting your code in multiple places, which is not always realistic.







