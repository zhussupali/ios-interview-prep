##### Creational Design Pattern Examples (Factory, Builder)

**Factory** method is a pattern which solves the problem of creating product objects without specifying their concrete classes.
The **Factory** Method defines a method, which should be used for creating objects instead of using a direct constructor call (new operator). Subclasses can override this method to change the class of objects that will be created.

```
// MARK: - Factory

protocol SomeFactoryProtocol {
    func makeClassA() -> ClassA
    func makeClassB() -> ClassB
}

final class SomeFactoryImpl: FactoryProtocol {
    func makeClassA() -> ClassA {
        let classA = ClassA()
        return classA
    }
    
    func makeClassB() -> ClassB {
        let classB = ClassB()
        return classB
    }
}
```


**Builder** is a pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

```
// MARK: - Builder

final class BurgerBuilder {
    private(set) var meat: Meat = .beef
    private(set) var sauces: Sauces = []
    private(set) var toppings: Toppings = []
    
    func addSauces(_ sauce: Sauces) {
        sauces.insert(sauce)
    }
    func removeSauces(_ sauce: Sauces) {
        sauces.remove(sauce)
    }
    func addToppings(_ topping: Toppings) {
        toppings.insert(topping)
    }
    func removeToppings(_ topping: Toppings) {
        toppings.remove(topping)
    }
    func setMeat(_ meat: Meat) {
        self.meat = meat
    }
    
    func build() -> Burger {
        return Hamburger(
            meat: meat,
            sauce: sauces,
            toppings: toppings
        )
    }
}
```