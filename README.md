# ArrayTools
This is a library, that allows easier usage of standard Java arrays. For an explanation of each method, 
look at the projects documentation.

Project owners are **Niklas Koll** and **Felix Brosius**, with the help of some friends.

## Table of Contents
- [Features][1]
- [How to add to your project][2]
- [Usage][3]
- [Development][4]

## Features
### Classes
This Library includes helper Classes that all do the same, except with different datatypes.\
These classes are the following:
- ArrayTools
  - Class used for every type of Object (e.g. String, custom classes,...)
- ArrayToolsByte
  - Class used for datatype byte
- ArrayToolsShort
  - Class used for datatype short
- ArrayToolsInt
  - Class used for datatype int
- ArrayToolsLong
  - Class used for datatype long
- ArrayToolsFloat
  - Class used for datatype float
- ArrayToolsDouble
  - Class used for datatype double
- ArrayToolsChar
  - Class used for datatype char
  
### Methods
All of these classes have the same methods:
- **contains(array, target)**
  - checks the array if it contains the target
- **getIndexOf(array, target)**
  - if contains() returns true, checks for the index of the target inside the array
- **getLastIndexOf(array, target)**
  - same as getIndexOf() except it goes through the array backwards 
  so the last appearance of the target is found
- **getMax(array)**
  - returns the maximum value of the array 
  (for the object class it uses a comparator. Klick [here][5] for more information on the usage).
- **getMin(array)**
  - same as the getMax() except returns the minimum value 
  (again, for objects it uses a comparator. Klick [here][5] to look at a more detailed usage case).
- **getCopy(array)**
  - returns an exact copy of the array. It uses the java build in Arrays.copyOf() method.
- **getAmountOf(array, target)**
  - if contains() returns true, counts how many times the target value is inside the array.
- **forEach(array, consumer)**
  - applies the given consumer function to every element in the array.
  This method could be a bit complicated to use, so I have a dedicated [Usage][6] part, only for this method.
- **applyForEach(array, function)**
  - applies the given function to every element in the array.
  This method could be a bit complicated to use, so I have a dedicated [Usage][6] part, only for this method.
- **toString(array)**
  - converts the whole array to a String in this format: [a1,a2,a3,...,a10].\
  For the object class, it uses the Object.toString() method. For the best results, overwrite the toString()
  method in your class.
- **swap(array, pos1, pos2)**
  - swaps two elements in an array. 
- **_Sorting:_**
 
  **Note:** every sorting method for the objects takes as a second parameter a comparator. 
  I have a dedicated part for examples and detailed explanations [here][5], 
  it is a bit easier to understand how to use. 
  - **sortArray(array)**
    - sorts the given array with the Java method Arrays.sort(). This should be safe to work with,
     without any problems.
  - **insertionSort(array)**
    - sorts the given array with an own implementation of the Insertion sort. 
  - **shakerSort(array)**
    - sorts the given array with an own implementation of the Shaker sort.
  - **radixSort(array)**
    - sorts the given array with an own implementation of the Radix sort.
    - _Note:_ Only available with datatypes: int, short, byte; more coming 
  - **More coming in the future...**

## How to add to your project
To add this library to your project you can either copy and paste the class files into your project or import 
the library as a .jar library. To do this, you have to look at the IDEs specific uses (these are the IDEs I used
and are the most used, I think):
- [IntelliJ](https://www.jetbrains.com/help/idea/library.html) 
- [Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_add_an_extra_library_to_my_project%27s_classpath%3F) 
- [NetBeans](https://stackoverflow.com/questions/5893349/java-how-to-add-library-files-in-netbeans)
- [BlueJ](https://stackoverflow.com/questions/32346079/adding-library-in-bluej) (second answer)

## Usage

- [Usage of the basic methods][7]
- [Detailed Example of Comparators][5]
- [Detailed Example of Functions][6]

### Usage of the basic methods
The following shows example uses with explanations to further understand how to use this library:

(_Note:_ Every method shown here is the exact same for primitive datatypes, except the comparator isn't needed.)

Let's begin by defining our class to be used. I made a very simple class to show how the tools work with custom 
classes:

```java
public class ExampleClass
{
    private int n;
    private String s;

    public ExampleClass(int n, String s)
    { 
        this.n = n;
        this.s = s;
    }

    public String getS() {return s;}

    public void setS(String s) {this.s = s;}

    public int getN() {return n;}

    public void setN(int n) {this.n = n;}

    @Override
    public String toString()
    {
        return getS() + "&" + getN();
    }
}
```

As you can see, I'm overwriting the toString() method. That's because I later want to use the ArrayTools.toString()
method and I want to see the values of the class and not the ID.\
The rest of the class is pretty self-explained. 
Just two private variables with the respective getter- & setter-methods.

Now, let's define our array:
```java
ExampleClass[] exampleArray = new ExampleClass[5];

exampleArray[0] = new ExampleClass(5,   "TestA");
exampleArray[1] = new ExampleClass(1,   "TestBeta");
exampleArray[2] = new ExampleClass(3,   "TestDelta");
exampleArray[3] = new ExampleClass(100, "TestGamma");
exampleArray[4] = new ExampleClass(3,   "TestDelta");
```

That's an array with 5 elements of the type ExampleClass. The first 3 elements then got instantiated in the following
lines.

#### contains()

```java
ExampleClass classInArray = new ExampleClass(5, "TestA");
ExampleClass classNotInArray = new ExampleClass(3, "TestA");

System.out.println(ArrayTools.contains(exampleArray, classInArray)); // outputs true
System.out.println(ArrayTools.contains(exampleArray, classNotInArray)); // outputs false
```
The first output is true and the second is false. But why is that?\
The answer is pretty simple:\
The **contains()** method works with the **toString()** method. If we take a look at the output of the **toString()**
on both objects, we see that the first one outputs `TestA&1`, which is the same output of the first element in our array.
The second object would output `TestA&3`, which has the same String before `&`, but a different number.

#### getIndexOf()

```java
System.out.println(ArrayTools.getIndexOf(exampleArray, classInArray)); // outputs 0
```

As we know, `classInArray` is inside the array, so now we want to know the index of it.
The output is `0` because the method iterates over the array and searches for the first appearance of the target element.
The search works basically like the `contains()` method. It iterates over the array and returns the current count of
iterations, if the current element's `toString()` gives the same as the targets `toString()`.
As we defined our array, the corresponding element is at index `0` so the output is correct.

#### getLastIndexOf()

```java
classInArray.setN(3);
classInArray.setS("TestDelta");

System.out.println(ArrayTools.getIndexOf(exampleArray, classInArray)); // outputs 2
System.out.println(ArrayTools.getLastIndexOf(exampleArray, classInArray)); // outputs 4
```

When we change the values of `classInArray` to the values from the duplicate in our array, we now have two different
indices for the same valued element. When we want just the first appearance of it, we can use `getIndexOf()` the same as
before, but if we want the last (in this case the second) appearance, we use `getLastIndexOf()`.
It works basically the same as `getIndexOf()`, except it iterates over the array backwards, which leads to the last index
of the target.

#### getAmountOf()

```java
System.out.println(ArrayTools.getAmountOf(exampleArray, classInArray)); // outputs 2
```

The method `getAmountOf()` counts the times the target is in the array. `classInArray` has the `toString()` value of
`TestDelta&3`. That is equal to 2 of the elements in our array.
This method works basically the same as the `getIndexOf()` method, except it counts the times the element is found 
instead of returning the index of the first appearance.

#### getCopy()

```java
ExampleClass[] secondArr = ArrayTools.getCopy(exampleArray);

for(int i = 0; i < exampleArray.length; i++)
    System.out.print(exampleArray[i].toString() + ", "); // outputs TestA&5, TestBeta&1, TestDelta&3, TestGamma&100, TestDelta&3, 

System.out.println();

for(int i = 0; i < secondArr.length; i++)
    System.out.print(secondArr[i].toString() + ", "); // outputs TestA&5, TestBeta&1, TestDelta&3, TestGamma&100, TestDelta&3, 
```

The method `getCopy()` returns a copy of the array passed as the parameter. The method `Object.equals(Object)` returns still
`false`, if it isn't overwritten in your class, because the method copies the value and not the reference, but if we
give out both arrays, they have all the same values.
`Object.equals(Object)` compares the references and not the values of the two objects.

#### toString()

```java
System.out.println(ArrayTools.toString(exampleArray)); // outputs [TestA&5,TestBeta&1,TestDelta&3,TestGamma&100,TestDelta&3]
```

The method `toString()` returns a String representation of the whole array. The output String is formatted like the following: 
`[element1,element2,...,elementN]`.

#### swap()

```java
System.out.println(exampleArray[0].toString() + ", " + exampleArray[2].toString()); // outputs TestA&5, TestDelta&3
ArrayTools.swap(exampleArray, 0, 2);
System.out.println(exampleArray[0].toString() + ", " + exampleArray[2].toString()); // outputs TestDelta&3, TestA&5
```

The method `swap()` swaps to elements of the array. It is pretty self-explained how to use.


### Detailed Example of Comparators

#### getMin()

```java
ExampleClass minimum = ArrayTools.getMin(exampleArray, (Comparator<ExampleClass>) (o1, o2) -> o1.getN() - o2.getN());
System.out.println(minimum.toString()); // outputs TestBeta&1

minimum = ArrayTools.getMin(exampleArray, new Comparator<ExampleClass>()
{
    @Override
    public int compare(ExampleClass o1, ExampleClass o2)
    {
        return o1.getS().length() - o2.getS().length();
    }
});

System.out.println(minimum.toString()); // outputs TestA&5
```

That looks a bit confusing at first. Let's break it down.

First things first, `getMin()` returns the minimum value of the given array. But how can we find the minimum,
if we don't know what value is less than the other?\
That's where the Comparator comes in handy.

The Comparator gives us the ability to define exactly that. But how?\
There are two ways of doing this:
1. [Lambda expressions][8]
2. [Anonymous Inner classes][9]

I recommend using Lambdas, because it is way shorter, and more readable.

In the first line, the variable minimum is assigned to `getMin()` of our array. The minimum here is found by comparing
the int attribute of our class, as we defined, that `getN()` returns the int value of that object. 
So, if everything is correct, we should get as our output `TestBeta&1` because `1` is the lowest number in our array.

In the third line, the variable minimum is reassigned tp `getMin()`, but this time with a different Comparator.
This time, the Comparator is an anonymous inner class, where it compares not the int value, but the length of 
the String of the object, as we defined, that `getS()` returns the String of that object and `String.length()` returns
the length of that String.

For more Information of the use of Lambdas or Anonymous Inner classes, klick the corresponding link in the list above.


#### getMax()

```java
ExampleClass maximum = ArrayTools.getMax(exampleArray, (Comparator<ExampleClass>) (o1, o2) -> o1.getN() - o2.getN());
System.out.println(maximum.toString()); // outputs TestGamma&100

maximum = ArrayTools.getMax(exampleArray, new Comparator<ExampleClass>()
{
    @Override
    public int compare(ExampleClass o1, ExampleClass o2)
    {
        return o1.getN() - o2.getN();
    }
});

System.out.println(maximum.toString()); // outputs TestDelta&3
```

The `getMax()` method is the counterpart to `getMin()` as it gives the maximum value.

Look at the [`getMin()`](#getmin) method to get a better explanation how it works.


#### sortArray()

```java
exampleArray[3] = new ExampleClass(0,"TestGammba");

ArrayTools.sortArray(exampleArray, (Comparator<ExampleClass>) (o1, o2) -> o1.getN() - o2.getN());
System.out.println(ArrayTools.toString(exampleArray)); // outputs [TestGammba&0,TestBeta&1,TestDelta&3,TestDelta&3,TestA&5]
```
(In the first line I changed the object to make the sorting more clear)

The use of the Comparator is basically the same like [`getMin()`](#getmin). It determines the order and rule
after which is sorted. 

In this example it's the int value of the object again. And, as you can see in the output,
it works. 


#### insertionSort()

```java
exampleArray[3] = new ExampleClass(0,"TestGammba");

ArrayTools.insertionSort(exampleArray, (Comparator<ExampleClass>) (o1, o2) -> o1.getS().length() - o2.getS().length());
System.out.println(ArrayTools.toString(exampleArray)); // outputs [TestA&5,TestBeta&1,TestDelta&3,TestDelta&3,TestGammba&0]
```
(In the first line I changed the object to make the sorting more clear)

The usage is the exact same as [`sortArray()`](#sortarray). Just the implementation is different.

In this example the rule for the sorting is the length of the String again. And, as you can see in the output, it works



### Detailed Example of Functions

These methods can be a bit complicated and hard to understand at first, so i made a couple examples for both.

#### forEach()

Example 1:
```java
ArrayTools.forEach(exampleArray, obj -> System.out.print(obj.toString() + ", ")); // outputs TestA&5, TestBeta&1, TestDelta&3, TestDelta&3, TestGammba&0,
```

In this example every element of the array gets printed out, separated by `", "`. \
The way, functions work in this case, is that the parameter of the lambda expression (in this case obj) is the current
element of the array. In other words: The iterates over the array and passes the current element as the parameter to the
Function.

Example 2:
```java
ArrayTools.forEach(exampleArray, obj -> obj.setN(obj.getN() * 2));
System.out.println(ArrayTools.toString(exampleArray)); // outputs [TestA&10,TestBeta&2,TestDelta&6,TestDelta&6,TestGammba&0]
```

In this example the function sets the int value of every element in the array to `obj.getN() * 2`, so it doubles it. 
Because of Lambdas type inference, the datatype of `obj` isn't needed, it automatically gets detected, in this case as
an object of `ExampleClass`.

With this function, you have to pay attention, **that there is no return value**.
If you want a return value, you have to use [`applyForEach()`](#applyforeach).


#### applyForEach()

Example 1:
```java
ArrayTools.applyForEach(exampleArray, obj -> new ExampleClass(obj.getN()/2, obj.getS()));
System.out.println(ArrayTools.toString(exampleArray)); // outputs [TestA&2,TestBeta&0,TestDelta&1,TestGamma&50,TestDelta&1]
```
In this example the function reassigns every element with a new one, that halfs the int value of the old element.
The way, functions work in this case, is that the parameter of the lambda expression (in this case obj) is the current
element of the array. In other words: The iterates over the array and passes the current element as the parameter to the
Function. In addition to that, it also returns the same datatype as the array. This may not be as useful for objects,
but if you have an int array, you can only change the current value inside the Lambda expression by reassigning the
current element.

Example 2:
```java
ArrayTools.applyForEach(exampleArray, obj -> {
    if((obj.getN()*obj.getN()) % 2 == 0) 
        obj.setS("Even");

    return obj;
});
System.out.println(ArrayTools.toString(exampleArray)); // outputs [Even&2,Even&0,TestDelta&1,Even&50,TestDelta&1]
```
This is the most complicated example so far.
In this case, the String value of the obj only gets reassigned, if the square number of it's int value is even.
For example: The object `TestGamma&50` gets passed to the function. The Square of `50*50=2500` and that is an even number,
so the String gets reassigned to `"Even"` but the int value stays 50.

With this function, you have to pay attention, **that there has to be a return value of the same type as the array**.
If you want no return value, you have to use [`forEach()`](#foreach).

As you can see, Lambda expressions can also be more than one line, but all the rules for Lambdas are listes [here][8].

### Lambda expression

**_work in progress..._**


### Anonymous Inner classes

**_work in progress..._**

### Development

This library is still being worked on, so please contact use if any problem come up or if you have questions or ideas.

---
[Back to Top](#arraytools)


[1]: #features
[2]: #how-to-add-to-your-project
[3]: #usage
[4]: #development
[5]: #detailed-example-of-comparators
[6]: #detailed-example-of-functions
[7]: #usage-of-the-basic-methods
[8]: #lambda-expression
[9]: #anonymous-inner-classes

