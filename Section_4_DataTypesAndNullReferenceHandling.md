# Section 4: Data Types and Null Reference Handling

### 28. The Builtin Data Types in Kotlin

* Java automatically widens the numbers
* There is not automatic widening of numbers in Kotlin
```
var myInt = 10
var myLong = 20L
myLong = myInt // Gives error
myLong = myInt.toLong() // Works
```
* Kotlin will automatically widen literals
* Primitive Data Types

```
val myInt: Int = 33
val myDouble: Double = 33.33
val myFloat: Float = 33.33f
val char: Char = 'd'
val myCharInt = 65
println("myCharInt.toChar() - ${myCharInt.toChar()}")
val myBoolean: Boolean = true
```
* When it comes to the primitive types, Kotlin classes compile to the primitive types under the cover
* `Any` - Base of the Kotlin Class Heirarchy
* `Unit` - If there is a method that does not return anything, then it has to be of type of `unit`. In Java, `void` method does not return anything. But in Kotlin, a method that returns `unit` returns `Singleton Unit` instance.
* `Nothing` - When a function is not going to return anything, then it has to be `Nothing`

### 29. Arrays in Kotlin

* No special Array type in Kotlin. Array is a class like any other.
* Array class is a Collections class.

```
val arrayOfNames1 = arrayOf("Shreyas", "Shrungi", "Sanjeev")
val arrayOfNames2 = arrayOf<String>("Shreyas", "Shrungi", "Sanjeev")
println(arrayOfNames1 is Array<String>) // prints true
println(arrayOfNames1[1]) // prints Shrungi
```
```
var arrayOfData: Array<Int>
arrayOfData = arrayOf(1, 2, 3)
```
```
var someArray: Array<Int>
someArray = arrayOf(1, 2, 3, 4)

for(numbers in someArray){
    println(numbers)
}

//Prints 1, 2, 3, 4
```
```
someArray = Array(6) {i -> (i + 1) * 10}

for(numbers in someArray){
    println(numbers)
}

//Prints 10, 20, .., 60
```
* Array can be created that can contain Ints, Strings, Chars etc
* Primitive Array Types
```
var mixedArray = arrayOf("Shreyas", 123, BigDecimal(10.5), 'S')

for(numbers in mixedArray){
    println(numbers)
}

//Prints Shreyas 123 10.5 S

println(mixedArray is Array<*>) //returns `true`
```
```
var someIntArray = intArrayOf(1, 2, 3, 4)
var someFloatArray = floatArrayOf(2.1F, 3.4F, 5.1F)

var arrayOfSize = IntArray(5)
arrayOfSize = intArrayOf(1, 2, 3, 4)
```
```
val convertedIntArray = myIntArray.toTypedArray()
```

### 30. 31. Null References in Kotlin
* If you want to tell Kotlin compiler that the variable can have the value null then you have to explicitly tell by using the `?`
```
val str: String? = null
```
```
val str: String? = "This isnt null"

str.toUpperCase() // Directly this without the null check gives an error

if(str != null){
    str.toUpperCase()
}
```
* `Safe Call Operator` - Substitute for the `if(str != null)` condition
```
val str: String? = "This isnt null"
str?.toUpperCase() //Replacement for the if condition above

```

* Whenever you are using `?` after the Data type, then you should use `?` after the variable so as to have a check for NullPointerException
```
var str: String? = "This can be null" // '?' after data type String
str?.toUpperCase() // '?' after variable str

println("What happens when we do this ${str?.toUpperCase()}")
```
* In the below line, a check is made
if the `bankBranch` is not null, then look out for `address`
if the `address` is not null, then look out for `country`
if the `country` is not null, then the `countryCode`
```
val countryCode: String? = bankBranch?.address?.country?.countryCode
```
* `Elvis Operator - ?:` - If value present then assign that value or else assign a default value.
```
val str: String? = "This isnt null"

println("What happens when we do this ${str?.toUpperCase()}")

val str2 = str ?: "Default value of str2"

println("Value of 'str2' is {$str2}") //Prints 'This isnt null'
```
```
val str: String? = null

println("What happens when we do this ${str?.toUpperCase()}")

val str2 = str ?: "Default value of str2"

println("Value of 'str2' is {$str2}") //Prints null
```
* Elvis operator applied to the previous example
```
val countryCode: String? = bankBranch?.address?.country?.countryCode ?: "USA"
```
`Safe Cast Operator - as?`
```
val something: Any = arrayOf(1, 2, 3, 4)
val str = something as? String
println(str) // Prints null because something is Int
```
* `Not Null Assertion - !!` - Tell the compiler that the variable cannot be null
This makes sure that the NullPointerException is thrown if the variable value is null
```
val str: String? = "This isnt null"
val str3 = str!!.toUpperCase()

//Equivalent of
if(str == null){
    throw Exception
}else{
    str3 = str.toUpperCase()
}
```
This throws NullPointerException
```
val str: String? = null
val str3 = str!!.toUpperCase()

//O/P -
Exception in thread "main" kotlin.KotlinNullPointerException
	at com.kotlinlearning.kotlincode.NullReferencesKt.main(NullReferences.kt:6)

```
* `let` - Will execute the step only if the value of the variable is not null.
let this happen as far as str is not null
Uses the lambda expression using the variable `it`
```
fun main(args: Array<String>) {

    val str: String? = "This isn't null"
    //val str: String? = null

    str?.let { printText(it) } //let this happen as far as str is not null

    //Equivalent of
    if(str != null){
       printText(str)
    }else{

    }

}

fun printText(str: String){

    println(str)

}

O/P - if str is null then nothing else print "This isn't null"
```