# Data Structures

## 1. What data structures are

**Data structures** are a way of organising data and providing convenient access to it.

The term **data structure** refers to a collection of elements containing data, as well as relationships between them, and data operations. As a rule, data structures have two types of **operations**: **internal**, supporting data organisation, and **external**, available to users for storing, retrieving, or modifying data. There are several common data structures: an array, a linked list, a hash table, a whole variety of trees (binary search tree, heap, red-black tree, B-tree, etc.)

## 2. The role of data structures

Different data structures have different \*\*\*\*time complexities for performing the same external operations in a set of data. This is why it is essential to consider all the possible structures and choose the most efficient amongst them.

## 3. Abstract data type

There is another term: **abstract data type (ADT)**, which is sometimes used as a synonym for data structures, though this is not entirely correct.

In general, an **Abstract Data Type** is a mathematical concept, a simpler and more abstract way to view the data structure as a whole. It is a data type that is defined by a set of values and a set of possible external operations (behavior) from the user's point of view*.* There are some common ADTs that every trained programmer should know: stack, queue*,* and so on*.* As a rule, modern programming languages like Java, Python, and C++ provide these ADTs in standard libraries so that we can use them in our programs.

## 4. Comparison

Data structures are exact representations of data, but ADTs are different. They reflect the point of view of an implementer, not a user. A data structure is an implementation of an ADT's functions, a way to look more closely at some specific operations and components of the structure. A good example of an abstract data type is an integer. We know what values integers can have and what operations they support (addition, subtraction, multiplication, and so on). At the machine level, they can be represented by a sequence of zeros and ones, but we usually don't care. It is enough for us to know that what we have is an integer, and not, say, a floating-point number. For those who are familiar with OOP, `java.util.Map`, for example, plays the role of an ADT, whereas `HashMap` or `LinkedHashMap` can be interpreted as data structures.

In some sense, an ADT defines the logical form of the data type, while a data structure implements the physical form of it.

## 5. Conclusion

All in all, data structures are a way of organizing data and providing convenient access to it. They have two types of operations: internal and external. There are many types of data structures, each with its own time complexities, features, and limitations. Another closely related concept to keep in mind is an abstract data type. In short, an ADT is a way to view the data structure, seeing its functions and general behavior, whereas the data structure itself is the implementation of these functions.
