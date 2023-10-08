##### MVC, MVP and MVVM

- **MVC** is a traditional pattern that focuses on separating responsibilities among the model, view, and controller. 
- **MVP** and **MVVM** are variations that put more emphasis on separating presentation logic from the view. 
- **MVP** introduces a presenter layer, while **MVVM** introduces a view model layer to further decouple the view from the model.

**Key differences**:

- In **MVP**, the presenter directly interacts with the view, whereas in **MVVM**, the view model interacts with the view indirectly through data binding.
- **MVP** focuses on the presenter as the central coordinator, while **MVVM** emphasizes the view model as the mediator between the view and the model.
- **MVVM** leverages data binding to automate the synchronization between the view and the view model, reducing the need for explicit updates.

![MVC, MVP and MVVM](../../../../Figures/figure1.jpeg)

https://www.simform.com/blog/mvc-mvp-mvvm-ios-app-development/