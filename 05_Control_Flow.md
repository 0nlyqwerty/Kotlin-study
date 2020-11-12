# Control Flow

## if, else

java 와 비슷하다

```kotlin
// 활용1
fun test() {
    val a = 10
    val b = 20
    val max = if (a > b) a else b
}

// 활용2
fun test() {
    val a = 10
    val b = 20
    val max: Int
    val min: Int
    if (a > b) {
        max = a
        min = b
    } else {
        max = b
        min = a
    }
}
```

## when

코틀린에는 `switch` 문이 존재하지 않기에 아래와 같이 `when` 사용

```kotlin
val a = 10
when (a) {
    1, 10 -> // ...
    else -> // ...
}
```

> 맨 마지막 else 는 반드시 붙어야함

### in, !in

또한, `in` 밑 `!in` 키워드로 포함, 포함되지 않은 경우 또한 분기 가능

```kotlin
val validNumbers = 9..10
val a : Any = 30
when (a) {
    in 1..10 -> println("1~10")
    in validNumbers -> println("validNumbers")
    !in 10..20 -> println("a is outside the range")
    else -> println("else")
}
// output: a is outside the range
```

### is

`is` 키워드로 `instaceof` 또한 분기 가능

```kotlin
val a = "message"
when (a) {
    1, 10 -> println("1~10")
    is String -> println(a)
    else -> println("else")
}
//output: message
```

### when의 return

아래와 같이 return 가능

```kotlin
fun isString(a: Any) = when (a) {
    is String -> true
    else -> false
}
println(isString("message"))
//output: true
```

아래와 같이 `data class` 처리에 활용 또한 가능

```kotlin
class ExampleUnitTest {

    @Test
    @Throws(Exception::class)
    fun test() {
        printSample(SampleOne("test"))
        printSample(SampleTwo(20))
    }

}

fun printSample(sample: Sample) {
    when (sample) {
        is SampleOne -> println("One ( String )")
        is SampleTwo -> println("Two ( Int )")
    }
}

sealed class Sample
data class SampleOne(val name: String) : Sample()
data class SampleTwo(val age: Int) : Sample()
```

## For

```kotlin
// for i 문
val name = "name"
for (i in name) {
    println("i $i")
}

// list 형태
val list = mutableListOf(1, 2, 3, 4, 5)
for (i in list) {
    println("i $i")
}
```

### list 에서 index 필요 시

`indices` 키워드 사용 시 가져올 수 있음

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
for (i in list.indices) {
    println("i ${list[i]}")
}
```

### list 에서 index 와 value 모두 필요할 시

`withIndex()` 사용

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
for ((index, value) in list.withIndex()) {
    println("$index $value")
}
```

### break

자바와 동일하게 `break` 키워드 사용

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
for ((index, value) in list.withIndex()) {
    println("$index $value")
    if (index == 1) {
        break
    }
}
```

### step

`step` 키워드 사용하여 점프할 수 있음

```kotlin
for (value in 1..10 step 2) {
    println("value: $value")
}
```

### map

아래와 같이 `map` 데이터형을 for 문으로 사용 시 k-v 형태로 가져올 수 있음

```kotlin
val map = mutableMapOf(1 to "ABC", 2 to "BBB", 3 to "CCC")
for ((key, value) in map) {
    println("key:$key value:$value")
}
```
