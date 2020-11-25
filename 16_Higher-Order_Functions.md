# Higher-Order Functions

**함수를 파라미터로 전달**하거나, **함수를 리턴**하는 기능
`lambda`를 통해 축약 형태로 제공하고, 변수로 함수 또한 가질 수 있다

```kotlin
// Higher-Order Functions 샘플
fun <T> lock(lock: Lock, body: () -> T): T {
    lock.lock()
    try {
        return body()
    }
    finally {
        lock.unlock()
    }
}
```

## Higher-Order Functions 을 분리하기

- 파라미터 이름 : `body`
- 정의 : `() -> T`
- 실제 정의 : `f() -> T`

> **T가 리턴이 되는 f 메소드**

## Higher-Order Functions 사용하기

```kotlin
fun toBeSynchronized() = sharedResource.operation()
val result = lock(lock, ::toBeSynchronized)
```

메소드인 `toBeSynchronized` 자체를 넘겨주고있음

## 파라미터 정의

### 파라미터가 없을 경우

```kotlin
fun print(body: () -> String) {
    println(body())
}

@Test
fun test() {
    print({ "return message" })
}
```

### 파라미터가 1개인 경우

```kotlin
fun print(body: (String) -> String) {
    println(body("print message"))
}

@Test
fun test() {
    print({ message ->
        "$message return message"
    })
}
```

### 파라미터가 1개 이상인 경우

```kotlin
fun print(body: (Int, String) -> String) {
    println(body(1, "message"))
}

@Test
fun test() {
    print({ int, message ->
        "$int, $message return message"
    })
}

// 마지막 Higher-Order Functions 에서는 아래와 같이 괄호 () 의 제거가 가능하다
@Test
fun test() {
    print { int, message ->
        "$int, $message return message"
    }
}
```

## Higher-Order Functions 가 2개인 경우

```kotlin
fun print(body: (Int, String) -> String, body2: () -> String) {
    println(body(1, "message"))
}

@Test
fun test() {
    print({ int, message ->
        "$int, $message return message"
    },{"body 2"})
}

// 역시 마지막 Higher-Order Functions 는 괄호 생략 가능
@Test
fun test() {
    print({ int, message ->
        "$int, $message return message"
    }) {"body 2"}
}
```

## 다른 메소드를 직접 호출하기

```kotlin
fun print(body: (Int, String) -> String) {
    println(body(1, "message"))
}

fun message(a: Int, b: String) = "$a $b"

@Test
fun test() {
    print { int, message -> message(int, message)}
}

// 아래와 같이 직접 호출하는 키워드 `::` 를 사용 또한 가능함
// 단, 타입이 맞지 않다면 람다식으로 사용 불가능함
@Test
fun test() {
    print(::message)
}
```

## 변수에 Higher-Order Functions 정의하기

코틀린에서는 `var` 에서 `getter`, `setter` 가 자동으로 만들어지기 때문에, 아래와 같이 뒷부분에 Higher-Order Functions 를 정의하면 됨

```kotlin
var higherOrderFunction: () -> Unit = {
    println("Print!!!")
}

@Test
fun test() {
    higherOrderFunction()
}
```

강사님은 여기에 `lateinit` 을 사용하여 `OnClickListener`를 자주 구현함

```kotlin
lateinit var higherOrderFunction: (String) -> Unit

@Test
fun test() {
    higherOrderFunction = {
        println("Print!!!")
    }
    higherOrderFunction("")
}
```

## Higher-Order Functions 를 사용한 사칙연산

```kotlin
@Test
fun test() {
    println(higherOrder { i, i2 -> i + i2 })
    println(higherOrder { i, i2 -> i - i2 })
    println(higherOrder { i, i2 -> i * i2 })
    println(higherOrder { i, i2 -> i / i2 })
}
fun higherOrder(body: (Int, Int) -> Int) = body(20, 10)
```

원래 형태는 아래와 같을것임

```kotlin
@Test
fun test() {
    println(higherOrder(::sum))
    println(higherOrder(::minus))
    println(higherOrder(::multiply))
    println(higherOrder(::division))
}

fun higherOrder(body: (Int, Int) -> Int) = body(20, 10)
fun sum(a: Int, b: Int) = a + b
fun minus(a: Int, b: Int) = a - b
fun multiply(a: Int, b: Int) = a * b
fun division(a: Int, b: Int) = a / b
```
