# Table Of Contents
* [Code Standards](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#code-standards)
  - [1. Naming](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#1-naming)
  - [2. Code Organization](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#2-code-organization)
    - [Protocol Conformance](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#protocol-conformance)
    - [Unused Code](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#unused-code)
    - [Minimal Imports](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#minimal-imports)
  - [3. Spacing](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#3-spacing)
  - [4. Comments and Documentation](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#4-comments-and-documentation)
  - [5. Function Declarations](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#5-function-declarations)
  - [6. Types](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#6-types)
    - [Constants](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#constants)
    - [Optionals](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#optionals)
  - [7. Classes vs Structs](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#7-classes-vs-structs)
    - [Which one to use?](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#which-one-to-use)
    - [Final](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#final)
  - [Useful Links](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#useful-links)
* [Code Review](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#code-review)
  - [What is a code review?](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#what-is-a-code-review)
  - [Why is performing a code review important?](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#why-is-performing-a-code-review-important)
  - [Steps of a good code review process](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#steps-of-a-good-code-review-process)
  - [Useful links](https://github.com/zhussupali/ios-interview-prep/blob/main/Contents/Software%20Development%20and%20Process/Architecture%20Knowledge/CodeStandards&CodeReviewProcess.md#useful-links-1)

# Code Standards
Coding standards are a set of guidelines, best practices, programming styles and conventions that developers follow when writing source code for a project.<br> Developers should follow these standards in order to, among other things:

- keep code maintainable
- keep code transparent, sane, and readable
- keep code scalable.

## 1. Naming
Descriptive and consistent naming makes software easier to read and understand. Use the Swift naming conventions described in the [API Design Guidelines](https://swift.org/documentation/api-design-guidelines/). Some key takeaways include:
- Meaningful and understandable variables name helps anyone to understand the reason of using it.
- Local variables should be named using camel case lettering starting with small letter (e.g. localData) whereas Global variables names should start with a capital letter (e.g. GlobalData). Constant names should be formed using capital letters only (e.g. CONSDATA).
- It is better to avoid the use of digits in variable names.
- The names of the function should be written in camel case starting with small letters.
- The name of the function must describe the reason of using the function clearly and briefly.

## 2. Code Organization
Use extensions to organize your code into logical blocks of functionality. <br>
Each extension should be set off with a `// MARK: – comment to keep things well-organized.`

### Protocol Conformance
In particular, when adding protocol conformance to a model, prefer adding a separate extension for the protocol methods.

This keeps the related methods grouped together with the protocol and can simplify instructions to add a protocol to a class with its associated methods.

Preferred:
```swift
class MyViewController: UIViewController {
  // class stuff here
}

// MARK: - UITableViewDataSource

extension MyViewController: UITableViewDataSource {
  // table view data source methods
}

// MARK: - UIScrollViewDelegate

extension MyViewController: UIScrollViewDelegate {
  // scroll view delegate methods
}
```
Not preferred:
```swift
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
  // all methods
}
```
### Unused Code
Unused (dead) code, including Xcode template code and placeholder comments should be removed. An exception is when your tutorial or book instructs the user to use the commented code.

### Minimal Imports
Import only the modules a source file requires. For example, don’t import UIKit when importing Foundation will suffice. Likewise, don’t import Foundation if you must import UIKit.

## 3. Spacing
Preferred:
```swift
if user.isHappy {
  // Do something
} else {
  // Do something else
}
```
Not preferred:
```swift
if user.isHappy
{
  // Do something
}
else {
  // Do something else
}
```
Preferred:
```swift
class TestDatabase: Database {
  var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```
Not preferred:
```swift
class TestDatabase : Database {
  var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```
##  4. Comments and Documentation
The code should be properly commented for understanding easily. Comments regarding the statements increase the understandability of the code.

## 5. Function Declarations
Keep short function declarations on one line including the opening brace:
```swift
func reticulateSplines(spline: [Double]) -> Bool {
  // reticulate code goes here
}
```
For functions with long signatures, put each parameter on a new line and add an extra indent on subsequent lines:
```swift
func reticulateSplines(
  spline: [Double], 
  adjustmentFactor: Double,
  translateConstant: Int, 
  comment: String
) -> Bool {
  // reticulate code goes here
}
```
Don't use `(Void)` to represent the lack of an input; simply use `()`. Use `Void` instead of `()` for closure and function outputs.

## 6. Types
Always use Swift's native types and expressions when available. Swift offers bridging to Objective-C so you can still use the full set of methods as needed.

Preferred:
```swift
let width = 120.0                                    // Double
let widthString = "\(width)"                         // String
```

Less preferred:
```swift
let width = 120.0                                    // Double
let widthString = (width as NSNumber).stringValue    // String
```

Not preferred:
```swift
let width: NSNumber = 120.0                          // NSNumber
let widthString: NSString = width.stringValue        // NSString
```

### Constants
Constants are defined using the `let` keyword and variables with the `var` keyword. Always use `let` instead of `var` if the value of the variable will not change.

Tip: A good technique is to define everything using `let` and only change it to `var` if the compiler complains!

### Optionals
Declare variables and function return types as optional with `?` where a `nil` value is acceptable.

Use implicitly unwrapped types declared with `!` only for instance variables that you know will be initialized later before use, such as subviews that will be set up in `viewDidLoad()`. Prefer optional binding to implicitly unwrapped optionals in most other cases.

When accessing an optional value, use optional chaining if the value is only accessed once or if there are many optionals in the chain:
```swift
textContainer?.textLabel?.setNeedsDisplay()
```
Use optional binding when it's more convenient to unwrap once and perform multiple operations:
```swift
if let textContainer = textContainer {
  // do many things with textContainer
}
```

## 7. Classes vs Structs

### Which one to use?

Remember, structs have [value semantics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures/). Use structs for things that do not have an identity. An array that contains [a, b, c] is really the same as another array that contains [a, b, c] and they are completely interchangeable. It doesn't matter whether you use the first array or the second, because they represent the exact same thing. That's why arrays are structs.

Classes have [reference semantics](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/classesandstructures/). Use classes for things that do have an identity or a specific life cycle. You would model a person as a class because two person objects are two different things. Just because two people have the same name and birthdate, doesn't mean they are the same person. But the person's birthdate would be a struct because a date of 3 March 1950 is the same as any other date object for 3 March 1950. The date itself doesn't have an identity.

### Final

Marking classes or members as `final` in tutorials can distract from the main topic and is not required.
<br>
Nevertheless, use of `final` can sometimes clarify your intent and is worth the cost. In the below example, `Box` has a particular purpose and customization in a derived class is not intended. Marking it `final` makes that clear.
```swift
// Turn any generic type into a reference type using this Box class.
final class Box<T> {
  let value: T
  init(_ value: T) {
    self.value = value
  }
}
```

## Useful links:
[iOS Best Practices and SWIFT Coding Standards: A Developer's Guide](https://www.perfomatix.com/ios-best-practices-and-swift-coding-standards/)<br>
[Swift Documentation](https://nshipster.com/swift-documentation/?source=post_page-----7f0badf4581b--------------------------------)<br>
[API Design Guidelines](https://www.swift.org/documentation/api-design-guidelines/?source=post_page-----7f0badf4581b--------------------------------)

# Code Review

## What is a code review?
A code review is a process in software development where one or more programmers examine another’s code to check for errors, bugs, or deviations from the project’s standards. 

Through constructive feedback, the code review process seeks to improve the quality and maintainability of an organization’s codebase. The review cycle repeats until the new code meets set standards and is ready to be shipped or integrated into the main codebase.

## Why is performing a code review important?
**Knowledge sharing**<br>
Giving feedback and sharing knowledge during code reviews creates an environment where team members learn from each other. When a developer reviews another’s code, they may learn something new about different approaches, algorithms, or techniques that were used. 
<br><br>
**Continuous improvement**<br>
Code reviews allow developers to give and receive feedback, enhancing team collaboration and continuous improvement. The iterative process of writing, reviewing, and revising code also encourages team members to improve their programming, communication, and teamwork skills. 
<br><br>
**Codebase consistency**<br>
Code reviews help ensure consistency in the coding style, which is vital for maintaining a clean, understandable, and transferable codebase. A consistent codebase reduces the build-up of technical debt and makes it easy for new developers joining a team to get up to speed and begin contributing. 
<br><br>
**Reducing testing cycles**<br>
Although code reviews are not a substitute for testing, they can help reduce the number of testing cycles required by catching and fixing issues early in the development process. This way, developers save time and resources that would otherwise be spent on lengthy testing and debugging, resulting in a more efficient development process and a higher-quality final product.
<br><br>
**Documentation**<br>
Through code reviews, developers can ensure that the code is well documented. Reviewers can check for the presence and quality of comments, making sure they accurately and concisely explain the code’s purpose. This makes the codebase easier to understand and reduces future technical debt.
<br><br>

## Steps of a good code review process

### 1. Verify feature requirements
The program needs to reliably perform functions the user expects. If your developer missed this step, postpone the review until the code offers the full range of features. 
To check the feature requirements, ask yourself:
* Does this code accomplish what the end user needs?
* Is there any missing functionality?
* Are there any poorly implemented functions?
* Could they add any related functions the user would like?

### 2. Assess readability
Review the legibility by asking: 
* Can you easily identify the code block starting and ending point?
* Can the lines fit on a standard laptop screen (14 inches) or desktop screen (22-24 inches)?
* Does the code speak for itself and convey its purpose?
* Does it prioritize clarity and brevity?
* Does it avoid obscure language?
* Can you discern the role of specific functions, methods, or classes?
* Did the dev break the code into easy-to-understand chunks?

 ### 3. Test maintainability
 Over time, you may have to expand or change your code, so ensuring it’s easy to maintain and adjust will save you a few headaches. 

Ask yourself these questions to assess maintainability:
* Is the code easy to test and debug?
* Can you configure the code to quickly change data values?
* Is the code tied to another system or an outdated program?
* Does the code rely on functions or technology you want to phase out?

### 4. Check for security vulnerabilities
To avoid security vulnerabilities, ask these questions:
* Does the code use outdated tools or ones with known security problems?
* If you wanted to steal data or access a system, do you see vulnerabilities?
* Does the code leverage authentication and authorization for security?
* Is the user’s input sanitized to prevent security attacks?
* Does the code securely store user data?
* Does the code protect P2 or other GDPR-related data?

### 5. Consider speed and performance
Code reviewers also need to weigh a program’s resource consumption against its speed. Balancing these priorities isn’t always easy, but great code should check off both boxes. 

Ask yourself a few questions to assess speed and performance:
* Does the code contain inefficient string concatenations, logging, or allocations of objects?
* Can you see duplicate code you don’t need?
* Will the program negatively affect system performance overall?
* Does the code rely on poorly optimized assets or multiple API requests?

### 6. Confirm adequate documentation
The best documentation explains what a codebase does and how you can use it. However, even great code may need some external documentation for ease of use. 

To make sure documentation is up to snuff, ask:
* Does the documentation explain the code’s purpose?
* Does the documentation teach the user how to use the code?
* Do any new features or code changes warrant additional documentation?
* Is the documentation clear and well written?

### 7. Inspect naming conventions
Clear naming conventions make it easier to read and understand code. When programmers choose arbitrary or suboptimal names, even great programs become hard for others to understand. 

## Useful Links:
[Understanding the Code Review Process](https://smartbear.com/learn/code-review/guide-to-code-review-process/)<br>
[Code review checklist](https://www.pluralsight.com/blog/software-development/code-review-checklist)
