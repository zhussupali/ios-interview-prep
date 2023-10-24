## Table Of Contents
* [Algorithms]()
  - [What is Algorithm?](#what-is-algorithm)
  - [Algorithm Complexity](#algorithm-complexity)
    * [Big O notation](#big-o-notation)
    * [Time and Space Complexity](#time-and-space-complexity)
  - [Types of Algorithms](#types-of-algorithms)
    * [1. Brute Force Algorithm](#1-brute-force-algorithm)
    * [2. Recursive Algorithm](#2-recursive-algorithm)
    * [3. Backtracking Algorithm](#3-backtracking-algorithm)
    * [4. Searching Algorithm](#4-searching-algorithm)
      - [Linear Search](#linear-search)
      - [Binary Search](#binary-search)
    * [5. Sorting Algorithm](#5-sorting-algorithm)
      - [Bubble Sort](#bubble-sort)
    * [Other Sorting algorithms](#other-sorting-algorithms)
* [Data Structures](#data-structures)
  - [What is Data Structure?](#what-is-data-structure)
  - [1. Array](#1-array)
  - [2. Set](#2-set)
  - [3. Dictionary](#3-dictionary)
  - [4. Hash Table](#4-hash-table)
  - [5. Stack](#5-stack)
  - [6. Queue](#6-queue)
  - [7. Linked Lists](#7-linked-lists)
  - [8. Graph](#8-graph)
  - [9. Trees](9-trees)

## What is Algorithm
Algorithm is a step-by-step procedure, which defines a set of instructions to be executed in a certain order to get the desired output.

## Algorithm Complexity
Algorithmic complexity is concerned about how fast or slow particular algorithm performs. 
The most common measure of complexity is **time complexity**, which refers to the amount of time an algorithm takes to produce a result as a function of the size of the input. **Space complexity** refers to the amount of memory used by an algorithm.

### Big O notation
Big O notation is a symbolism used in complexity theory, computer science, and mathematics to describe the asymptotic behavior of functions. Basically, it tells you how fast a function grows or declines.

Big O is also known as the algorithm's upper bound since it analyses the worst-case situation.

The best-case scenario usually tells us nothing — we'll possibly solve the problem on the first try. That’s why we employ worst-case scenarios to get meaningful input. It tells us that the algorithm will always perform equal to or better than the worst-case scenario.

Here is a list of classes of functions that are commonly encountered when analyzing algorithms. The slower growing functions are listed first. c is some arbitrary constant.

| Notation  | Name |
| ------------- | ------------- |
| O(1)  | constant  |
| O(log(n))  | logarithmic  |
| O(n)  | linear  |
| O(n^2)  | quadratic  |
| O(n^c)  | polynomial  |

<img width="321" alt="Снимок экрана 2023-10-17 в 20 05 07" src="https://github.com/kdyrovadd/test/assets/103488736/05024693-6bb7-4f3a-b8ac-2ae971d93080">

### Time and Space Complexity
A function's **time complexity** measures how long it takes to execute in terms of computational steps. 
The **space complexity** of a function is determined by the amount of memory it uses.

## Types of Algorithms
There are several types of algorithms available. Some important algorithms are:

### 1. Brute Force Algorithm:
A brute force algorithm is a straightforward approach to problem-solving that involves trying every possible solution until a satisfactory one is found.

**For example**, imagine you have a small padlock with 4 digits, each from 0-9. You forgot your combination, but you don't want to buy another padlock. Since you can't remember any of the digits, you have to use a brute force method to open the lock.

So you set all the numbers back to 0 and try them one by one: 0001, 0002, 0003, and so on until it opens. In the worst case scenario, it would take 104, or 10,000 tries to find your combination.

A classic **example in computer science** is the traveling salesman problem (TSP). Suppose a salesman needs to visit 10 cities across the country. How does one determine the order in which those cities should be visited such that the total distance traveled is minimized?

The brute force solution is simply to calculate the total distance for every possible route and then select the shortest one. This is not particularly efficient because it is possible to eliminate many possible routes through clever algorithms.

**Time complexity:** `O(mn)`(So, if we were to search for a string of "n" characters in a string of "m" characters using brute force, it would take us n * m tries)

### 2. Recursive Algorithm:
A recursive algorithm is based on [recursion](https://www.geeksforgeeks.org/introduction-to-recursion-data-structure-and-algorithm-tutorials/). In this case, a problem is broken into several sub-parts and called the same function again and again.

To build a recursive algorithm, you will break the given problem statement into two parts. The first one is the base case, and the second one is the recursive step.

* Base Case: It is nothing more than the simplest instance of a problem, consisting of a condition that terminates the recursive function. This base case evaluates the result when a given condition is met.
* Recursive Step: It computes the result by making recursive calls to the same function, but with the inputs decreased in size or complexity.

_Difference between iteratiev and recursive method:_ 
<img width="600" alt="Снимок экрана 2023-10-12 в 19 25 16" src="https://github.com/kdyrovadd/test/assets/103488736/f9aa870a-a381-4a5b-ad7b-75732e8a5639">

### 3. Backtracking Algorithm:
Backtracking can be defined as a general algorithmic technique that considers searching every possible combination in order to solve a computational problem.

The term backtracking suggests that if the current solution is not suitable, then backtrack and try other solutions. Thus, recursion is used in this approach.

**Problem**: You want to find all the possible ways of arranging 2 boys and 1 girl on 3 benches. 
Constraint: Girl should not be on the middle bench.

**Solution**: There are a total of 3! = 6 possibilities. We will try all the possibilities and get the possible solutions. We recursively try all the possibilities.

All the possibilities are:<br>
<img width="295" alt="Снимок экрана 2023-10-12 в 20 08 35" src="https://github.com/kdyrovadd/test/assets/103488736/9ce07e10-4b56-45e7-a6c8-1260d59a3e3c">

The following [state space tree](https://www.simplilearn.com/tutorials/data-structure-tutorial/backtracking-algorithm#:~:text=State%2DSpace%20Tree,leaf%20as%20a%20terminal%20state.) shows the possible solutions.<br>
<img width="249" alt="Снимок экрана 2023-10-12 в 20 09 59" src="https://github.com/kdyrovadd/test/assets/103488736/c40b08af-0674-4982-b337-b9f88c05c66a">

### 4. Searching Algorithm:
Searching Algorithms are designed to check for an element or retrieve an element from any data structure where it is stored.

Based on the type of search operation, these algorithms are generally classified into two categories:

1. Sequential Search: In this, the list or array is traversed sequentially and every element is checked. For example: Linear Search.

#### Linear Search

Linear Search is defined as a sequential search algorithm that starts at one end and goes through each element of a list until the desired element is found, otherwise the search continues till the end of the data set.

In Linear Search Algorithm, 

* Every element is considered as a potential match for the key and checked for the same.
* If any element is found equal to the key, the search is successful and the index of that element is returned.
* If no element is found equal to the key, the search yields “No match found”.

<img width="476" alt="Снимок экрана 2023-10-12 в 21 50 27" src="https://github.com/kdyrovadd/test/assets/103488736/4d6ecd82-a3a0-48f3-bd0c-d2a7dc87334f"><br>

Implementation of Linear Search Algorithm(Swift):

```swift
func linearSearch<T: Equatable>(_ array: [T], _ object: T) -> Int? {
  for (index, obj) in array.enumerated() where obj == object {
    return index
  }
  return nil
}
```

Put this code in a playground and test it like so:
```swift
let array = [5, 2, 4, 7]
linearSearch(array, 2)     // This will return 1
```

**Time Complexity**:
* Best Case: `O(1)`
* Average Case: `O(N)`
* Worst Case: `O(N)`<br>

**Space Complexity**: `O(1)`

2. Interval Search: These algorithms are specifically designed for searching in sorted data-structures. These type of searching algorithms are much more efficient than Linear Search as they repeatedly target the center of the search structure and divide the search space in half. For Example: Binary Search.

#### Binary Search

Binary Search is defined as a searching algorithm used in a sorted array by repeatedly dividing the search interval in half. The idea of binary search is to use the information that the array is sorted and reduce the time complexity to O(log N). 

To apply Binary Search algorithm:

* The data structure must be sorted.
* Access to any element of the data structure takes constant time.

In this algorithm, 

1. Divide the search space into two halves by finding the middle index “mid”.
2. Compare the middle element of the search space with the key.
3. If the key is found at middle element, the process is terminated.
4. If the key is not found at middle element, choose which half will be used as the next search space.
   * If the key is smaller than the middle element, then the left side is used for next search.
   * If the key is larger than the middle element, then the right side is used for next search.
7. This process is continued until the key is found or the total search space is exhausted.

<img width="562" alt="Снимок экрана 2023-10-12 в 22 08 38" src="https://github.com/kdyrovadd/test/assets/103488736/c95e11a3-bca3-40ca-bc3c-78a80e415302">

The Binary Search Algorithm can be implemented in the following two ways

* Iterative Binary Search Algorithm
* Recursive Binary Search Algorithm

1. Implementation of Iterative Binary Search(Swift):

```swift
func binarySearchAlgo(arr: [Int], key: Int) -> Int? {

   var LBound = 0
   var UBound = arr.count - 1
    
   while LBound <= UBound {
      let middle = (LBound + UBound) / 2
      if arr[middle] == key {
        
         // Found the key element
         return middle 
      } else if arr[middle] < key {
        
         // Searching in the upper half
         LBound = middle + 1 
      } else {
        
         // Searching in the lower half
         UBound = middle - 1 
      }
   }
    
   // Key element is not found
   return nil 
}
```
2. Implementation of Recursive Binary Search(Swift):

```swift
func recursiveBinarySearch(for value: Int, in items: [Int], left: Int, right: Int) -> Int? {
    var mid = (left + right) / 2

    if left > right {
        return nil
    } else if items[mid] == value {
        return mid
    } else if items[mid] < value {
        return recursiveBinarySearch(for: value, in: items, left: mid + 1, right: right)
    } else {
        return recursiveBinarySearch(for: value, in: items, left: left, right: mid - 1)
    }
}
```

**Time Complexity:**
* Best Case: `O(1)`
* Average Case: `O(log N)`
* Worst Case: `O(log N)`

**Space Complexity:** `O(1)`, If the recursive call stack is considered then the auxiliary space will be `O(logN)`.

### 5. Sorting Algorithm:
A Sorting Algorithm is used to rearrange a given array or list of elements according to a comparison operator on the elements. For example,

<img width="442" alt="Снимок экрана 2023-10-17 в 20 43 21" src="https://github.com/kdyrovadd/test/assets/103488736/1c11a3ca-5aec-4942-9d63-d6a2d2c79de9">

There are various sorting algorithms that can be used to complete this operation. And, we can use any algorithm based on the requirement.

### Bubble Sort

Bubble sort is a sorting algorithm that compares two adjacent elements and swaps them until they are in the intended order.

Just like the movement of air bubbles in the water that rise up to the surface, each element of the array move to the end in each iteration. Therefore, it is called a bubble sort.

**Working of Bubble Sort**

1. First Iteration (Compare and Swap)

* Starting from the first index, compare the first and the second elements.
* If the first element is greater than the second element, they are swapped.
* Now, compare the second and the third elements. Swap them if they are not in order.
* The above process goes on until the last element.

<img width="374" alt="Снимок экрана 2023-10-17 в 20 51 41" src="https://github.com/kdyrovadd/test/assets/103488736/b72f58c6-7c39-4e7c-ad69-cc92ad356289">

2. Remaining Iteration

The same process goes on for the remaining iterations.

After each iteration, the largest element among the unsorted elements is placed at the end.

<img width="360" alt="Снимок экрана 2023-10-17 в 20 52 34" src="https://github.com/kdyrovadd/test/assets/103488736/3a2d8c97-ecf5-4cf1-9dc9-a6fa03c9456b">

In each iteration, the comparison takes place up to the last unsorted element.

<img width="359" alt="Снимок экрана 2023-10-17 в 20 52 58" src="https://github.com/kdyrovadd/test/assets/103488736/f76c3c60-df34-4399-81e3-72741ca015d9">

The array is sorted when all the unsorted elements are placed at their correct positions.

<img width="363" alt="Снимок экрана 2023-10-17 в 20 53 22" src="https://github.com/kdyrovadd/test/assets/103488736/cd9678ad-24e2-44a5-9444-4abd1e270aca">

Implementation in Swift:
```swift
func mBubbleSort(_ array: inout [Int]) {
   let size = array.count
    
   for x in 0..<size {
      for y in 0..<size-x-1 {

         if array[y] > array[y+1] {
            let temp = array[y]
            array[y] = array[y+1]
            array[y+1] = temp
         }
      }
   }
}
```

**Time Complexity:**
* Best Case: `O(n)`
* Average Case: `O(n^2)`
* Worst Case: `O(n^2)`

**Space Complexity:** `O(1)`

### Other Sorting Algorithms:

* [Quicksort](https://www.programiz.com/dsa/quick-sort)
* [Insertion Sort](https://www.programiz.com/dsa/insertion-sort)
* [Merge Sort](https://www.programiz.com/dsa/merge-sort)
* [Selection Sort](https://www.programiz.com/dsa/selection-sort)

## What is Data Structure?
A data structure is a storage that is used to store and organize data. It is a way of arranging data on a computer so that it can be accessed and updated efficiently.
A data structure is not only used for organizing the data. It is also used for processing, retrieving, and storing data. There are different basic and advanced types of data structures that are used in almost every program or software system that has been developed.
<img width="633" alt="Снимок экрана 2023-10-24 в 17 32 37" src="https://github.com/kdyrovadd/test/assets/103488736/f1f45e55-1643-4fbd-b097-130229b02211">

Data structure where data elements are arranged sequentially or linearly where each and every element is attached to its previous and next adjacent is called a **linear data structure**.
Its examples are array, stack, queue, linked list, etc. 

### 1. Array
Array is arguably one of the most commonly used data structures in Swift, and for good reasons. It keeps its elements in sequence, it’s easy to iterate through in a predictable fashion, and it can store any kind of value — from structs, to class instances, to other collections.

For example, here we’re using an array to store a collection of shapes that are placed on a `Canvas` within a drawing app. Then, when asked to render our canvas into an image, we simply iterate through our array in order to draw each element using a `DrawingContext` — like this:
```swift
struct Canvas {
    var shapes: [Shape]

    func render() -> Image {
        let context = DrawingContext()
        shapes.forEach(context.draw)
        return context.makeImage()
    }
}
```

Array Methods:

| Method  | Description |
| ------------- | ------------- |
| append(num)  | adds an element at the end of the array  |
| insert(num, at: i)  | add elements at the specified position of an array  |
| remove(at: i) | remove the last element from an array  |
| removeFirst()  | remove the first element  |
| removeAll() | remove all elements of an array  |
| sort() | sorts array elements |
| shuffle()	| changes the order of array elements |
| contains() | searches for the element in an array |
| swapAt() | exchanges the position of array elements |
| reverse()| reverses the order of array elements |


### 2. Set
A set is a collection of unique data. 

There are two fundamental differences between a set and an array:
* the set provides no defined ordering
* a value can only appear once in a set

We can declare a Set using the following syntax:
```swift
let uniqueNumbers: Set<Int> = [0, 2, 1, 3, 42]
print(uniqueNumbers)
// Output: [42, 2, 0, 1, 3]
```

Set Methods:
| Method  | Description |
| ------------- | ------------- |
| insert(num)  | add the specified element to a set  |
| remove(num)  | remove the specified element from a set  |
| removeFirst()  | remove the first element of a set  |
| removeAll()  | remove all elements of a set  |
| sorted() | sorts set elements |
| forEach() | performs the specified actions on each element |
| contains() | searches the specified element in a set |
| randomElement() | returns a random element from the set |
| firstIndex() | returns the index of the given element |

### 3. Dictionary
Swift dictionary is an unordered collection of items. It stores elements in key/value pairs. Here, keys are unique identifiers that are associated with each value.

Here's how we can create a dictionary in Swift.
```swift
var capitalCity = ["Nepal": "Kathmandu", "Italy": "Rome", "England": "London"]
print(capitalCity)
```

Note: Keys should conform to `Hashable` protocol

Dictionary Methods:
| Method  | Description |
| ------------- | ------------- |
| dict[key] = value  | add elements to a dictionary  |
| dict.keys  | access all the keys from the dictionary  |
| dict.values  | access all the values from the dictionary.  |
| dict.removeValue(forKey: key) | remove an element from the dictionary |
| removeAll() | remove all elements of a dictionary |
| sorted() | sorts dictionary elements |
| shuffled() | changes the order of dictionary elements |
| contains() | checks if the specified element is present |
| randomElement() | returns a random element from the dictionary |
| firstIndex() | returns the index of the specified element |

### 4. Hash Table
A hash table is nothing more than an array. Initially, this array is empty. When you put a value into the hash table under a certain key, it uses that key to calculate an index in the array. The trick is how the hash table calculates those array indices. That is where the hashing comes in. When you write the following statement,
```swift
hashTable["firstName"] = "Steve"
```
the hash table takes the key “firstName” and asks it for its hashValue property. Hence, keys must conform to the `Hashable` protocol.

**Hash functions**<br>
When you write `"firstName".hashValue`, it returns a big integer: `-8378883973431208045`. Likewise, `"hobbies".hashValue` has the hash value `477845223140190530`.
Hash values are calculated by a hash function, which takes some input and returns an integer:

<img width="236" alt="Снимок экрана 2023-10-24 в 21 50 49" src="https://github.com/kdyrovadd/test/assets/103488736/3dc091fc-e922-4055-9a1e-4b39b143479c"><br>

**Collisions**<br>
Collision problems are a common issue when working with hash tables. A collision occurs when two or more keys are mapped to the same index in the hash table, leading to an overlap in the data stored at that index. This can cause the hash table to become inefficient and slow, as it takes longer to retrieve data from the table.
One way to solve collision problems in hash tables is to use a technique called **chaining**. In chaining, each index in the hash table is a linked list, and when a collision occurs, the new key-value pair is added to the end of the list. This allows for multiple key-value pairs to be stored at the same index without causing any overlap.

In iOS development, there is no official corresponding HashTable type. However, in its place, we have the popular Hashable protocol. The idea is that one can extend any type to support _Hash table-like_ functionality. 

Useful links: [Building A Hash Data Structure In Swift](https://medium.com/journey-of-one-thousand-apps/building-a-hash-data-structure-in-swift-e9b2733d9e20) <br>
[What is Hashable in Swift?](https://www.programiz.com/swift-programming/hashable)

### 5. Stack
The data structure follows the rule of LIFO (Last In-First Out) where the data last added element is removed first. Push operation is used for adding an element of data on a stack and the pop operation is used for deleting the data from the stack. This can be explained by the example of books stacked together. In order to access the last book, all the books placed on top of the last book have to be safely removed.

In iOS, some of the things are based on Stack like:
* UINavigationController uses the Stack to push and pop the controllers.
* Memory allocations for local variables are managed by Stack.

Stack functions:
| Function  | Description |
| ------------- | ------------- |
| peek()  | peek at the top-most element in the stack  |
| pop()  | returns the top item from the Stack and then removes it |
| push()  | allow us to add values to the Stack  |

#### How to implement Stack using Swift language?

```swift
import Foundation

struct Stack<T> {
    private var items: [T] = []

    func peek() -> T {
        guard let topElement = self.items.first else { fatalError("This stack is empty.") }
        return topElement
    }
    
    mutating func pop() -> T? {
        if items.isEmpty { return nil }
        return self.items.removeFirst()
    }
  
    mutating func push(_ element: T) {
        self.items.insert(element, at: 0)
    }
}

extension Stack<T>: CustomStringConvertible {
    var description: T {
        let topDivider = "---Stack---\n"
        let bottomDivider = "\n-----------\n"

        let stackElements = array.joined(separator: "\n")

        return topDivider + stackElements + bottomDivider
    }
}
```

### 6. Queue
Similar to a stack, data elements are removed or added at one end only. However, queues follow the first in, first out protocol (FIFO). The last element added to a stack is the element which will be removed first. 

Stack functions:
| Function  | Description |
| ------------- | ------------- |
| peek()  | peek at the top-most element in the Queue  |
| dequeue()  | returns the top item from the Queue and then removes it |
| enqueue()  | allow us to add values to the Queue  |


#### How to implement Queue using Swift language?

```swift
struct Queue<T> {
     var list = [T]()

     mutating func enqueue(_ element: T) {
        list.append(element)
     }

     mutating func dequeue() -> T? {
         if !list.isEmpty {
             return list.removeFirst()
         } else {
             return nil
         }
     }

     func peek() -> T? {
         if !list.isEmpty {
            return list[0]
         } else {
            return nil
         }
     }

     var isEmpty: Bool {
         return list.isEmpty
     }
}
```

### 7. Linked Lists
A Linked List is a list of linked nodes. A node is a single element that contains a generic value and a reference/pointer to the next node. There are a few types of Linked Lists, such as:
* Singly Linked Lists — Each node only has a reference/pointer to the next node. The operations can only travel in one direction.
* Doubly Linked Lists — Each node has two references/pointers, one to the next node and one to the previous node. Operations can travel in both forward and backward directions.
* Circular Linked Lists — The next reference/pointer of the last node points to the first node, and/or the previous reference/pointer of the first node points to the last node.

#### How to implement Linked List using Swift language?(Singly Linked Lists)
First we create a Node class. Remember that each node has a value and a pointer to the next. We will call the pointer next and is a type Node class. We will also make this node a generic and Equtable.
```swift
class Node<T: Equatable> {
  var value: T? = nil
  var next: Node? = nil
}
```

```swift
class LinkedList<T: Equatable> {
  var head = Node<T>()
}
```

**Insert**<br>
<img width="529" alt="Снимок экрана 2023-10-24 в 20 49 21" src="https://github.com/kdyrovadd/test/assets/103488736/19fd3ee0-dc86-4ff7-b0de-8efc20b192e3">

Now that we have set up our Node Class and LinkedList Class, we will now insert a node. This function goes inside our LinkedList Class. Our strategy will be inserting the node at the end of the linked list. We will use these steps to check our insertion:
* Check if the head has an value, if it doesn’t, then the value we insert is the head
* Find the last node of the linked list.
* Connect the last node’s pointer to the new node’s value.

```swift
func insert(value: T) {
  if self.head.value == nil {
    self.head.value = value
  } else {
    var lastNode = self.head
    while lastNode.next != nil {
      lastNode = lastNode.next!
    }

    let newNode = Node<T>()
    newNode.value = value
    lastNode.next = newNode
  }
}
```

**Remove**<br>
<img width="309" alt="Снимок экрана 2023-10-24 в 20 51 04" src="https://github.com/kdyrovadd/test/assets/103488736/c5bc4044-ad91-4930-8890-3259d09fe3eb">

For removal, we have to remove the Node. Create a function that takes in a value to be removed. This function goes inside our LinkedList Class. The steps will be:
* Check if the value to be removed is at the head.
* Traverse the linked list to see if the value is in the linked list.
* Keep track of the previous Node.
* When found, connect the previous node’s next to the next node’s value.

```swift
func remove(value: T) {
  if self.head.value == value {
    self.head = self.head.next!
  }
if self.head.value != nil {
    var node = self.head
    var previousNode = Node<T>()
    while node.value != value && node.next != nil {
      previousNode = node
      node = node.next!
    }
    if node.value == value {
      if node.next != nil {
        previousNode.next = node.next
      } else {
        previousNode.next = nil
      }
    }
  }
}
```


to be continued...
