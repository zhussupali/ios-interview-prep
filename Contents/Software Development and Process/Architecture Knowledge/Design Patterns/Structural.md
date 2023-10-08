##### Structural Design Pattern Examples (Adapter, Facade)

The **Adapter** pattern is pretty common in Swift code. It’s very often used in systems based on some legacy code. In such cases, **Adapters** make legacy code work with modern classes.

```
// MARK: - Adapter

class LegacyClass {
    // parameters and methods
}

// first method
final class LegacyClassAdapter: LegacyClass {
    // customize legacy class
}

final class LegacyClassAdapter2 {
    private var legacyClass = LegacyClass()
}
```

**Facade** design pattern that provides a simplified interface to a library, a framework, or any other complex set of classes.

```
// MARK: - Facade

final class Facade {
    private var subsystem1: Subsystem1
    private var subsystem2: Subsystem2

    init(subsystem1: Subsystem1 = Subsystem1(),
         subsystem2: Subsystem2 = Subsystem2()) {
        self.subsystem1 = subsystem1
        self.subsystem2 = subsystem2
    }

    func operation() -> String {

        var result = "Facade initializes subsystems:"
        result += " " + subsystem1.operation1()
        result += " " + subsystem2.operation1()
        result += "\n" + "Facade orders subsystems to perform the action:\n"
        result += " " + subsystem1.operationN()
        result += " " + subsystem2.operationZ()
        return result
    }
}

final class Subsystem1 {

    func operation1() -> String {
        return "Sybsystem1: Ready!\n"
    }

    func operationN() -> String {
        return "Sybsystem1: Go!\n"
    }
}

final class Subsystem2 {

    func operation1() -> String {
        return "Sybsystem2: Get ready!\n"
    }
    
    func operationZ() -> String {
        return "Sybsystem2: Fire!\n"
    }
}
```