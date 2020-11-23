# Sealed Classes

## 다형성이란

- 부모 클래스를 상속받은 자식 클래스
- 자식 클래스는 부모 클래스로부터 접근할 수 있다
- 이때 자식 클래스는 모두 다른 행동을 할 수 있다

`java` 에서 `extends` 및 `@override` , `super` 키워드로 다형성 구현 가능

## Kotlin 에서의 Sealed class 는?

- 첫번째 조건은 생성자는 `private` 이어야 한다.
  아래처럼 변수는 가질 수 있으나, `private` 이기에 같은 파일 위치에 이를 상속받는 클래스가 정의되어야함.

```kotlin
// 즉, 다른 파일에 정의할 수 없음
sealed class Sample(val a: Int)
data class Num : Sample()
data class Num2 : Sample()
```

- 아래와 같이 sealed class {} 안에 class 를 정의 할 수도 있음

```kotlin
sealed class Sample {
    data class Num : Sample()
    data class Num2 : Sample()
}
```

- `abstract` 메소드 생성 또한 가능

```kotlin
sealed class A {
    abstract fun printA()
}
```
