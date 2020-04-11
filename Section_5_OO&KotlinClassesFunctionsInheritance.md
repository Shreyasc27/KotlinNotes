# Section 5 : OO And Kotlin : Classes, Functions, Inheritance

### 35. Access Modifier

* In Kotlin, `Functions` and `Properties` can be defined at the top level.
* 4 access modifiers -
    * public
    * private
    * protected
    * internal
    
#### Top-Level
   
* If no access modifier is specified, then declaration is `Public`.
* `Default visibility is Public`
* If top level item is Private then everything within the same class can access it.
* Not necessary that the name of the file should name of the class in the file. So we can many `Public` classes in a single kotlin file.

* Classes can be `Private`. Everything within the same file can be accessed.

* `Module` - Group of files that are compiled together
* Top level item that is marked `Internal` can only be accessed inside a `Module`

* `Private` - Visible with the same file
* `Protected` - Can't be used
* `Public` - Visible everywhere
* `Internal` - Visible within the same module

#### Class Members
* Anything inside a `Module` that can see a `Class` can also see its `Internal Members`.

* In Kotlin, classes cannot see Private members belonging to Inner classes.

* When Kotlin files compile, the access modifiers have to be compiled to the modifiers that JVM understands.
    * `Private` is compiled to `Package Private`
    * `Internal` is compile to `Public`

* Kotlin inforces its visibility rules at Compile time.

### 36. Declaring Classes and Using Constructors in Kotlin

* All classes are `Public` & `Final` by default.

#### Primary Constructors
* Kotlin has a concept of `Primary Constructors` that can be defined outside the Curly braces.
* Since `Primary Constructors` are outside the curly braces, they cannot hold the code. So if there is something to be done, that is to be done using the `init` block.
```
fun main(args : Array<String>) {

    val emp = Employee("Shrungi")
    print("${emp.firstName}")

}

class Employee constructor(firstName: String){

    val firstName: String

    init{
        this.firstName = firstName
    }

}

//OR - Getting rid of the the `init` block
class Employee constructor(firstName: String){

    val firstName: String = firstName

}

//OR - Constructor definition also being property declaration
class Employee constructor(val firstName: String){

}

//OR - Removing the keyword constructor
class Employee(val firstName: String){

}

```
* When defining a constructor with specific access, the keyword constructor has to be mentioned explicitly. If access is public, then not needed.
```
class Employee protected constructor(val firstName: String){

}

```
#### Secondary Constructors
* Once declared inside the Curly braces of the class are called as `Secondary Constructors`.
* If a class has a `Primary Constructor` in the class then the `Secondary Constructor` has to delegate to the `Primary Constructor`.
* Default values can also be used in the `Secondary Constructor`.
```
fun main(args : Array<String>) {

    val emp1 = Employee("Shrungi")
    println("${emp1.firstName}")

    val emp2 = Employee("Shreyas")
    println("${emp2.firstName}")
    println("${emp2.fullTime}")

    val emp3 = Employee("Sanjeev", false)
    println("${emp3.firstName}")
    println("${emp3.fullTime}")

}

class Employee constructor(val firstName: String){

    var fullTime: Boolean = true

    //this(firstName) makes sure that the default constructor is used
    constructor(firstName: String, fullTime: Boolean) : this(firstName){
        this.fullTime = fullTime
    }

}
```
* When the multiple values are to be defined as a part of the `primary constructor` and initialized a default value as well.
```
fun main(args : Array<String>) {

    val emp1 = Employee("Shrungi")
    println("${emp1.firstName}")

    val emp2 = Employee("Shreyas")
    println("${emp2.firstName}")
    println("${emp2.fullTime}")

    val emp3 = Employee("Sanjeev", false)
    println("${emp3.firstName}")
    println("${emp3.fullTime}")

}

class Employee constructor(val firstName: String, var fullTime: Boolean = true){

}
```
* It is absolutely okay to not have `Primary Constructor`. In that case, we do not have to differ to anything.
```
fun main(args : Array<String>) {

    println(Department().name)

}

class Department{

    val name: String

    constructor() {
        name = "N26"
    }

}
```

#### init blocks
* `init` block runs when the instance is created and it runs in conjuction with the primary constructor.
* There can be mulitple `init` blocks within the same class.

### 37. Properties and Backing Fields in Kotlin

### 38. Constants and Data Classes

#### Constants
* In Kotlin, we can have `Top Level Constants` like we have `Top Level Functions`
* No need of declaring a dedicated class for only constants (especially in the absence of ENUMS)
```
package academy.learning

//Top Level Constant
val MY_CONSTANT = 100

fun main(args : Array<String>) {

    println(MY_CONSTANT)

}
```

#### Data Classes
* If we have a class that stores state i.e. fields and getters and setters and nothing else then we should make use of the `Data Class`.
* When we create a Data class, we get some functionality for free from Kotlin.
* Comes free with -
    * toString()
    * custom implementation of the equals() and hashcode() functions
    * copy function
* If you dont want the default functions, then you can add your own
* Data Class Requriements -
    * `Primary Constructor` to have atleast 1 parameter
    * all the `Primary Consturctor` parameters have to marked `val or var`.
    * can't be `sealed, abstract or inner classes`
    * Can add properties that are not part of the default constructor. But those will not be toString() or equals().
```
fun main(args : Array<String>) {

    val myCar = Car("White", "i10", 2017)
    println("Data Class - ${myCar}")

    val emp = Employee("Shrungi")
    println("Non-Data Class - ${emp}")

}

class Employee constructor(val firstName: String, var fullTime: Boolean = true){

}

data class Car(val color: String, val model: String, val year: Int){

}

O/P -
Data Class - Car(color=White, model=i10, year=2017) // Default implemented toString() method of Data class
Non-Data Class - academy.learning.Employee@60e53b93 // Non-implemented method of Normal class print instane reference

```
* When you worked with `Data classes`, you get equals function for free
```
fun main(args : Array<String>) {

    val myCar1 = Car("White", "i10", 2017)
    println("Data Class - ${myCar1}")

    val myCar2 = Car("White", "i10", 2017)
    println("Data Class - ${myCar2}")

    println(myCar1 == myCar2)

}

O/P - true //equals method implemented by the Data Class
```
* When you worked with `Data classes`, you get copy function for free
fun main(args : Array<String>) {

    val myCar1 = Car("White", "i10", 2017)
    
    val myCar3 = myCar1.copy()
    println("${myCar3}")

    val myCar4 = myCar1.copy(year = 2018)
    println("${myCar4}")

}

O/P - 
Car(color=White, model=i10, year=2017) // Default copy()
Car(color=White, model=i10, year=2018) // Copy with value over-ridden

### 41. Inline Functions

* When `Inline Function` is compiled, it is not compiled to a function. It is compiled to its body.
* If you do not mark the function as `Inline` does not mean it will not be `Inline`. JVM might decide to make it `Inline` as well.
* Inlining qorks best for functions with Lambda paramters.

??? Need to study this concept more