# Section 8 : File IO

### 76. Reading Text Files

* Kotlin does not have its own IO classes. It makes use of `java.io`
* It has Extension function to the existing Java IO classes.
* `File` - java.io & `reader()` - Kotlin.io
```
import java.io.File

fun main(args: Array<String>){

    val lines = File("TestFiles.txt").reader().readLines()
    //File - from java.io
    //reader() - Extension function from kotlin.io

    lines.forEach { println(it) }

}
```
```
import java.io.File

fun main(args: Array<String>){

    File("TestFiles.txt").reader().forEachLine { println(it) }

}
```

### 77. Reading Binary Files

### 78. Walking the File Tree

`Walking a tree`
* `.walkTopDown()` - Directories are visited before the files.
```
import java.io.File

fun main(args: Array<String>){

    File(".").walkTopDown().forEach { println(it) }

}
```
* Files that end with .kt extension.
```
fun main(args: Array<String>){

    File(".")
        .walkTopDown()
        .filter { it.name.endsWith(".kt") }
        .forEach { println(it) }

}
```