# Section 6: Loops, and the If, When, and Try/Catch Expressions

* For loops in Kotlin uses `Ranges`.
* `Ranges` - Have start anf the end value. Can be used for For loop or Can be assigned to variables.
* Any type that is `comparable` can be used in a range.
* `in` operator is used to check if the value is in range.
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

}
```
```
* Loops can be named using '@'. Eg - 
```
loopSeasons@ for(season in seasons){
        println(season)
    }

    break@loopSeasons
    continue@loopSeasons
```