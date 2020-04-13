# Section 3 : Basic Differences Between Kotlin and Java

### 16. Hello World from Kotlin

* `In Kotlin, it is possible to write code that is outside the class.`

* `REPL` - Read Eval Print Loop

* When compiling the Kotlin programs, `Kotlin compiler` compiles that `.kt` files in `byte code` ie `.class` files

* Java : Java Runtime Library
Kotlin : Kotlin Runtime Library

* In Kotlin, methods can be created independent of classes.
* When the code is compiled, Kotlin compiler adds classes to the methods.

* Functions defined out classes are called `Top Level Functions`

### 17. The Kotlin Standard Library

* Kotlin imports whole lot of stuff be default into every Kotlin file.

* Kotling Standard Library serves the same purpose as what the JDK does.

* While distributing the Kotlin application, also have to distribute the Kotlin Runtime.

### 18. Variable Declarations in Kotlin

* Kotlin uses `Type Inference`. Compiler can usually figure out or infer the type of the variable based on the context in which you are using it.
* This happens at Compile time and not at Run time.
* Kotlin is a statically type language.

* `val` - Declaration is Immutable. Equivalent to final in Java. Recommended in Kotlin.
* For immutable variables, it is possible to change the value of the instance properties.

### 19. How to Create Type Aliases in Kotlin

* Kotlin Aliases - They help you use another name for the existing type.
e.g.
`typealias EmployeeSet = Set<Employee>`
`var employees : EmployeeSet`
* Prevents the effort of writing `Set<Employee>` everytime.

### 20. Quick Differences Between Kotlin and Java

* Dont have to put Semicolons at the end of the statement.
* Kotlin has Wrappers. `println` is a Kotlin wrapper around Java's `System.out.println`
* Hard and Soft Keywords
* [] Square brackets can be used to access elements in the collection. e.g. println(names[1])
* Kotlin has its own String class. Kotlin does not use java.lang.String.
* Kotlin does not distinguish between Checked and UnChecked Exception. throws keyword does not exist in Kotlin. All exceptions are UnChecked.
* Kotlin does not have Terniary Operator. It is replaced with If. If is an expression in Kotlin.
* Java like for loops i.e. for(i=0; i<10; i++) does not exist in Kotlin.
* Kotlin does not have a static keyword. But concept of static is still there.
* Kotlin does not have `new` keyword. e.g. `var employee1 = Employee("Priyanka Chaudhary", 111)`

### 21. How Kotlin handles equality differently from Java

In Java, 
* `==` operator looks for `Referential Equality`
* `equals` operator looks for `Structural Equality`

In Kotlin,
* `==` operator looks for `Structural Equality` 
* `===` operator looks for `Referntial Equality` 

* For checking if both the instances have the same value use the `==` operator.
* For checking if both the instances refer to the same instance use the `===` operator.

### 22. Bit Operators and Smart Casting in Kotlin

`Smart Casting`

Java :: `instanceOf`
Kotlin :: `is` & `as`

```
    val name: Any = "The Any type is the root of the Kotlin Type Hierarchy"

    if(name is String){
        println("Uppercase string : ${name.toUpperCase()}")
    }
```

### 23. String Templates in Kotlin

`String Templates`

val change = 4.22
* println("$change")
`O/P - 4.22`
* println("\\$change")
`O/P - $change`
* println("$$change")
`O/P - $4.22`

val numerator = 10.11
val denominator = 20.22
* `O/P - println("$numerator divided by $ denominator is ${numerator/denominator}")`

Printing object properties
* `O/P - println("Employee One is ${employeeone.id}")`

### 24. Raw Strings in Kotlin

`Raw Strings or Triple Quoted Strings`
* `String filePath = "C:\\SHREYAS\\2.Git"` OR `String filePath = """C:\SHREYAS\2.Git"""`
* Triple Quoted String
```
println("""   1
        |  11
        | 111
        |1111
    """.trimMargin())
```
No need of new line characters.
* `trimMargin("|")` - For proper indentation in the code
* The `Any type` is the root of the Kotlin Type Hierarchy

### 25. The Kotlin REPL

`REPL` - [R]ead [E]val [P]rint [L]oop
