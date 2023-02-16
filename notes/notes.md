# Java, Algorithms & Data Structures Prep

---

# THEORY:

## Java Notes

### Instance methods

All methods can be divided into two groups: _instance_ and _static_.

#### Summary:

In Java, every method should be declared within a class. The difference between the instance and the static methods lies whether they interact with an object or not. Let's recap:

- static method is associated with the class as a whole;
- instance method can only be invoked through an *instance* of a class, so that you have to create an object first;
- instance methods can access the fields of the class with `this` keyword.

Instance methods allow programmers to manipulate particular objects of a class. And because of it, they give us more functionality and are used more often than static methods!

#### What’s the difference?

```java
class Human {
    String name;
    int age;

		// So if the method has the word **static**, then it is a **static** method.
    public static void printStatic() {
        System.out.println("It's a static method");
    }
		// If the method doesn’t have static in it, then it is an **instance** method.
    public void printInstance() {
        System.out.println("It's an instance method");
    }
}
```

#### Understanding: static and instance

To invoke a **static** method we don’t need to create an object. We just call the method with the class name.

```java
public static void main(String[] args) {

    Human.printStatic(); // will print "It's a static method"
}
```

The **instance** method requires a different invocation. We need to create an object first. Otherwise, there is no way to use an instance method. It’s called the instance method because an instance is a concrete representation of an object.

Here we call the method `printInstance` for two different objects:

```java
public static void main(String[] args) {

    Human peter =  new Human();
    peter.printInstance(); // will print "It's an instance method"

    Human alice =  new Human();
    alice.printInstance(); // will print "It's an instance method"
}
```

So we can that an instance method is a method that belongs to each object that we created of the particular class

#### Instance methods: features

Instance methods have a great advantage: they can access field of the class. (Human class below has been modified)

<aside>
💡 The keyword `this` is optional, so the code will work the same without it. But it's a good practice to add it.

</aside>

```java
class Human {
    String name;
    int age;

    public static void averageWorking() {
        System.out.println("An average human works 40 hours per week.");
    }

    public void work() {
        System.out.println(this.name + " loves working!");
    }
}
```

It’s easier to understand by an example:

```java
public static void main(String[] args) {

    Human.averageWorking(); // "An average human works 40 hours per week."

    Human peter =  new Human();
    peter.name = "Peter";
    peter.work(); // "Peter loves working!"


    Human alice =  new Human();
    alice.name = "Alice";
    alice.work(); // "Alice loves working!"
}
```

### TDD

Most Java exercises include multiple test cases. These cases are structured to support a useful process known as **[test-driven development (TDD)](https://en.wikipedia.org/wiki/Test-driven_development)**. TDD involves repeating a structured cycle that helps programmers build complex functionality piece by piece rather than all at once. That cycle can be described as follows:

1. Add a test that describes one piece of desired functionality your code is currently missing.
2. Run the tests to verify that this newly-added test fails.
3. Update your existing code until:
   - All the old tests continue to pass;
   - The new test also passes.
4. **[Clean up](https://en.wikipedia.org/wiki/Code_refactoring)** your code, making sure that all tests continue to pass. This typically involves renaming variables, removing duplicated chunks of logic, removing leftover logging, etc.
5. Return to step 1 until all desired functionality has been built!

### Interface

An interface is a special kind of class that cannot be instantiated. The main idea of an interface is declaring functionality. Interfaces help to abstract from specific classes and emphasize the functionality. It makes software design more reusable and clean. It is a good practice to apply the so-called interface-oriented design which means that you should rely on interfaces instead of concrete implementations. To implement an interace, the keyword `implements` is used. Opposite to a class, an interface can extend several interfaces. A class can implement multiple interfaces.

To declare an interface you should write the keyword `interface` instead of `class` before the name of the interface:

`interface Interface {}`

An interface can contain:

- public constraints;
- abstract methods without an implementation (the keyword `abstract` is not required here);
- default methods with implementation (the keyword `default` is required);
- static methods with implementation (the keyword `static` is required);
- private methods with implementation

<aside>
💡 If the modifiers are not specified once the method is declared, its parameters will be **public abstract** by default.

</aside>

An interface can’t contain fields (only **constants**), constructors, or non-public abstract methods. Let’s declare an interface containing all possible members:

```java
interface Interface {

    int INT_CONSTANT = 0; // it's a constant, the same as public static final int INT_FIELD = 0

    void instanceMethod1();

    void instanceMethod2();

    static void staticMethod() {
        System.out.println("Interface: static method");
    }

    default void defaultMethod() {
        System.out.println("Interface: default method. It can be overridden");
    }

    private void privateMethod() {
        System.out.println("Interface: private methods in interfaces are acceptable but should have a body");
    }
}
```

The variable `INT_CONSTANT` is not a field here – it's a static final constant. Two methods `instanceMethod1()` and `instanceMethod2()` are abstract methods. The `staticMethod()` is just a regular static method. The default method `defaultMethod()` has an implementation but it can be overridden in subclasses. The `privateMethod` has an implementation as well and can be used to decompose `default` methods.

---

A class can implement an interface using the keyword `implements`. We must provide implementations for all abstract methods of the interface.

Let’s implement the interface we’ve considered earlier:

```java
class ExampleClassImplementation implements Interface {

    @Override
    public void instanceMethod1() {
        System.out.println("Class: instance method1");
    }

    @Override
    public void instanceMethod2() {
        System.out.println("Class: instance method2");
    }
}
```

Now we can create an instance of the class and call its methods:

```java
Interface instance = new Class();

instance.instanceMethod1(); // it prints "Class: instance method1"
instance.instanceMethod2(); // it prints "Class: instance method2"
instance.defaultMethod();   // it prints "Interface: default method. It can be overridden"
```

Note that the `instance` variable has `Interface` type, although it is ok to use `Class`for denoting type.

```java
Class instance = new Class();
```

---

One of the important interface features is **multiple inheriance**.

A class can implement multiple interfaces:

```java
interface A {}
interface B {}
interface C {}

class D implements A, B, C {}
```

An interface can extend one or more other interfaces using the keyword `extends`:

```java
interface A {}
interface B {}
interface C {}

interface E extends A, B, C {}
```

A class can also extend another class and implement multiple interfaces:

```java
class A {}

interface B {}
interface C {}

class D extends A implements B, C {}
```

All the examples above do not pose any problems.

Multiple inheritance of interfaces is often used in the Java standard class library. The class String, for example, implements three interfaces at once:

```java
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence {
// ...
}
```

---

In some situations, an interface can have no members at all. Such interfaces are called **marker** or **tagged interfaces**. For example, a well-known interface `Serializable` is a marker interface:

```java
public interface Serializable {
}
```

Other examples of marker interfaces are `Cloneable`, `Remote`, etc. They are used to provide essential information to the JVM.

---

You can declare and implement a static method in an interface

```java
interface Car {
	static float covertToMilesPerHour(float kmh) {
		return 0.62 * kmh;
	}
}
```

To use a static method you just need to invoke it directly from an interface

```java
Car.convertToMilesPerHour(4.5);
```

The main purpose of interface static methods is defining utility functionality that is common for all classes implementing the interface. They help to avoid code duplication and creating additional utility classes.

---

### Inheritance

#### 1. Extending classes

**Inheritance** is a mechanism for deriving a new class from another base class. The new class acquires some fields and methods of the base class. Inheritance is one of the main principles of object-oriented programming. It allows developer to build convenient class hierarchies and reuse existing code.

When it comes to inheritance, there are several terms. A class **derived** from another class is called a **subclass** (it’s also known as a **deriver class**, **extended class** or **child class**). The class from which the subclass is derived is called a **superclass** (a.k.a **base** or **parent class**).

To derive a new class from another the keyword `extends` is used. The common syntax is shown below.

```java
class SuperClass { }

class SubClassA extends SuperClass { }

class SubClassB extends SuperClass { }

class SubClassC extends SubClassA { }
```

There are important points about inheritance in Java:

- Java doesn’t support multiple-class inheritance meaning that a class can only inherit from a single superclass;
- a class hierarchy can have multiple levels (class C can extend class B that extends class A);
- a superclass can have more than one subclass.

A subclass inherits all public and **protected** fields and methods from the superclass. A subclass can also add new fields and methods. The inherited and added members will be used in the same way.

A subclass **doesn’t** inherit **private** fields and **methods** from the superclass. However, if they superclass has public or protected methods for accessing its private fields, these members can be used inside subclasses.

Constructors are not inherited, but the superclass’ constructor can be invoked from the subclass using the special keyword `super`. (see example below)

If you’d like the base class members to be accessible from all subclasses but not from the outside code (excluding the same package), use the access modifier `protected`.

#### 2. Example

Class hierarchy diagram

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled.png)

```java
class Person {
    protected String name;
    protected int yearOfBirth;
    protected String address;

    // public getters and setters for all fields here
}

class Client extends Person {
    protected String contractNumber;
    protected boolean gold;

    // public getters and setters for all fields here
}

class Employee extends Person {
    protected Date startDate;
    protected Long salary;

    // public getters and setters for all fields here
}

class Programmer extends Employee {
    protected String[] programmingLanguages;

    public String[] getProgrammingLanguages() {
        return programmingLanguages;
    }

    public void setProgrammingLanguages(String[] programmingLanguages) {
        this.programmingLanguages = programmingLanguages;
    }
}

class Manager extends Employee {
    protected boolean smile;

    public boolean isSmile() {
        return smile;
    }

    public void setSmile(boolean smile) {
        this.smile = smile;
    }
}
```

**Inheritance** provides a powerful mechanism for code reuse and writing convenient hierarchies. Many things of the real world can be simulated like hierarchies from a more general to a more particular concept,

#### 3. Final classes

If a class is declared with the keyword `final`, it cannot have subclasses at all.

```java
final class SuperClass { }
```

If you try to extend the class, a compile-time error will occur.

Some standard classes are declared as final: `Integer`, `Long`, `String`, `Math`. They cannot be extended.

#### 4. Conclusion

**Inheritance** allows you to build class hierarchies when subclasses (children) take some fields and methods of the superclass(parent). Such a hierarchy can have multiple levels, but every class can inherit only a single superclass. A good class hierarchy helps to avoid code duplication and make your program more modular. If a class should not have subclasses, it should be marked as `final`.

### The big O notation

We use this to estimate the efficiency of an algorithm.

#### 1. Input size

The running time of an algorithm depends on the **input data**. Naturally, the program will take a different time to proceed with 10 or 1,000,000 numbers. We will use the term **input size** as a proxy measure of the size of input data. If you need to work with **m** numbers, then **m** is the input size. The input size isn’t always the amount of the input data itself. If you need to find the first $n$ prime numbers, then searching for the 10 first primes or 10,000 first primes will also take a different time, however, you only enter a single number $n$ as input. In such cases, that number’s value is typically considered the input size.

If we can estimate how the number of operations depends on the input size, we will have a machine-independent measure of algorithm complexity. If we want to find a good algorithm, we are mostly interested in its behaviour with big data. For this, we can compare the behaviour of the algorithm’s running time with some standard functions.

#### 2. Big O notation

Less formally, we can say that an algorithm has the **time complexity** $O(f(n))$ if its number of operations grows bigger similar to (or slower than) the function $f(n)$ when the input size $n$ is a larger number. In order to avoid unnecessary abstractness, let’s consider the following task: given a $n$ x $n$ table with integers in its cell. Find the number $k$ in the given table.

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%201.png)

Alice and Bob have come up with their own algorithms to solve the problem. Bob's algorithm consists in scanning every cell of the table and checking if the corresponding value is equal to $k$. Well, this implies a maximum of $n^2$ comparisons, which means that the time complexity of Bob's algorithm is $O(n^2)$. On the other hand, Alice somehow knows earlier in which column the number $k$ will be located, hence, she only needs to scan the elements of that column. A column consists of $n$ cells, meaning that Alice's algorithm will take $O(n)$ time.

Basically, on a table $2$ x $2$, Bob will have to perform a maximum of $4$ operations; meanwhile, Alice will perform no more than $2$. Not a big difference really, is it? What if we have a table $*n$* × $*n\*$ for a large $n$? In this case, $n^2$ will be considerably bigger than $n$, as shown below. This is exactly what determines the efficiency of an algorithm – the way it behaves with large input sizes. Hence, we conclude that Alice's algorithm is faster than Bob's, as the big O notation suggests.

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%202.png)

However, a simple question arises: why can't we write simply $n^2$ or $n$ for the complexities? Why do we need to add this beautiful round letter in front of these functions? Well, imagine that the element $k$ is placed in the first cell of the table. Bob will find it immediately and terminate his algorithm. How many steps does he perform: $n^2$? No, just one.

That is why we use the big O: roughly speaking, it describes the upper bound for the function's growth rate. This is one of the big O notation's essential advantages. It means that you can calculate how much time to allocate for processing a certain amount of input data and be sure that the algorithm will process it all in due time. In practice, an algorithm might sometimes work even better than what the big O notation shows for its complexity, but not worse.

#### 3. Common growth rates

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%203.png)

Below are, from best to worst, some common values of the big O function for the time complexity, also known as complexity classes.

- $O(1)$ (**constant time**). \*\*\*\*The algorithm performs a constant number of operations. Maybe one, two, twenty-six or two hundred - it doesn’t matter. What is important is that it doesn’t depend on the input size. Typical algorithms of this class include calculating the answer using a direct formula, printing a couple of values, all letters of the English alphabet, etc.
- $O(log$ $n)$ (**logarithmic time**). We usually refer to logarithms of base 2; however, the base does not affect the class. By definition, $log_2$ $n$ equals the number of times $n$ must be divided by $2$ to get $1$. That being said, it should not be difficult to guess that such algorithms divide the input size into **halves** at each step. They are relatively fast: if the size of the input is huge, say $2^{31}$, the algorithm will perform approximately $log_2 (2^{31})$ $=$ $31$ operations, which is pretty effective.
- $O(n)$ (**linear time**). This time is proportional to the input size, i.e., the time grows linearly as the input size increases. Often, such algorithms are iterated only once. They occur quite frequently, because it is usually necessary to go through every input element before calculating the final answer. This makes $O(n)$ class one of the most effective classes in practice.
- $O(n^2)$ (**quadratic time**). Normally, such algorithms go through all pairs of input elements. Why? Well, mathematics is generous, it constantly provides us with important results: in this case, basic maths confirms that the number of unordered pairs is a set of $n$ elements is equal to ${n(n-1)}/2$, which is $O(n^2)$. **Quadratic time algorithms usually contain nested loops.**
- $O(2^n)$ (**exponential time**). Maths states that the number of subsets of a set of $n$ elements is equal to $2^n$, therefore, it is reasonable to expect that such algorithms scan all the subsets of the input elements. It is worth noting that this class is extremely inefficient in practice; even for small input sizes, the time taken by the algorithm will be remarkably high.

There are also other less common complexity classes, which you will come across in some following topics:

- $O(\sqrt n)$ (**square root time**);
- $O(n \log n)$ (**log-linear time**);
- $O(n^k$) (**polynomial time**);
- $O(n!)$ (**factorial time)**.

#### 4. Calculating complexity

to be able to calculate complexities by yourself, it is essential for you to get familiar with the basic properties of the Big O:

- **Ignore the constants.** As we discussed above, while calculating complexities, we focus solely on the behaviour of our algorithm with large input sizes. Therefore, repeating some steps a constant number of times does not affect the complexity. For example, if you traverse $n$ elements $5$ times, we say that the algorithm's time complexity is $*O(n)*$, and not $*O(5n)*$. Indeed, there is no significant difference between 1,000,000,000 and 5,000,000,000 operations performed by the algorithm. In either case, we conclude that it is relatively slow. Formally, we write $c \cdot O(n)=O(n)$. It is similar for the rest of the complexity classes.
- **Applying a procedure $n$ times.** What if you need to go over $n$ elements $n$ times? It is not a constant anymore, as it depends on the input size. In this case, the time complexity becomes $O(n^2)$. It's simple: you do $n$ times an action proportional to $n$, which means the result is proportional to $n^2$. In big O notation, we write it as $n\cdot O(n) = O(n^2)$.
- **Smaller terms do not matter.** Another common case is when after doing some actions, you need to do something else. For instance, you traverse $*n*$ elements $*n*$ times and then traverse $*n*$ elements again. In this case, the complexity is still $*O(n^2)*$. Additional $*n*$ actions do not affect your complexity, which is proportional to $*n^2*$. In big O notation, it looks like this: $*O(n)+O(n^2)=O(n^2)*$. All in all, always keep the largest term in Big O and forget about all others. It is rather easy to understand which terms are larger based on the order provided in the previous section.

#### 5. Conclusion

Big O notation is an essential instrument for algorithm performance evaluation. We can use it to assess both the time and the memory complexity. The greatest advantage of big O notation is that it classifies an algorithm rather than gives you a real running time in seconds or required memory in megabytes.

[Data Structures](./data-structures.md)

### Objects

#### 1. Creating objects

The keyword **new** creates an object of a particular class. Here we create a standard string and assign it to the variable **`str`**:

```java
String str = new String("hello");
```

The variable **`str`** stores a reference to the object **"hello"** located somewhere in the heap memory.

In the same way, we can create an object of any class we know.

Here is a class that describes a patient in a hospital information system:

```java
class Patient {
    String name;
    int age;
}
```

Here is an instance of this class:

```java
Patient patient = new Patient();
```

Despite the fact that **`String`** is a standard class and **`Patient`** is our own class, both classes are regular reference types. However, there is a big difference between those classes and we will discuss it below.

#### 2. Immutability of objects

There is an important concept in programming called **immutability**. Immutability means that an object always stores the same values. If we need to modify these values, we should create a new object. The common example is the standard **`String`** class. Strings are immutable objects so all string operations produce a new string. Immutable types allow you to write programs with fewer errors.

The class **`Patient`** is not immutable because it is possible to change any field of an object.

```java
Patient patient = new Patient();

patient.name = "Mary";
patient.name = "Alice";
```

In the following topics, we will look at the existing immutable classes as well as learn how to create new ones and when to use them.

#### 3. Sharing references

More than one variable can refer to the same object.

```java
Patient patient = new Patient();

patient.name = "Mary";
patient.age = 24;

System.out.println(patient.name + " " + patient.age); // Mary 24

Patient p = patient;

System.out.println(p.name + " " + p.age); // Mary 24
```

It is important to understand that two variables refer to the same data in memory rather than two independent copies. Since our class is mutable, we can modify the object using both references.

```java
patient.age = 25;
System.out.println(p.age); // 25
```

#### 4. Nullability

As for any reference types, a variable of class type can be **null** which means it is not initialized yet.

```java
Patient patient = null;
```

This is a common feature in Java available for classes since they are reference types.

#### 5. Conclusion

By now, not only have we already worked with some classes from the standard library but also learned how Java allows us to create our own classes. In this topic, we've discussed that the nature of custom classes' objects and standard library ones are based on the same principles.

Keep in mind, that classes defined by programmers are **reference types**. When objects are created by the **new** operator it returns reference in memory where the created objects are located. By this reference, we can get access to its fields and change them. Several variables can refer to the same object through a reference. It is also possible to create two independent objects with the same field's content. It's important to understand that references to such objects are different. However, not all objects allow changing its state after creation. Such a feature is called **immutability**.

### The Object Class

#### 1. The root class in Java

**_The Java Standard Library_** has a class named `Object` that is the default parent of all standard classes and your custom classes. Every class extends this one implicitly, therefore it’s a root of inheritance in Java programs. The class belongs to the `java.lang` package that is imported by default.

Let’s create an instance of the `Object` class.

```java
Object anObject = new Object();
```

The `Object` class can refer to an instance of any class because any instance is a kind of an `Object` (upcasting).

```java
Long number = 1_000_000L;
Object obj1 = number; // an instance of Long can be cast to Object

String str = "str";
Object obj2 = str; // the same with the instance of String
```

When we declare a class, we can explicitly extend the `Object` class. However, there is no point, since the extension is already done implicitly.

#### 2. Methods provided by the Object class

The `Object` class provides some common methods to all subclasses. It has nine instance methods (excluding overloaded methods) which can be divided into four groups:

- _threads synchronisation_: `wait`, `notify`, `notifyAll`;
- _object identity_: `hashCode`, `equals`;
- _object management_: `finalize`, `clone`, `getClass`;
- _human-readable representation_: `toString`;

This way of grouping methods isn’t perfect, but it can help you remember them. Here’s a more detailed explanation of the methods:

- The first group of methods (`wait`, `notify`, `notifyAll`) are for working in multithreaded (google this pls) applications.
- `hashCode` returns a hash code value for the object.
- `equals` indicates whether some other object is “**equal to**” this particular one.
- `finalize` is called by the garbage collector (GC) on an object when the GC wants to clean it up. (**Note**: this method has been deprecated as of JDK 9).
- `clone` creates and returns a copy of the object.
- `getClass` returns an instance of `Class`, which has information about the runtime class.
- `toString` returns a string representation of the object.

Some of the methods listed above are native, which means that they are implemented in the **native** code. It is typically written in C or C++. Native methods are usually used to interface with system calls or libraries written in other programming languages.

#### 3. Conclusion

The `Object` class is a default class in the `java.lang package` and it is a root of inheritance in Java programs. Every instance of any class is a kind of `Object` so there is no need to explicitly extend it when declaring a class. It provides some common methods to all subclasses, including nine instanace methods that are divided into four groups in the present topic. Some of these methods are native so you can use them to interface with system calls or other programming language libraries.

### Computer algorithms

An **algorithm** is a step-by-step sequence of actions you need to perform to achieve the desired result. It can be an algorithm for cooking a sandwich described by a recipe or an algorithm for getting dressed according to today’s weather and your mood.

Among all algorithms, there is one special group called **computer algorithms**. They are usually created for and utilised by computers.

#### 1. Computer Algorithms

An important difference between real-life and computer algorithms is that a computer cannot guess what we intend to do. If something goes wrong or an algorithm is not clear, a human can adjust the algorithm based on their experience. Computers cannot do the same.

If we realise that we’re out of bread, a human would think of going to the store and buying some more. On the other hand, a computer would report the absence of such an ingredient or proceed with its work without noticing that, which would result in incorrect output. Thus, it is our responsibility to describe a computer algorithm precisely and unambiguosly.

#### 2. Programs and algorithms

A program is a sequence of instructions to perform some tasks on a computer. The difference between programs and algorithms is that programs are written using a specific programming language while algorithms are usually described at a higher level than programming statements. In other words, an algorithm is like an abstract schema, and a program can be its implementation. This means you can implement one algorithm in different programming languages.

#### 3. Summary

An algorithm is a sequence of actions you need to perform to achieve a certain result. An important group of algorithms is computer algorithms: the ones created for computers and utilised by them. There are several reasons why it is essential to learn computer algorithms:

- Software developers often encounter tasks of the same type while working on different projects. For such typical tasks, programming languages provide ready-to-use algorithms in standard libraries. To utilise these algorithms efficiently, you need to understand how they work under the hood;
- There are numerous well-known algorithms that cannot be found as ready-to-use functions from libraries. Sometimes you may even encounter problems that are impossible to solve using well-known algorithms. In both cases, you need to implement a suitable algorithm yourself. To be able to do that, you need to know basic algorithm approaches, their pros and cons, and which one to apply in a particular case;
- Often you need not only to write the code yourself, but also to read the code written by other developers. If you want to understand the algorithms they might be likely to use, you need to know basic algorithms and algorithmic approaches as well;
- Implementing algorithms will help you improve your programming skills.

### Algorithms

**What are algorithms?** Steps you take to manipulate data

**Data Structures**: The way data is arranged in memory

**Main Data Structure Operations:** Inserting, Deleting, Searching

### Multi-threading

#### 1. What are the benefits of using Multithreading?

There are various benefits of multithreading as given below:

- Allow the program to run continuously even if a part of it is blocked.
- Improve performance as compared to traditional parallel programs that use multiple processes.
- Allows to write effective programs that utilise maximum CPU time.
- Improves the responsiveness of complex applications or programs.
- Increase use of CPU resources and reduce costs of maintenance.
- Saves time and parallelism tasks.
- If an exception occurs in a single thread, it will not affect other threads as threads are independent.
- Less recourse-intensive than executing multiple processes at the same time.

---

---

---

### Complexities

#### **Queue**

##### Time Complexities:

###### These are the Big O Notations for the various data structures you may come across and use in Java

**Access:** $`O(n)`$

**Insertion:** $`O(1)`$

**Deletion:** $`O(1)`$

---

##### Space Complexities:

A **queue** typically has a space complexity of $`O(1)`$ as its size is bounded by a constant (5000).

#### HashTable (HashMap has the same time complexity)

##### Time Complexities:

**Worst Case:** $`O(n)`$

**Best Case:** $`O(1)`$

---

##### Space Complexities:

A **hashtable** typically has a space complexity of $`O(n)`$

---

#### Arrays

##### Time Complexities:

**Access:** $`O(1)`$

**Insertion:** $`O(n)`$

**Deletion:** $`O(n)`$

---

##### Space Complexities:

An **array** typically has a space complexity of $`O(n)`$ for 1D arrays, and then $`O(n^2)`$ for 2D arrays, etc.

#### Binary Trees

##### Time Complexities:

Time complexity is generally $`O(h)`$ where h is the height of the tree

Worst Case(skewed)**:** $`O(n)`$

Best Case(balanced)**:** $`O(\log n)`$

---

#### Linked List

##### Time Complexities:

**Access:** $`O(n)`$

**Insertion:** $`O(1)`$

**Deletion:** $`O(1)`$

---

##### Space Complexities:

A **linked list** typically has a space complexity of $`O(n)`$

#### Stacks

##### Time Complexities:

Pop**:**$`O(1)`$

Push**:**$`O(1)`$

---

##### Space Complexities:

A **stack** typically has a space complexity of $`O(n)`$

---

### Difference between ArrayList, LinkedList and Vectors

**ArrayList:** it’s a dynamic array that is initialised by size, faster than LinkedList for .get() $O(1)$

**LinkedList:** better performance on add and remove, but worse on get and set methods

**Vector**: similar to ArrayList except that it is synchronized (NOTE - Vectors are not used now. They are old and inefficient in lots of areas).

### Multithreading and how to implement it in Java and what packages to use

Multithreading is the ability to execute multiple different paths of code at the same time.

Normally only using one thread.

When you break into multiple threads, there’s no guarantee which thread will execute first if they’re running concurrently.

If one thread throws an exception, it doesn’t impact the other threads.

---

Two main ways of this in Java: (better to implement the Runnable interface generally, as you can’t have multiple inheritance for a class)

first way is having a class extending the Thread class (below)

second way is having the class implement the Runnable interface, only difference being that you can’t use .start(), instead you have to use `Thread myThread = new Thread(myThing);` and then do `myThread.start();`

- **Code**

  ```java
  public class Multithreading {

  	public static void main(String[] args) {
  		// creating 5 threads using a for loop
  		for(int i = 0; i < 5; i++) {
  			MultithreadThing myThing = new MultithreadThing(i);
  			myThing.start();
  		}

  		MultithreadThing myThing = new MultithreadThing();
  		MultithreadThing myThing2 = new MultithreadThing();
  		// to kick off a new thread, we need to use .start() rather than .run()
  		// this will have the two items below running in parallel
  		myThing.start();
  		myThing2.start();

  	}

  }

  public class MultithreadThing extends Thread {
  	int threadNumber;
  	// allows you to assign a thread number to each thread
  	public MultithreadThing (int threadNumber) {
  		this.threadNumber = threadNumber;
  	}

  	// whatever code you need to run in multiple thread needs to be written in the method below
  	@Override
  	public voic run(){
  		for(int i = 1; i <= 5; i++) {
  			System.out.println(i + " from thread: " + threadNumber);
  			Thread.sleep(1000); // has the thread "sleep" for 1000 miliseconds between each print
  		}
  	}
  }
  ```

---

### Depth First Search (for graphs)

Depth-first search is an algorithm for traversing or searching tree or graph data structures. The algorithm starts at the root node (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking.

So the basic idea is to start from the root or any arbitrary node and mark the node and move to the adjacent unmarked node and continue this loop until there is no unmarked node. Then backtrack and check for other unmarked nodes and traverse them. Finally print the nodes in the path.

**Algorithm: 1.** Create a recursive function that takes the index of the node and a visited array. 2. Mark the current node as visited and print the node 3. Traverse all the adjacent and unmarked nodes and call the recursive function with the index of the adjacent node.
(_for a disconnected graph)_ 4. Run a loop from 0 to the number of vertices and check if the node is unvisited in the previous DFS, call the recursive function with the current node.

**Complexity Analysis:
Time complexity:** $`O(V+E)`$, where V is the number of vertices and E is the number of edges in the graph
**Space complexity:** $`O(V)`$, since an extra visited array of size V is required.

### Tree Traversals

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%204.png)

**Depth First Traversals:**
(a) Inorder (Left, Root, Right): 4 2 5 1 3
(b) Preorder (Root, Left, Right): 1 2 4 5 3
(c) Postorder (Left, Right, Root): 45231
(d) Breadth-Frist or Level Order Traversal: 1 2 3 4 5

**Algorithm Inorder:**

1. Traverse the left subtree, i.e., call Inorder(left-subtree)
2. Visit the root
3. Traverse the right subtree, i.e., call Inorder(right-subtree)

**Algorithm Preorder:**

1. Visit the root
2. Traverse the left subtree, i.e., call Preorder(left-subtree)
3. Traverse the right subtree, i.e., call Preoder(right-subtree)

**Algorithm Postorder:**

1. Traverse the left subtree, i.e., call Postorder(left-subtree)
2. Traverse the right subtree, i.e., call Postorder(right-subtree)
3. Visit the root

### How a HashMap is made at the fundamental level, and what the time complexities are

HashMap put and get operatiion time complexity is O(1) with assumption that key-value pairs are well distributed across the buckets. Meaning hashcode implementation is good.

HashMap contains an array of Node, and Node is an object represented by:

```java
int hash;
K key;
V value;
Node next;
```

Hashing: converting an object into integer form by using the method hashCode()

Bucket: one element of the HashMap array used for storing nodes. One bucket can have two or more nodes, which are then connected by a link list structure.

Steps for inserting entry into HashMap:

1. Calculate the hashCode of the Key
2. Calculate the index by using index method
3. Create a node object with the required values filled out

If there is already an object at the index:

1. Place this object at index 6 if no other object is presented there.
2. In this case a node object is **found at the index 6** – this is a case of collision.
3. In that case, check via hashCode() and equals() method that if both the keys are same.
4. If keys are same, replace the value with current value.
5. Otherwise connect this node object to the previous node object via linked list and both are stored at index 6.

Steps for fetching data:

1. Calculate hash code of Key
2. Calculate index by using index method
3. Go to the index of array and compare first element’s key with given key. If both are equals then return the value, otherwise check for next element if it exists.

### Compare HashMaps, LinkedHashMaps, TreeMaps

**HashMaps**: basic implementation of the Map interface. Stores data in (key, value) pairs amd upi cam access them using the key. Doesn’t maintain the order it’s implemented in. HashMap provided the advantage of quick insertion, search, and deletion.

---

**LinkedHashMaps**: Extends HashMaps, so has all the same features as HashMaps except it maintains insertion order.

---

**TreeMaps:** (not an implementation of HashMap) when you enter elements into the map, they will naturally be sorted/ordered (if keys are integers, then all entries will be sorted as integers are, lowest to highest; alphabets/strings are sorted alphabetically). If a custom class is used as a key, then you have to manually implement the sorting.

### Search algorithms

Searching Algorithms are designed to check for an element or retrieve an element from any data structure where it is stored.

---

**Linear Search**: start from the beginning element of an array, checking equivalency all the way through the array until it matches whatever we’re looking for. The time complexity of the algorithm is $`O(n)`$

- **Linear Search code**

  ```java
  public static void search(int arr[], int search_Element) {
  	int left = 0;
  	int length = arr.length;
  	int right = length - 1;
  	int position = -1;

  	// run loop from 0 to right
  	for (left = 0; left <= right;) {

  		// if search_element is found with left variable
  		if (arr[left] == search_Element) {
  			position = left;
  			System.out.println(
  				"Element found in Array at "
  				+ (position + 1) + " Position with "
  				+ (left + 1) + " Attempt");
  			break;
  		}

  		// if search_element is found with right variable
  		if (arr[right] == search_Element) {
  			position = right;
  			System.out.println(
  				"Element found in Array at "
  				+ (position + 1) + " Position with "
  				+ (length - right) + " Attempt");
  			break;
  		}

  		left++;
  		right--;
  	}

  	// if element not found
  	if (position == -1){
  		System.out.println("Not found in Array with "
  			+ left + " Attempt");
  	}
  }
  ```

---

**Binary Search**: they only work on sorted lists. A binary search will cut the list in half after every iteration in which it doesn’t find its target
Except in unusual circumstances, a binary search won’t need to check all entries

- **Binary Search code**

  ```java
  public static int binSearch(int[] list, int target){
  	int left = 0;
  	int right = list.length - 1;

  	while(left <= right) {
  		int middle = (left + right) / 2;

  		if(target < list[middle) { // too high
  			right = middle - 1;
  		}
  		else if(target > list[middle]) { // too low
  			left = middle + 1;
  		}
  		else { // just right
  			return middle;
  		}
  	}

  	return -1;
  }
  ```

---

### Sorting algorithms

Algorithms used to sort an array of numbers.

---

**Selection Sort:** sorts an array by repeatedly finding the minimum element from the unsorted counterpart and putting it at the beginning. The time complexity is $O(n^2)$ as there are two nested loops within the code

- **Selection Sort code**
  ```java
  void sort(int arr[]){
     int n = arr.length;
     // One by one move boundary of unsorted subarray
     for (int i = 0; i < n-1; i++){
        // Find the minimum element in unsorted array
        int min_idx = i;
        for (int j = i+1; j < n; j++) {
           if (arr[j] < arr[min_idx]){
              min_idx = j;
           }
  			}
        // Swap the found minimum element with the first
        // element
        int temp = arr[min_idx];
        arr[min_idx] = arr[i];
        arr[i] = temp;
     }
  }
  ```

---

**Bubble Sort:** works way through the array and sorts the number in the right order as it goes through (if the left number is greater than the right number, they are swapped). The time complexity can be from $O(n^2)$ (if the array is reverse sorted) or $O(n)$ if the array is already sorted

- **Bubble Sort code**
  ```java
  void bubbleSort(int arr[]) {
     int n = arr.length;
     for (int i = 0; i < n-1; i++){
        for (int j = 0; j < n-i-1; j++) {
           if (arr[j] > arr[j+1]){
              // swap arr[j+1] and arr[j]
              int temp = arr[j];
              arr[j] = arr[j+1];
              arr[j+1] = temp;
           }
        }
     }
  }
  ```

---

**Insertion Sort:** walks through an array, ([0] → [n]) and if the current element is smaller than the element to it’s left, it gets inserted into that position and the larger element get’s inserted on the current element’s position. The time complexity is $O(n^2)$

- **Insertion Sort code**

  ```java
  void insertionSort(int[] inputArray) {
  	for(int i = 1; i < inputArray.length; i++) {
  		int currentValue = inputArray[i];

  		int j = i-1;
  		while(j >= 0 && inputArray[j] > currentValue) {
  			inputArray[j+1] = inputArray[j];
  			j--;
  		}
  		inputArray[j + 1] = currentValue;
  	}
  }
  ```

---

**Quick Sort:** The time complexity is $O(n^2)$ (worst case) or $O(n \log n)$ (best case)

1. choose one of the numbers in your array as the pivot (can be random, but will choose the last element to be the pivot)
2. Partition: move all numbers lower than the pivot to the left, and all numbers higher than the pivot to the right; the pivot is now in its correct spot within the array
3. Recursively quicksort all the elements to the left and right of the pivot

- **Quick Sort code**

  ```java
  public static void quicksort(int[] array, int lowIndex, int highIndex) {

      // logic to return if it's trying to quicksort an array of one index
      if (lowIndex >= highIndex) {
          return;
      }

      int pivot = array[highIndex];

      // PARTITIONING
      // left pointer needs to be pointed at something greater than the pivot
      // right pointer needs to be pointed at something smaller than the pivot
      int leftPointer = lowIndex;
      int rightPointer = highIndex;

      // when the left pointer runs into the right pointer, the loop will end
      while(leftPointer < rightPointer) {

          // walking the pointer from the left side to the right
          while(array[leftPointer] <= pivot && leftPointer < rightPointer) {
              leftPointer++;
          }

          // walking the pointer from the right side to the left
          while(array[rightPointer] >= pivot && leftPointer < rightPointer) {
              rightPointer--;
          }

          swap(array, leftPointer, rightPointer);

      }

      // to swap the left pointer and the pivot to create the partition
      swap(array, leftPointer, highIndex);

      // recursive call to the left of the pivot
      quicksort(array, lowIndex, leftPointer - 1);
      // recursive call to the right of the pivot
      quicksort(array, leftPointer + 1, highIndex);

  }

  private static void swap(int[] arr, int index1, int index2) {
      int temp = arr[index1];
      arr[index1] = arr[index2];
      arr[index2] = temp;
  }
  ```

##### Quick sort is better for arrays: quick sort in its general form is an in-place sort whereas merge sort requires O(N) extra storage

---

**Merge Sort:** The time complexity is always $O(n \log n)$

1. Find the middle point to divide the array into two halves
2. Call mergeSort for first half & second half (unless the input length of array is less than 2, then it has already been sorted (has length 1) or is an empty array)
3. Merge the two halves which have been sorted
   1. done by comparison

- **Merge Sort code**

  ```java
  public static void mergeSort(int[] inputArr) {
      int inputLength = inputArr.length;

      // accounts for when the array's been broken down to a single entry/is empty
      if(inputLength < 2) {
          return;
      }

      int midIndex = inputLength / 2;
      int[] leftHalf = new int[midIndex];
      int[] rightHalf = new int[inputLength - midIndex];

      // filling up the left half of the array
      for(int i = 0; i < midIndex; i++) {
          leftHalf[i] = inputArr[i];
      }
      // filling up the right half of the array
      for(int i = midIndex; i < inputLength; i++) {
          rightHalf[i - midIndex] = inputArr[i];
      }

      mergeSort(leftHalf);
      mergeSort(rightHalf);

      // need to merge these two arrays into a sorted array
      merge(inputArr, leftHalf, rightHalf);
  }

  private static void merge(int[] inputArr, int[] leftArr, int[] rightArr) {
      int leftSize = leftArr.length;
      int rightSize = rightArr.length;

      // i - iterator for right half; j - iterator for left half; k - iterator for main array
      int i = 0, j = 0, k = 0;

      // looping till we run out of elements in the left array & the right array
      while(i < leftSize && j < rightSize) {
          if(leftArr[i] <= rightArr[j]) {
              inputArr[k] = leftArr[i];
              i++;
          }
          else {
              inputArr[k] = rightArr[j];
              j++;
          }
          k++;
      }

      // to add any leftover entries in the left array
      while(i < leftSize) {
          inputArr[k] = leftArr[i];
          i++;
          k++;
      }
      // to add any leftover entries from the right array
      while(j < rightSize) {
          inputArr[k] = rightArr[j];
          j++;
          k++;
      }
  }
  ```

##### Merge sort is better for linked lists: to do with memory allocation as it requires O(N) extra storage and linked lists are more memory efficient as we can insert items into the middle of arrays by just changing the pointers

---

---

---

### Questions: Arrays

- **What is an array?**
  An **array** is a collection of **homogeneous** (same type) data items stored in **contiguous memory** locations. The elements of an array are accessed by using an **index**.

---

- **Name some characteristics of Array Data Structure**
  Arrays are:
  - **Finite (fixed size)** - An array is finite because it contains only limited number of elements
  - **Order** - All the elements are stored one by one in a linear order
  - **Homogenous** - All the elements of an array are of the same data type
  - **Duplicates** - Arrays can contain duplicate entries (compared to sets which don't guarentee order, but also don't allow duplicate entries!)

---

- **What are dynamic arrays?**
  A **dynamic array** is an array which resizes automatically as you add elements.

---

- **What is the main difference between an Array and a Dictionary (HashMap in Java)?**
  - Arrays store a set of objects (that can be accessed randomly)
  - Dictionaries store pairs of objects
  - Items in an array are accessed by position (index) (often a number) and hence have an order.
  - Items in a dictionary are accessed by key and are unordered.
    This makes array/lists more suitable when you have a group of objects in a set (prime numbers, colors, students, etc.). Dictionaries are better suited for showing relationships between a pair of objects.

---

- **Pros and cons of using Arrays**
  **Pros**:
  - **Fast lookups**. Retrieving the element at a given index takes O(1) time, regardless of the length of the array.
  - **Fast appends**. Adding a new element at the end of the array takes O(1) time.
    **Cons**:
  - **Fixed size**. You need to specify how many elements you're going to store in your array ahead of time.
  - **Costly inserts and deletes**. You have to shift the other elements to fill in or close gaps, which takes worst-case O(n) time.

---

- **Time complexity of basic array operations**
  | Operation | Complexity |
  | --------- | ---------- |
  | Read | ⁍ |
  | Append | ⁍ |
  | Insert | ⁍ |
  | Delete | ⁍ |
  | Search | ⁍ |

---

### Questions: Binary Tree

- **Define Binary Tree**
  A binary tree is made of nodes, where each node contains a “left” pointer, a “right” pointer, and a data element.
  There are three different types of binary trees:
  - **Full binary tree**: Every node other than leaf nodes has 2 child nodes
  - **Complete binary tree**: All levels are filled except possibly the last one, and all nodes are filled in as far left as possible
  - **Perfect binary tree**: All nodes have two children and all leaves are at the same level
    ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%205.png)

---

- **What is binary search tree?**
  **Binary search tree** is a data structure that quickly allows to maintain a _sorted_ list of numbers.
  - It is called a _binary tree_ because each tree node has max of two children
  - It is called a _search tree_ because it can be used to search for the presence of a number in
    $`O(\log n)`$ time
    The properties that separates a binary search tree from a regular binary tree are:
  - All the nodes of left subtree are less than root node
  - All nodes of right subtree are more than root node
  - Both subtrees of each node are also BSTs, i.e. they have the above two properties
    ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%206.png)

---

### Questions: Heaps

- **What is a priority queue**
  A **priority queue** is different from a "normal" queue, because instead of being a "first-in-first-out" data structure, values come out in order by **priority**.

---

- **What is a heap**
  A **heap** is a special tree-based structure which is an almost complete tree that satisfies the heap property:
  - in a **max heap**, for any given node C, if P is a parent node of C, then the key (value) of P is greater than or equal to the key of C
  - in a **min heap**, the key of P is less than or equal to the key of C.
  - NOTE: for a max heap the root is always the largest value, and for a min heap the root is always the smallest
    The node at the top of the heap (with no parents) is called the root node.
    ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%207.png)

---

- **What is Binary Heap?**
  A **binary heap** is a Binary Tree with following properties:
  - It is a complete tree (all levels are completely filled except possibly the last level and the last level has all keys as left as possible). This property of Binary Heap makes them suitable to be stored in an array
  - A binary heap is either **Min Heap** or **Max Heap**. In a Min Binary Heap, the key at root must be minimum among all keys present in Binary Heap. The same property must be recursively true for all nodes in Binary Tree. Max Binary Tree is similar to MinHeap.

---

- **How is Binary Heap usually implemented?**
  A **binary heap** is commonly implemented with an array. Any binary tree can be stored in an array, but because a binary heap is always a complete binary tree, it can be stored compactly. No space is required for pointers, instead, the parent and children of each node can be found by arithmetic on array indices:
  - The root element is `0`
  - Left child: `(2*i)+1`
  - Right child: `(2*i)+2`
  - Parent child: `(i-1)/2`
    ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%208.png)

---

### Questions: Queues

- **What is a queue**
  A **queue** is a container of objects that are inserted and removed according to the first-in first-out principle.
  ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%209.png)

---

- **Why and when should I use Stack or Queue data structure instead of Arrays/Lists**
  - Use a **queue** when you want to get things out in the order that you put them in (FIFO)
  - Use a **stack** when you want to get things out in the reverse order than you put them in (LIFO)
  - Use a **list** when you want to get anything out, regardless of when you put them in (and when you don’t want them to automatically be removed).

---

### Questions: Stacks

- **Explain why Stack is a recursive data structure**
  A **stack** is a recursive data structure, so it’s:
  - a stack is either empty or
  - it consists of a top and the rest which is a stack by itself.

---

- **Define stack**
  A **stack** is a container of objects that are inserted and removed according to the last-in first-out principle.
  There are basically three operations that can be performed on stacks. They are **push**, **pop** and **peek/top.**

---

- **Why and when should I use Stack or Queue data structure instead of Arrays/Lists**
  - Use a **queue** when you want to get things out in the order that you put them in (FIFO)
  - Use a **stack** when you want to get things out in the reverse order than you put them in (LIFO)
  - Use a **list** when you want to get anything out, regardless of when you put them in (and when you don’t want them to automatically be removed).

---

- **Why are stacks useful**
  They’re very useful because they afford you constant time $`O(1)`$ operations when inserting or removing from the front of a data structures.

---

### Questions: Big O Notation

- **What is Big O notation?**
  **Big-O** notation is a relative representation of the complexity of an algorithm. It shows how an algorithm scales based on input size.

---

- **What does it mean if an operation is $`O(\log n)`$?**
  $`O(\log n)`$ means that for every element, you’re doing something that only needs to look at
  **`log N`** of the elements. This is usually because you know something about the elements that let you make an efficient choice.

---

- **What exactly would an $`O(n^2)`$ operation do?**
  $`O(n^2)`$ means that for every element, you’re doing something with every other element, such as comparing them.

---

- **What is worst case?**
  **Worst case** analysis gives the maximum number of basic operations that have to be performed during execution of the algorithm.

---

- **Why do we use Big O notation to compare algorithms?**
  It's difficult to determine the exact runtime of an algorithm. It depends on the speed of the computer processor. So instead of talking about the runtime directly, we use Big O Notation to talk about *how quickly the runtime grows* depending on input size.

---

- **Explain the difference between $`O(1)`$ and $`O(n)`$ space complexities?**
  Let’s consider a traversal algorithm for traversing a list.
  - $`O(1)`$ denotes constant space use: the algorithm allocates the same number of pointers irrespective to the list size
  - $`O(n)`$ denotes linear space use: the algorithm space use grows together with respect to the input size $`n`$

---

### Questions: Hash Tables

- **What is a Hash Table**
  A **hash map** is a data structure that implements an **associative** array abstract data type, a **structure** that can **map keys to values**. Hash tables implement an associative array, which is indexed by arbitrary objects (keys). A hash table uses a **hash function** to compute an **index**, also called a **hash value**, into an **array of buckets** or slots, from which the desired **value** can be found.
  The ConcurrentHashMap implementation provides a thread safe Map implementation.

---

- **Differences between HashMap and HashTables**
  A HashMap is not thread-safe but a HashTable is thread-safe. And HashMaps allow one null key and null values, but a HashTable doesn’t allow any null keys or values.
  (**Thread-safe** means that it functions correctly during simultaneous execution by multiple threads)

---

- **Explain what is Hash Value**
  A **Hash Value** is a string value of string value (of specific length), which is the result of calculation of a Hashing Algorithm.

---

- **What is a hash function?**
  A **hash function** is any function that can be used to map data of arbitrary size to fixed-size values.

---

- **What is hashing**
  **Hashing** is the practice of using an algorithm to map data of any size to a fixed length.

---

### Questions: Linked List

- **Define Linked List**
  A **linked list** is a linear data structure where each element is a separate object. Each element (known as a **node**) of a list is comprising of two item - the **data** and a **reference** (**pointer**) to the next node. The last node has a reference to **null**.
  The entry point into a linked list is called the **head** of the list.

---

- **Advantages of Linked List**
  - Linked Lists are **Dynamic Data Structure** - it can grow and shrink at runtime by allocating and deallocating memory
  - Insertion and deletion are **simple to implement** - unlike array, here we don’t have to shift elements after insertion and deletion of an element. In linked list we just have to update the address present in next pointer of a node
  - **Efficient Memory Allocation/No Memory Wastage** - In case of array there is lot of memory wastage, like if we declare an array of size 10 and only store 6 elements in it.

---

- **Disadvantages of Linked Lists**
  - They use more memory than arrays because of the storage space that pointers take
  - Random access has linear time

---

- **What is a cycle/loop in the singly-linked list**
  A cycle/loop occurs when a node’s next points back to a previous node in the list. The linked list is no longer linear with a beginning and end - instead, it cycles through a loop of nodes

---

- **What are some types of LinkedList**
  - A **singly linked list**
    ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2010.png)
  - A **doubly linked list** is a list that has two references, one to the next node and another to previous node
    ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2011.png)
  - A **multiply linked list** - each node contains two or mode link fields, each field being used to connect the same set of data records in a different order of same set
  - A **circular** **linked list** - where last node of the list points back to the first node (or the head) of the list
    ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2012.png)

---

- **Under what circumstances are Linked Lists useful**
  Linked lists are very useful when you need:
  - to do a lot of insertion and removal
  - splitting and joining lists is very efficient

---

### Questions: Recursion

- **How Dynamic Programming is different from Recursion and Memoization**
  - **Memoization** is when you store previous results of a function call ( a real function always returns the same thing, given the same inputs). It doesn’t make a difference for algorithmic complexity before the results are stored.
  - **Recursion** is the method of a function calling itself, usually within a smaller dataset. Since most recursive functions can be converted to similar iterative functions, this doesn’t make a difference for algorithmic complexity either.
  - **Dynamic Programming** is the process of solving easier-to-solve sub-problems and building up the answer from that.

---

- **What is a good example of Recursion (other than generating a Fibonacci sequence)?**
  There are some:
  Binary tree search, check for palindrome, finding factorial, merge sort

---

- **What is the difference between Backtracking and Recursion?**
  **Recursion** describes the calling of the same function that you are in. You always need a condition that makes recursion stop.
  **Backtracking** is when the algorithm makes an opportunistic decision, which may come up wrong. If the decision was wrong then the backtracking algorithm restores the state before the decision. It builds candidates for the solution and abandons those which cannot fulfil the conditions.

---

```java
private static long[] fibonacciCache;

public static void main(String[] args){
	int n = 6;

	fibonacciCache = new long[n + 1];

	System.out.println(fibonacci(n));
}

public static long fibonnaci(int n) {
	if(n <= 1) {
		return n;
	}

	if(fibonnaciCache[n] != 0) {
		return fibonnaciCache[n];
	}

	long nthFibNum = (fibonnaci(n-1) + fibonnaci(n-2));
	fibonnaciCache[n] = nthFibNum;
	return nthFibNum;
}
```

---

### Questions: Trees

- **Define tree data structure**
  **Trees** are well-known as a non-linear data structure. They don’t store data in a linear way. They organise data hierarchically.
  A **tree** is a collection of entities called **nodes**. Nodes are connected by **edges**. Each node contains a **value** or **data** or **key**, and it may or may not have a **child** node. The first node of the tree is called the **root**. **Leaves** are the last nodes on a tree. They are nodes without children.
  ![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2013.png)

---

- **What is Height and Depth of a Tree and its Nodes**
  - The **depth of a node** is the length to the path to its root
  - The **height of a node** is the number of edges on the longest path from the node to a leaf
  - The **height of a tree** is the length of the longest path to a leaf

---

- **Difference between trees and graphs**
  A graph is a collection of two sets V and E, where V is a finite non-empty set of vertices and E is a finite non-empty set of edges
  - Vertices are nothing but the nodes in the graph
  - Two adjacent vertices are joined by edges.
  - Any graph is denoted as G = {V, E}
  ***
  A tree is a finite set of one or more nodes such that
  - There is a specifically designated node called root
  - The remaining nodes are partitioned into n ≥ 0 disjoint sets $T_1$, $T_2$, $T_3$, ..., $T_n$ where $T_1$, $T_2$, $T_3$, ..., $T_n$ are called the subtrees of the root
  ***
  | Graph                                                           | Tree                                                                                                             |
  | --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
  | Each node can have any number of edges                          | General Trees can have any number of edges, but for nodes in binary trees, they can have at most two child nodes |
  | There is no unique node called root in the graph                | There is a unique node called root in trees                                                                      |
  | A cycle can be formed                                           | There will not be any cycle                                                                                      |
  | Applications: for finding the shortest path in networking graph | Applications: for game trees, decision trees                                                                     |

---

- **What is the difference between Backtracking and Recursion?**
  **Recursion** describes the calling of the same function that you are in. You always need a condition that makes recursion stop.
  **Backtracking** is when the algorithm makes an opportunistic decision, which may come up wrong. If the decision was wrong then the backtracking algorithm restores the state before the decision. It builds candidates for the solution and abandons those which cannot fulfil the conditions.

---

---

---

# CODE BASED EXAMPLES (JAVA):

### LinkedList

In a LinkedList, each element is linked using pointers and addresses. Each element is known as a node, generally preferred over arrays due to ease of insertions and deletions. The nodes cannot be accessed directly instead we need to start from the head and follow through the link to reach a node we wish to access.

Pros: dynamically allocated; inserts & deletes items faster; don’t use a lot of memory

Cons: can’t index items (takes longer to find than an array)

#### Performing Various Operations on LinkedList

##### 1. Adding Elements

- `add(Object)`: This method is used to add an element at the end of the LinkedList
- `add(int index, Object)`: This method is used to add an element at a specific index in the LinkedList

```java
public static void main(String args[]) {
    LinkedList<String> ll = new LinkedList<>();

    ll.add("Geeks");
    ll.add("Geeks");
    ll.add(1, "For");

    System.out.println(ll);
}
```

##### 2. Changing Elements

- `set(int index, Object)`: This method is used to change an element at a specific index in the LinkedList

```java
public static void main(String args[]){
    LinkedList<String> ll = new LinkedList<>();

    ll.add("Geeks");
    ll.add("Geeks");
    ll.add(1, "Geeks");

    System.out.println("Initial LinkedList " + ll);

    ll.set(1, "For");

    System.out.println("Updated LinkedList " + ll);
}
```

##### 3. Removing Elements

- `remove(Object)`: This method is used to simply remove an object from the LinkedList. If there are multiple such objects, then the first occurence of the object is removed
- `remove(int index)`: Since a LinkedList is indexed, this method takes an integer value which simply removes the element present at the specific index in the LinkedList. After removing the element the object is updated, essentially giving a new object with updated indices.

```java
public static void main(String args[]) {
    LinkedList<String> ll = new LinkedList<>();

    ll.add("Geeks");
    ll.add("Geeks");
    ll.add(1, "For");

    System.out.println(
        "Initial LinkedList " + ll);

    ll.remove(1);

    System.out.println(
        "After the Index Removal " + ll);

    ll.remove("Geeks");

    System.out.println(
        "After the Object Removal " + ll);
}
```

##### 4. Iterating the LinkedList

```java
public static void main(String args[]) {
    LinkedList<String> ll
        = new LinkedList<>();

    ll.add("Geeks");
    ll.add("Geeks");
    ll.add(1, "For");

    // Using the Get method and the
    // for loop
    for (int i = 0; i < ll.size(); i++) {

        System.out.print(ll.get(i) + " ");
    }

    System.out.println();

    // Using the for each loop
    for (String str : ll)
        System.out.print(str + " ");
}
```

#### **Example code**

```java
// Java Program to Demonstrate
// Implementation of LinekdList
// class

// Importing required classes
import java.util.*;

// Main class
public class GFG {

    // Main driver method
    public static void main(String args[]) {
        // Creating object of the
        // class linked list
        LinkedList<String> ll = new LinkedList<String>();

        // Adding elements to the linked list
        ll.add("A");
        ll.add("B");
        ll.addLast("C");
        ll.addFirst("D");
        ll.add(2, "E");

        System.out.println(ll);

        ll.remove("B");
        ll.remove(3);
        ll.removeFirst();
        ll.removeLast();

        System.out.println(ll);
    }
}
```

### Maps & HashMap

A map is just a set of key value pairs. (input a name and get back their id number)

HashMap is the most common implementation of the Map interface. Maps don’t guarantee a certain order, but the values are linked up by the key so it doesn’t matter.

```java
// our keys will be String, our values will be Integer
// the values within the diamond operator have to be Java classes
// they can't be primitive types
HashMap<String, Integer> empIds = new HashMap<>();
// adding an entry into a HashMap
empIds.put("Reuben", 12345);
empIds.put("Ryan", 678910);
empIds.put("George", 11121314);

System.out.println(empIds);
// {Reuben=12345, Ryan=678910, George=11121314}

// gets the value for the corresponding key
empIds.get("Reuben");

// checks whether the key has a value within the map (returns a boolean)
empIds.containsKey("Preethi"); // returns false
// checks whether the value has a key within the map
empIds.containsValue(2); // returns false

// if you use .put with and existing key, it will update it's value to the new one

// can use .replace: only replaces value if the key already exists
// does nothing otherwise

// to remove an entry, use .remove as below with the key within the brackets
empIds.remove("Reuben");
```

### HashSet

In Java, HashSet is commonly used if we have to access elements randomly. It is because elements in a hash table are accessed using hash codes.

The hashcode of an element is a unique identity that helps to identify the element in a hash table.

HashSet is not index based as ArrayList, that is why there is no order in HashSets. They also do not accept duplication of elements, but in ArrayList duplication is allowed.

In order to print HashSet elements, you can use Iterator or you can use for-each loop.

HashSets also don’t keep their order when being added, like HashMaps :/
The alternative is LinkedHashSet, which keeps that order!

### General HashSet notation:

```java
// the type of data that's contained in the HashSet is defined by
// what's in the diamond operator
HashSet<String> primates = new HashSet<String>();
// to add to a HashSet
primates.add("lemur");
primates.add("orangutan");
primates.add("spider monkey");
primates.add("silverback gorilla");

System.out.println(primates);
// [lemur, orangutan, spider monkey, silverback gorilla]

// can also do .remove to remove an entry
primates.remove("lemur");

// can remove everything by doing .clear()
primates.clear();

// can get size by doing .size()
System.out.println(primates.size());

// can see if it contains a certain value using .contains()
primates.contains("lemur"); // returns true

// check to see if the Object is empty using .isEmpty()
h.isEmpty(); // returns true if empty, false if not
```

#### Iterating through HashSets:

```java
HashSet<Integer> hashbrowns = new HashSet<Integer>();
hashbrowns.add(7);
hashbrowns.add(24);
hashbrowns.add(5);

// can convert to an array to iterate through it
int[] h = hashbrowns.toArray();

// the better way to do it is
Iterator<Integer> it = hashbrowns.iterator();
// if the set has a next value, it'll keep going
while(it.hasNext()) {
	System.out.println(it.next());
}
```

### Trees

#### Code Structure of TreeNode in a Binary Tree

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2014.png)

Implementing the binary tree (below) in code: (not a search tree)

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2015.png)

```java
public class BinaryTree {
	private TreeNode root;

	private class TreeNode {
		private TreeNode left, right;
		private int data;

		public TreeNode(int data) {
			this.data = data;
		}
	}

	public void createBinaryTree() {
		TreeNode first = new TreeNode(1);
		TreeNode second = new TreeNode(2);
		TreeNode third = new TreeNode(3);
		TreeNode fourth = new TreeNode(4);
		TreeNode fifth = new TreeNode(5);

		root = first;
		root.left = second;
		root.right = third;

		second.left = fourth;
		second.right = fifth;
	}
}
```

#### Code Structure for a Node(binary search tree) and some node functions

```java
package com.company;

public class Node {
    private Node left, right;
    private int data; // Generic type

    public Node(int data) {
        this.data = data;
    }

		// inserting a node into the tree
    public void insert(int value) {
        if (value <= data) {
            if (left == null) {
                left = new Node(value);
            } else {
                left.insert(value);
            }
        } else {
            if (right == null) {
                right = new Node(value);
            } else {
                right.insert(value);
            }
        }
    }

		// check if the node is in the tree
    public boolean contains(int value) {
        if(value == data) {
            return true;
        } else if(value < data) {
            if (left == null) {
                return false;
            } else {
                return left.contains(value);
            }
        } else {
            if(right == null) {
                return false;
            } else {
                return right.contains(value);
            }
        }
    }

		// print the order of the nodes
    public void printInOrder() {
        if (left != null) {
            left.printInOrder();
        }
        System.out.println(data);
        if(right != null) {
            right.printInOrder();
        }
    }

}
```

#### Binary Tree ( each node can have 0 to 2 child nodes)

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2016.png)

#### Inverting a binary tree:

```java
public TreeNode invertTree(TreeNode root) {
    if(root == null) {
        return root;
    }

    TreeNode left = invertTree(root.left);
    TreeNode right = invertTree(root.right);

    // swap
    root.right = left;
    root.left = right;

    return root;
}
```

#### Binary Search Tree (on any subtree, the left nodes are less than the root node, which is less than all of the right nodes).

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2017.png)

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2018.png)

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2019.png)

![Untitled](Java,%20Algorithms%20&%20Data%20Structures%20Prep%2085342950d5c84aae876ddf76e0a24820/Untitled%2020.png)
