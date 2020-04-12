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
`Example covering all the concepts above`
```
package academy.learnprogramming.oochallenge

open class kotlinBicycle (var cadence: Int, var speed: Int, var gear: Int){

    fun kotlinApplyBrake(decrement: Int){
        speed -= decrement

    }

    fun kotlinSpeedUp(increment: Int){
        speed += increment

    }

    open fun printDescription(){

        println("Bike is in gear $gear with a cadence of $cadence travelling at a speed of $speed.")

    }

}

class kotlinMountainBike(var seatHeight: Int, cadence: Int, speed: Int, gear: Int) : kotlinBicycle(cadence, speed,
    gear){

    override fun printDescription(){

        super.printDescription()
        println("Mountain Bike has a seat height of $seatHeight.")

    }

}

class kotlinRoadBike(val tireWidth: Int, cadence: Int, speed: Int, gear: Int) : kotlinBicycle(cadence, speed,
    gear){

    override fun printDescription(){

        super.printDescription()
        println("Road Bike has a seat height of $tireWidth.")

    }

}

```
`Secondary Constructor`
```
package academy.learnprogramming.oochallenge

fun main(args: Array<String>){

    val kBic = kotlinBicycle(2, 40)
    val kMB = kotlinMountainBike(3, 3, 30)
    val kRB = kotlinMountainBike(4, 2, 50, color = "Green")

    kBic.printDescription()
    kMB.printDescription()
    kRB.printDescription()

}

open class kotlinBicycle (var cadence: Int, var speed: Int, var gear: Int = 10){

    fun kotlinApplyBrake(decrement: Int){
        speed -= decrement

    }

    fun kotlinSpeedUp(increment: Int){
        speed += increment

    }

    open fun printDescription(){

        println("Bike is in gear $gear with a cadence of $cadence travelling at a speed of $speed.")

    }

}

class kotlinMountainBike(var seatHeight: Int, cadence: Int, speed: Int, gear: Int = 15) : kotlinBicycle(cadence, speed,
    gear){

    var color: String = "Red"

    constructor(seatHeight: Int, cadence: Int, speed: Int, gear: Int = 3, color: String) : this(seatHeight, cadence,
        speed, gear){
        this.color = color
        println("This is the $color")
    }

    override fun printDescription(){

        super.printDescription()
        println("Mountain Bike has a seat height of $seatHeight.")

    }

}

class kotlinRoadBike(val tireWidth: Int, cadence: Int, speed: Int, gear: Int = 20) : kotlinBicycle(cadence, speed,
    gear){

    override fun printDescription(){

        super.printDescription()
        println("Road Bike has a seat height of $tireWidth.")

    }

}
```

#### init blocks
* `init` block runs when the instance is created and it runs in conjuction with the primary constructor.
* There can be mulitple `init` blocks within the same class.

### 37. Properties and Backing Fields in Kotlin
* Kotlin classes can only have properties. They do not have fields.
??? Need to understand this better


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

### 39. Kotlin function Basics

* When a function is member of the class, it is generally referred to as `method` or `member function`.
* If you are not returning anything form the function, you are returning `Unit`.
`fun main(args: Array<String>)` is same as `fun main(args: Array<String>) : Unit`
* Functions with curly braces have `Block body`. Functions without curly braces have `Expression body`.

```
fun main(args: Array<String>){

    println(labelMultiply1(3, 4, "Result : "))
    println(labelMultiply2(3, 5, "[Make function 1 liner] Result : "))
    println(labelMultiply3(3, 6, "[Remove return type from function] Result : "))

}

fun labelMultiply1(op1: Int, op2: Int, msg: String) : String{

    return ("$msg${op1 * op2}")

}

fun labelMultiply2(op1: Int, op2: Int, msg: String) : String = "$msg${op1 * op2}" //Make the function 1 liner

fun labelMultiply3(op1: Int, op2: Int, msg: String) = "$msg${op1 * op2}" //Remove return type
```
#### main function - expression body
```
fun main(args: Array<String>)= println(labelMultiply1(3, 4, "Result : "))
```
#### Name Argumets 
* Calling the function and naming the arguments
```
fun main(args: Array<String>)= println(labelMultiply1(op1=3, op2=4, label="Result : "))
```
#### vararg
* Kotlin can have functions that can have arbitary number of arguments i.e. Number of cars below are 3 but they can be 5 as well.
* Only `vararg` parameter per function signature
```
fun main(args: Array<String>){

    val car1 = Cars("i10", "White", 2014)
    val car2 = Cars("Swift", "Blue", 2014)
    val car3 = Cars("Baleno", "Navy Blue", 2014)

    printCarNameColors(car1, car2, car3)

}

fun printCarNameColors(vararg cars : Cars){
    for(car in cars){
        println(car.model + " -- " + car.color)
    }
}
```
* Additional parameter
```
fun main(args: Array<String>){

    val car1 = Cars("i10", "White", 2014)
    val car2 = Cars("Swift", "Blue", 2014)
    val car3 = Cars("Baleno", "Navy Blue", 2014)

    printCarNameColors(car1, car2, car3, str = "Color is:  ")

}

fun printCarNameColors(vararg cars: Cars, str: String ){
    for(car in cars){
        println(car.model + " -- " + car.color)
    }
}
```
`Spread Operator (*)` 
* Used to get the actual elements of the array
* Without Spread Operator
```
fun main(args: Array<String>){

    val car1 = Cars("i10", "White", 2014)
    val car2 = Cars("Swift", "Blue", 2014)
    val car3 = Cars("Baleno", "Navy Blue", 2014)

    val manyCars = arrayOf(car1, car2, car3)

    val moreCars = arrayOf(car2, car3)

    val car4 = car1.copy()

    var multipleCarArray = arrayOf(manyCars, moreCars, car4)

    for(car in multipleCarArray){
        println(car)
    }

}
O/P - 
[Lacademy.learning.Cars;@60e53b93
[Lacademy.learning.Cars;@5e2de80c
Cars(model=i10, color=White, year=2014)
```
* With Spread Operator
```
fun main(args: Array<String>){

    val car1 = Cars("i10", "White", 2014)
    val car2 = Cars("Swift", "Blue", 2014)
    val car3 = Cars("Baleno", "Navy Blue", 2014)

    val manyCars = arrayOf(car1, car2, car3)

    val moreCars = arrayOf(car2, car3)

    val car4 = car1.copy()

    var multipleCarArray = arrayOf(*manyCars, *moreCars, car4)

    for(car in multipleCarArray){
        println(car)
    }

}
O/P - 
Cars(model=i10, color=White, year=2014)
Cars(model=Swift, color=Blue, year=2014)
Cars(model=Baleno, color=Navy Blue, year=2014)
Cars(model=Swift, color=Blue, year=2014)
Cars(model=Baleno, color=Navy Blue, year=2014)
Cars(model=i10, color=White, year=2014)
```

### 40. Extension Functions

* Extension functions let you extend any class you want to extend.
* For adding the methods.
* But that is not sub classing. 
* `Extension functions` create an illusion of adding methods to a specific class. Eg - If we have created certain String manipulation functions then instead of writing these methods in a separate class these methods can be added as Extension functions to the String class.
`Note` : To make a function an Extension -
* `String.` is added before the name of the function
* String argument is removed as it is a string function
* String variable is referred to with `this`
* In this example, String is the class we are extending. Hence it is a `Receiver type`
```
fun main(args: Array<String>) {

    val sampleStr = "stay hungry stay foolish"
    println(sampleStr.upperFirstAndLast())

}

fun String.upperFirstAndLast() : String{

    val upperFirst = this.substring(0, 1).toUpperCase() + this.substring(1)
    return upperFirst.substring(0, upperFirst.length-1) +
        upperFirst.substring(upperFirst.length-1, upperFirst.length)
        .toUpperCase()

}
```
`Note` - Above function will run after removing `this` as well
 ```
 fun String.upperFirstAndLast() : String{

    val upperFirst = this.substring(0, 1).toUpperCase() + this.substring(1)
    return upperFirst.substring(0, upperFirst.length-1) +
        upperFirst.substring(upperFirst.length-1, upperFirst.length)
        .toUpperCase()

}
```

### 41. Inline Functions

* When `Inline Function` is compiled, its body is directly compiled for the function call.
* It is not compiled to function at all. It is compiled to its body.
* If you do not mark the function as `Inline` does not mean it will not be `Inline`. JVM might decide to make it `Inline` as well.
* Inlining works best for functions with Lambda paramters.

### 42. 43. Inheritance 

* Everything in Kotlin is `public` and `final` buy default.
* `open` - When the class is to be extended then it has to get rid of the default `final`. In that case, the class is made `open`.
* `open` keyword is not to be used with the `abstract` classes.
* When the need is for something to be `extendable` or `overridden`, then make the use of the `open` keyword unless it is `abstract`.
* When we override a function from the superclass, then we have to use the `override` keyword next to the function.
* When making use of the `abstract classes` or `abstract keyword`, we need not make the use of the `open` keyword.

```
package academy.learnprogramming.inheritance

fun main(args : Array<String>){

    val laser = LaserPrinter("Xenon")
    laser.displayModel()

}

abstract class Printer(val modelName: String){

    open fun displayModel() = println("Model name is $modelName")
    abstract fun bestSellingPrice(): Double

}

class LaserPrinter(modelName: String) : Printer(modelName) {

    override fun displayModel() = println("Laser Printer Model name is $modelName")
    override fun bestSellingPrice(): Double = 129.99

}
```
* `override` also means `open`. So when we use the `override` keyword, what we also mean is that the function is `open`.
* If we do not want the method of a class to be `overridden` further, then make the use of the `final` keyword. This is the only place where the keyword `final` is explicitly used.*
```
package academy.learnprogramming.inheritance

fun main(args : Array<String>){

    val laser = LaserPrinter("Xenon")
    laser.displayModel()

}

abstract class Printer(val modelName: String){

    open fun displayModel() = println("Model name is $modelName")
    abstract fun bestSellingPrice(): Double

}

open class LaserPrinter(modelName: String) : Printer(modelName) {

    final override fun displayModel() = println("Laser Printer Model name is $modelName")
    override fun bestSellingPrice(): Double = 129.99

}

class SpecialLaserPrinter(modelName: String) : LaserPrinter(modelName){
    
    override fun displayModel() = println("Special Laser Printer Model name is $modelName") // Gives Error
    
}
```
* Calling `super secondary constructor` only makes sense if there is no `primary constructor`.
* `Data classes` are closed tight. They cannot be extended.

### 44. Interfaces

* When a class extends another class, `open` keyword has to be used. But in case of interfaces, that is not needed.
```
interface myInterface{

    fun myFunction(str: String)

}

interface mySubIntreface : myInterface{

    fun mySubFunction(num: Int)

}

class myClass : mySubIntreface{

    override fun mySubFunction(num: Int) {

    }

    override fun myFunction(str: String) {

    }

}
```
* If a property is defined, then its value has to be provided in the class that implements it.
`Concrete Implementation`
```
interface myInterface{

    fun myFunction(str: String)
    val number: Int

}

interface mySubIntreface : myInterface{

    fun mySubFunction(num: Int)

}

class myClass() : mySubIntreface{

    override val number: Int = 25 //Concrete Implementation

    override fun mySubFunction(num: Int) {

    }

    override fun myFunction(str: String) {

    }

}
```

### 45. Singletons
* There are 3 use cases for the object keyword -
    * Singleton
    * Companion objects
    * Object expressions
* Singleton is used when we want only one and one instance of the class while the application is running.
* When we need Singleton in Kotlin, we make use of the `Object` keyword because this way there will be only one instance of the object class.
* When we declare the `Object` class what we say is we want only one and one instance of the class.
* There is ever a one instance of the object and it is created the first time the class is used.
* `Singletons` can extends other Classes or implement Interfaces.
```
package academy.learnprogramming.inheritance

import java.time.Year

fun main(args: Array<String>){

    println(ObjectCompanions.getTagLine())
    println(ObjectCompanions.getTradeMark())

}

object ObjectCompanions {

    val currentYear = Year.now().value
    fun getTagLine() = "Our Company Rocks!"
    fun getTradeMark() = "Copyright \u00A9 Our company. All rights reserved."

}
```

### 46. Companions
* `static` keyword does not exist in Kotlin.
* `Companion objects` can be created inside classes and they can be accessed inside classes without creating an instance of the class.
* Everything within the `Companion Object` is static which is equivalent of what we had in Java.
```
fun main(args: Array<String>){

    println(someClass.someCompanion.accessPrivateVar())
    println(someClass.accessPrivateVar()) // This and the line above means the same

}

class someClass{

    companion object someCompanion{

        private var privateVar = 6

        fun accessPrivateVar() = "I'm accessing private var $privateVar"

    }

}
```
* `Companion objects` can be used to call `Private constructors`. 

### 47. Anonymous Objects 

* `Anonymous Objects` are used where we used `Anonymous Classes` in Java.
??? Need to understand this better

### 48. Enums

* Kotlin has `enum class` to declare enums
* Can declare properties in `enum`
* When you add function to the enum, you will have to add ';' after the next enum
```
fun main(args: Array<String>) {

    println(testStatus.PASSED.printTestStatus())

}

enum class testStatus(val msg: String, val count: Int){

    PASSED ("Number of Passed Tests", 5),
    FAILED ("Number of Failed Tests", 4),
    SKIPPED ("Number of Skipped Tests", 1);

    fun printTestStatus() = "$msg : $count"

}
```

### 49. Imports in Kotlin

#### Packages
* Package names do not have to match the directory structure
```
package academy.learning.anotherpackage

import academy.learning.labelMultiply3

fun main(args: Array<String>) {

    println(labelMultiply3(5, 6, "[From Another Package] Multiplicaton Result : "))

}
```

#### Module
* If a Module wants to make the use of the method from the package of the parent project, then the module will have to be added as a dependency.
```
package com.academy.learning

import academy.learning.labelMultiply3

fun main(args: Array<String>){

    println(labelMultiply3(5, 6, "[From Another Module]  Multiplicaton Result : "))
    println(testStatus.PASSED.printTestStatus())

}
```

* Imports can be shortened by using `as` for Objects, Top-Level Functions
```
package com.academy.learning

import academy.learning.labelMultiply3 as lblMult3

fun main(args: Array<String>){

    println(lblMult3(5, 6, "[From Another Module] Multiplicaton Result : "))

}

* Imports also work for `Extension functions`
```
package com.academy.learning

import academy.learning.javacode.upperFirstAndLast

fun main(args: Array<String>){

    println("shreyas chaudhari".upperFirstAndLast())

}

### 50. Internal Access Modifier

* `Private` Only accessible within the class
* `Internal` Only visible within the same module
* If the class is `private` then there is no meaning in declaring its members are `internal` because anyways they are accessible only within the class. 
