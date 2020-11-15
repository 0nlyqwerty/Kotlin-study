# Return, Jumps, This Expression

## Jump Expression

return : 반환할 때  
break : 빠져나갈때  
continue : 특정 조건에 대해서만 처리하지 않을 때.  
이러한 jump expression을 label 과 함께 사용했을때 어떻게 달라지는지 확인

### Label 정의

정의할 때 : `name@`  
사용할 때 : `@name`

### Break and Continue Labels

```kotlin
loop@ for (i in 1..100) {
    for (j in 1..100) {
        if (j > 10) break@loop
        print(j)
    }
    println()
}
println("end")
```

output: 12345678910end

## Return at Labels

```kotlin
vak ints = mutableListOf(1, 2, 0, 4, 5)
fun foo() {
    ints.forEach lit@ {
        if (it == 0) return@lit
        print(it)
    }
}
//output: 1234
```

아래와 같이 `lambda` 식으로 `forEach` 를 부를 수 있음

```kotlin
val ints = mutableListOf(1, 2, 0, 4, 5)
fun foo() {
    ints.forEach {
        if (it == 0) return@forEach
        print(it)
    }
}
```

## This Expression

아래 경우 `this`는 클래스(`Sample`)를 가리키며, `temp1` 와 `temp2`는 동일한 결과를 가지게 됨

```kotlin
class Sample {
    val temp1 = this@Sample
    val temp2 = this
}
```

\+

```kotlin
class Sample {
    fun Int.foo() {
        val a = this@Sample // Sample class를 가리킴
        val b = this        // 메소드 내부의 의 Int 를 가리킴
        val c = this@foo    // 메소드 내부의 의 Int 를 가리킴
    }
    fun test(a: Int) {
        a.foo()
    }
}
```
