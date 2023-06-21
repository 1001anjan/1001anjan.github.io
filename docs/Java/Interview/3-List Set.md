---
layout: default
title: List, Set, Map interface
parent: Interview Preparation
grand_parent: Java
nav_order: 3
---
### HashSet

In Java, a `HashSet` is implemented using a hash table. It internally uses a `HashMap` to store its elements. The `HashSet` class extends the `AbstractSet` class and implements the `Set` interface.

Here's how a `HashSet` is maintained:

* Hashing: When an element is added to a `HashSet`, its hash code is calculated using the `hashCode()` method of the element. The hash code is an integer value that represents the element's internal state.

* Bucket Calculation: The hash code is used to determine the bucket (or index) in the underlying array where the element will be stored. The bucket calculation is performed using the hashCode() value and the current capacity of the HashSet.

* Handling Collisions: In case of hash code collisions (when two elements have the same hash code), a process called "chaining" is used. Chaining involves storing multiple elements in the same bucket by maintaining a linked list of elements. Each bucket can contain multiple elements in a linked list.

* Equals Method: To handle potential hash collisions, the equals() method of the elements is used to check for actual equality between the elements within the same bucket. The `equals()` method is called to compare the added element with the existing elements in the bucket.

* Load Factor and Rehashing: `HashSet` has a load factor, which determines when the underlying array should be resized. By default, the load factor is 0.75, which means that when the HashSet reaches 75% of its capacity, it automatically increases its capacity and rehashes the elements into the new array to maintain efficient performance.

The use of hashing and linked lists (in case of collisions) allows HashSet to provide fast insertion, deletion, and retrieval operations with an average time complexity of O(1).

### Here's an example to illustrate the basic usage of a HashSet:
```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> colors = new HashSet<>();

        colors.add("Red");
        colors.add("Green");
        colors.add("Blue");
        colors.add("Red"); // Duplicate element

        System.out.println("Colors in HashSet: " + colors);
    }
}
```

### TreeSet
In Java, `TreeSe`t is an implementation of the `Set` interface that provides a sorted, ordered set of elements. It uses a self-balancing binary search tree called a `red-black` tree as its underlying data structure. The elements in a `TreeSet` are stored in sorted order according to their natural ordering or a custom `Comparator` provided during construction.

Key features of `TreeSet`:

* Sorted Order: `TreeSet` maintains the elements in sorted order. This allows efficient operations like range queries and finding the minimum or maximum element.
* Unique Elements: Like other `Set` implementations, `TreeSet` does not allow duplicate elements. It ensures that each element in the set is unique.
* Null Values: `TreeSet` does not allow null elements. If you try to insert a null element, it will throw a `NullPointerException`.
* Fast Operations: `TreeSet` provides efficient performance for operations like insertion, deletion, and searching, thanks to the balanced tree structure.
* NavigableSet Interface: `TreeSet` implements the `NavigableSet` interface, which provides additional navigation methods like `lower()`, `higher()`, `floor()`, and `ceiling()` for finding elements relative to a given value.

Here's an example that demonstrates the usage of `TreeSet`:
```java
import java.util.Set;
import java.util.TreeSet;

public class TreeSetExample {
    public static void main(String[] args) {
        Set<String> fruits = new TreeSet<>();

        // Adding elements to TreeSet
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Mango");
        fruits.add("Orange");
        fruits.add("Pineapple");

        // Printing the TreeSet
        System.out.println("Fruits in sorted order: " + fruits);

        // Removing an element
        fruits.remove("Banana");
        System.out.println("After removing Banana: " + fruits);

        // Checking if an element exists
        boolean containsMango = fruits.contains("Mango");
        System.out.println("Contains Mango? " + containsMango);

        // Finding the size of the TreeSet
        int size = fruits.size();
        System.out.println("Size of the TreeSet: " + size);

        // Iterating over the TreeSet
        System.out.println("Iterating over the TreeSet:");
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
    }
}
```
To use objects in a `TreeSet` in Java, you need to ensure that the objects being stored in the set implement the `Comparable` interface or provide a custom `Comparator` to define the sorting order. Here's an example:
```java
import java.util.Set;
import java.util.TreeSet;

class Student implements Comparable<Student> {
    private String name;
    private int rollNumber;

    public Student(String name, int rollNumber) {
        this.name = name;
        this.rollNumber = rollNumber;
    }

    public String getName() {
        return name;
    }

    public int getRollNumber() {
        return rollNumber;
    }

    @Override
    public int compareTo(Student other) {
        return this.rollNumber - other.rollNumber;
    }

    @Override
    public String toString() {
        return "Student [name=" + name + ", rollNumber=" + rollNumber + "]";
    }
}

public class TreeSetExample {
    public static void main(String[] args) {
        Set<Student> studentSet = new TreeSet<>();

        studentSet.add(new Student("Alice", 1));
        studentSet.add(new Student("Bob", 2));
        studentSet.add(new Student("Charlie", 3));
        studentSet.add(new Student("David", 4));
        studentSet.add(new Student("Emily", 5));

        System.out.println("Students in ascending order of roll number:");
        for (Student student : studentSet) {
            System.out.println(student);
        }
    }
}
```
