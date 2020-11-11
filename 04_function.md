# Function

## Defining functions

1. 리턴값이 없는 경우

```kotlin
fun 함수명(변수): Unit {    // Unit 생략 가능
    값 처리
}
```

2. 리턴값이 있는 경우

```kotlin
fun 함수명(변수): 리턴타입 {
    return 값
}
```

아래와 같이 한줄로 되어있는 단순한 함수라면 return 의 생략이 가능하며, 유추하기를 통해 리턴타입 또한 생략 할 수 있음

```kotlin
fun getSum(a: Int, b: Int): Int {
    return a + b
}

// return 생략
fun getSum(a: Int, b: Int): Int = a + b

// 유추하기를 통한 생략
fun getSum(a: Int, b: Int) = a + b
```

## Extension Functions

함수를 확장하여 기존에 있던 것처럼 사용할 수 있음.

> 단, Extenstion 보다 Class 내에 있던 원래 함수가 우선순위가 높음

```kotlin
fun 타입.함수명(변수): 리턴 타입 {
    return 값
}
```

위와 같은 형태로 만들 수 있으며, 기존 `타입` 에 정의되어있는 함수처럼 `타입` 을 통해 접근하는 함수만 노출됨

```kotlin
fun Int.max(x: Int): Int = if (this > x) this else x

// 사용 시
숫자.max(숫자)

// 예시
print(1.max(15))   // output:15
print(5.max(2))    // output:2
```

### infix notation

Extension Function 에서 변수가 1개만 있을 경우 아래와 같이 함수 앞에 `infix` 키워드를 추가하여 더욱 축약 가능

```kotlin
infix fun Int.max(x: Int): Int = if (this > x) this else x

fun test() {
    1.max(15)
    1 max 15
}
```

## Extenstion Properties

`Function Extension` 으로도 구현이 가능하나 Property 자체 또한 간단히 확장해줄 수 있음

```kotlin
val <T> List<T>.lastIndex: Int
    get() = size - 1
```

## Named Arguments

```kotlin
fun setParams(age: Int, name: String = "Default") {
    // ...
}

// 사용
setParams(email = "email@email.com", age = 10)
```

key - value 로 전달됨
