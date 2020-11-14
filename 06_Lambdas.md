# Lambdas

코틀린에서는 기본적으로 람다를 제공하고있음.

```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View view) {
        view.setAlpha(0.5f);
    }
});
```

위와같은 java 코드가 **setOnClickListener 의 구현해야하는 메소드가 한가지(`onClick()`) 뿐이기에** 아래와 같이 3줄로 줄어들 수 있음

```kotlin
button.setOnClickListener {
    view -> view.alpha = 0.5f
}
```

또 한번 더, `onClick()` 메소드가 `싱글 파라미터`(한가지의 파라미터만을 가지는 메소드) 이기에 `it` 키워드를 사용하여 아래와 같이 생략 가능함

```kotlin
button.setOnClickListener {
    it.alpha = 0.5f
}
```

## Closure

`Closure` 란 내부의 컨텍스트에서 바깥에 있는 컨텍스트에 접근하는것. 코틀린은 `closure` 가 제공되기때문에 아래와 같이 사용하면 됨

```kotlin
var count = 0
button.setOnClickListener {
    count++
}
// or
var sum = 0
ints.filter { it > 0 }.forEach {
    sum += it
}
```

위 코틀린 코드를 디컴파일 시 기존 java 에서 외부 컨텍스트에 접근하듯 배열을 만들어 접근함.

## return

```kotlin
button.setOnTouchListener { view, motion Event ->
    // 함수 내 마지막 줄이 return에 해당한다
    true
}
```

## stream

`filter`, `map` 키워드로 구현

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
list.filter { item -> item > 5 }.map { item -> Log.d("TAG", "index ${item * 2}") }
```

역시, 아래처럼 `item` 을 지우고 `it`으로 대체 가능

```kotlin
val list = mutableListOf(1, 2, 3, 4, 5)
list.filter { it > 5 }.map { item -> Log.d("TAG", "index ${it * 2}") }
```

## map

`forEach` 로 손쉽게 접근

```kotlin
val map = mutableMapOf(1 to "value", 2 to "value", 3 to "value")
map.forEach { item ->
    println("Key ${item.key} value ${item.value}")
}
```

아래처럼 `item` 을 지우고 `it` 대체 가능

```kotlin
val map = mutableMapOf(1 to "value", 2 to "value", 3 to "value")
map.forEach {
    println("Key ${it.key} value ${it.value}")
}
```

> forEach { key, value -> } sms minSdk **21 이상**에서 사용 가능
