---
layout: post
title: "The convenience initializer in Swift"
---

A convenience initializer in Swift is a secondary initializer that provides a simplified or more convenient way to initialize an object. It is often used to offer default values or to configure the object in a particular way, while ultimately delegating the responsibility of full initialization to one of the class’s designated initializers.

Key Features:

* Delegation: A convenience initializer must call a designated initializer from the same class using self.init(...). It cannot directly initialize all the properties of the class itself.
* Optional Customization: It’s commonly used to provide additional ways to initialize an object, such as providing default values for parameters.
* Simplifies Object Creation: It reduces the need for boilerplate code when creating instances of a class by offering simplified ways to create those instances.

Syntax:

```swift
class MyClass {
    var name: String
    var age: Int
    
    // Designated initializer
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    // Convenience initializer
    convenience init() {
        self.init(name: "Default Name", age: 0)  // Calls the designated initializer
    }
}
```

Example:

In this example, init() is a convenience initializer that provides default values for the name and age properties, while the actual initialization is done by calling the designated initializer init(name:age:).

Rules:

* Convenience initializers must delegate to another initializer (either another convenience initializer or the designated initializer) in the same class.
* They cannot fully initialize the properties themselves but can offer shortcuts for object creation.

Use Cases:

* To provide sensible default values or simplified initialization paths.
* To offer alternative initialization logic based on different parameters.