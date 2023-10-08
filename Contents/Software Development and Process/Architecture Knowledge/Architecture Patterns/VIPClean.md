##### VIPER, VIP, Clean

- **VIPER** *(View, Interactor, Presenter, Entity, Router)* is an architectural pattern that aims to create highly modular and decoupled code. **VIPER** enforces strict separation between components, making it easier to maintain and test each individual piece. It emphasizes loose coupling and dependency injection.

- **VIP** is a simplified version of **VIPER**, focusing on the essential components for building an iOS application:
    - *View*: Displays the user interface and handles user interactions.
    - *Interactor*: Contains the business logic and interacts with the data layer.
    - *Presenter*: Mediates between the view and the interactor, handling presentation logic.

- **Clean Architecture** is a software design principle that promotes separation of concerns and independence from external frameworks and libraries. It consists of several layers, each with its own responsibilities:
    - *Presentation Layer*: Handles user interactions, input validation, and UI rendering. It corresponds to the UI components in an iOS app.
    - *Domain Layer*: Contains the business logic and rules of the application. It is independent of the presentation layer and any external frameworks.
    - *Data Layer*: Deals with data persistence, remote API calls, and external services. It interacts with the data sources and provides data to the domain layer.

![VIPER, VIP, Clean](../../../../Figures/figure2.png)

https://www.youtube.com/watch?v=Szlgqnk6gHg