# null 예외처리

## Elvis Operator

`Elvis Operator` : `?:`  
java 의 삼항연산자에서 `?` 와 `:` 를 따로 쓰는것과 비교해서, 붙어있음

```kotlin
var temp: String? null
// 1. if / else 사용 가능
// 2. safe call 사용 가능

// 3. Elvis Operator
val size = temp?.length ?: 0
// output : 0 | length
```

### Elvis Operator 유용하게 사용하기

```java
// JAVA
String temp = null;
textView.setText(temp != null ? temp : "");
```

```kotlin
// KOTLIN
val temp: String? = null
// textView.text = if (temp != null) temp else ""
textView.text = temp ?: ""
```

## NPE(Null Pointer Exception)

### NPE 발생시키는 방법

1. `!! Operator` 사용

null인 경우 자동으로 NPE을 발생시킨다

```kotlin
val temp: String? = null
val size = temp!!.length    // npe 발생
```

`try/catch` 가 필요한 경우 사용하면 됨.

```kotlin
val size = try {
    temp!!.length
} catch (e: NullPointerException) {
    0
}
```

2. `Elvis Operator` 사용

```kotlin
val temp: String? null
val size = temp?.length ?: throw NullPointerException("temp is null")
```

> **이러니저러니해도, Java 와 Kotlin 을 같이 쓸때는 주의해야함**
