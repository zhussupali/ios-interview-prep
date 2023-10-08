#### Behavioral Design Pattern Examples (Strategy)

The **Strategy** pattern is very common in Swift code. It’s often used in various frameworks to provide users a way to change the behavior of a class without extending it. **Strategy** pattern can be recognized by a method that lets a nested object do the actual work, as well as a setter that allows replacing that object with a different one.

```
protocol FactoryProtocol {
    func makeClassA() -> ClassA
    func makeClassB() -> ClassB
}

final class FactoryImpl: FactoryProtocol {
    func makeClassA() -> ClassA {
        let classA = ClassA()
        return classA
    }
    
    func makeClassB() -> ClassB {
        let classB = ClassB()
        return classB
    }
}

final class CustomizedFactoryImpl: FactoryProtocol {
    func makeClassA() -> ClassA {
        let classA = ClassA()
        // customize...
        return classA
    }
    
    func makeClassB() -> ClassB {
        let classB = ClassB()
        // customize...
        return classB
    }
}

// MARK: - Strategy

final class SomeClass {
    private let factory: FactoryProtocol
    
    init(factory: FactoryProtocol) {
        self.factory = factory
    }
}
```

so, when creating instance of ```SomeClass```, we can provide either ```FactoryImpl``` or ```CustomizedFactoryImpl```.