# Section 6 : Loops, and the If, When, and Try/Catch Expressions

### 54. For Loop

* For loops in Kotlin uses `Ranges`.
* `Ranges` - Have start anf the end value. Can be used for For loop or Can be assigned to variables.
* Any type that is `comparable` can be used in a range.
* `in` operator is used to check if the value is in range.
* Loops can be named using '@'. Eg - 
```
package academy.learningprogramming.loops

fun main(args: Array<String>) {

    val range = 1..5
    for(i in range){
        println(i)
    }

    val charRange = 'a'..'z'
    val stringRange = "ABC".."XYZ"
    //Not allowed
    /*for(s in stringRange){
        println(s)
    }*/

    val str = "ShreyasChaudhari"
    for(i in str){
        println(i)
    }

    val backwardRange = 5.downTo(1)
    val backwardRangeIncorrect = 5..1 // Does not work

    println(2 in range)
    println('p' in charRange)
    println("CCCCC" in stringRange)
    println("PQR" in stringRange)
    println("ZZZZZZ" in stringRange) //false as "Z" > "X"
    println(3 in backwardRange)

    val stepRange = 3..15
    for(i in stepRange){
        println(i)
    }
    val stepThree = stepRange.step(3)
    for(i in stepThree){
        println(i)
    }
    val reversedRange = range.reversed()
    for(i in reversedRange){
        println(i)
    }

    println(stepThree)
    println(reversedRange)

    for(num in 1..20 step 4){
        println(num)
    }

    for(num in 20 downTo 15){
        println(num)
    }

    for(num in 1 until 10){
        println(num)
    }
}
```
```
fun main(args: Array<String>) {

    val seasons = arrayOf("spring", "summer", "winter", "fall")

    loopSeasons@ for(season in seasons){
        println(season)
    }

    for(index in seasons.indices){
        println("${seasons[index]} is a season number $index")
    }

    seasons.forEach { println(it) }

    val notASeason = "whatever" !in seasons
    println(notASeason)

    val notInRange = 32 !in 1..10
    println(notInRange)

    loopSeasons@ for(season in seasons){
        println(season)
    }

    //break@loopSeasons
    //continue@loopSeasons

}    
```

### 55. The If Expression
* `If` can evaluate to a value.
* `Iternary Operator` does not exist in Kotlin.
* When `If` is to be used as an expression there has to be both if and else.   
* `When` should be exhaustive. It should have necessary Else branch. 
```
fun main(args: Array<String>){

    val someCondition = 221 < 33

    val num = if (someCondition) 30 else 50

    println(num)

}
```

### 56. When Expression

* `When` is `Switch`.
* Like `Switch` there is no `break` in `When`. So in Kotlin, only 1 branch can be executed at any point in time.
```
fun main(args: Array<String>){

    val num = 12

    when(num){

        in 10..15 -> println("Range 10 to 15")
        100, 600 -> println("100-600")
        200 -> println("200")
        300 -> println("300")
        else -> println("Doesn't match anything")

    }

}
```
`Expressions in When`
```
fun main(args: Array<String>){

    val num1 = 100
    val x = 20

    when(num1){
        x + 80 -> println("90")
        x + 90 -> println("100")
        x + 100 -> println("110")
    }

}
```
`When - Smart Casting`
```
fun main(args: Array<String>){

    val obj1 : Any = "String"
    val obj2 : Any = BigDecimal(20.55)
    val obj3 : Any = 32

    val obj = obj1

    when(obj){
        is String -> println("String")
        is BigDecimal -> println("Big Decimal")
        is Integer -> println("Integer")
    }

}
```
`Exhaustive Else Branch` - When assigning value of `When` to variable.
```
fun main(args: Array<String>){

    val obj1 : Any = "String"
    val obj2 : Any = BigDecimal(20.55)
    val obj3 : Any = 32

    val obj = null

    val z = when(obj){
        is String -> println("String")
        is BigDecimal -> println("Big Decimal")
        is Integer -> println("Integer")
        else -> println("Unknown Type")
    }

}
```
`Enums - When` - Branches in Enum are exhaustive. Hence do not need an `else`.
* If any of the values from the enum are removed, then the `else` will become mandatory.
```
enum class Season{
    SPRING, SUMMER, WINTER, FALL
}

fun main(args: Array<String>){

    val timeOfTheYear = Season.FALL
    
    val season = when(timeOfTheYear){
        Season.WINTER -> println("WINTER")
        Season.SPRING -> println("SPRING")
        Season.SUMMER -> println("SUMMER")
        Season.FALL -> println("FALL")
    }

    println(season)

}
```
`Conditions - When`
```
fun main(args: Array<String>){

    val numb1 = 100
    val numb2 = 200

    when{
        numb1 < numb2 -> println("Numb1 < Numb2")
        numb1 > numb2 -> println("Numb1 > Numb2")
        else -> println("Numb1 == Numb2")
    }

}
```

### 57. Try/Catch Expression
* `try-catch` is similar to the one in Java. However, in Kotlin, `try-catch` can be used as an expression. 
* Kotlin does not distinguish between `Checked` & `UnChecked` exceptions.
* `finally` block is not involved in the evaluation of the `try-catch` expression. No value will ever be returned from the finally block.
```
import java.lang.NumberFormatException

fun main(args: Array<String>){

    println(getNumber("Shreyas"))
    println(getNumber("123"))

}

fun getNumber(str : String) : Int{

    return try{
        Integer.parseInt(str)
    }catch(e: NumberFormatException){
        0
    }finally{
        println("In Finally Block!")
    }

}
```

```
import java.lang.IllegalArgumentException
import java.lang.NumberFormatException

fun main(args: Array<String>){

    println(getNumber("22.5")) ?: throw IllegalArgumentException("Number is an int!")

}

fun getNumber(str : String) : Int?{

    return try{
        Integer.parseInt(str)
    }catch(e: NumberFormatException){
        null
    }finally{
        println("In Finally Block!")
    }

}
```
`Nothing Class` - There can be a case when there is a possiblility of function throwing an exception.
import java.lang.IllegalArgumentException
import java.lang.NumberFormatException
```
fun main(args: Array<String>){

    notImplemented("String")

}

fun notImplemented(something: String) : Nothing{

    throw IllegalArgumentException("Implement me!")

}
```