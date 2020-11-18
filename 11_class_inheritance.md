# 클래스 상속(class inheritance)

## open class

코틀린은 class에 `open` 키워드를 붙이지 않으면 기본적으로 `final` 이다. 그러므로 클래스의 `상속` 을 하기 위해서는 `open` 키워드로 `final` 키워드를 제거해주어야한다

```kotlin
open class Empty(a: Int)
class Sample(a: Int) : Empty()
```

## java View class 상속

ConstraintLayout 상속받는 코드를 예시로 생성자 연습

```kotlin
// secondary 생성자 활용
class CustomConstraintLayout(
    context: Context,
    attrs: AttributeSet?,
    defStyleAttr: Int)
: ConstraintLayout(context, attrs, defStyleAttr) {
    constructor(context: Context, attrs: AttributeSet?) : this(context, attrs, 0)
    constructor(context: Context) : this(context, null)
}
```

```kotlin
// default 값을 추가하여 secondary 생성자 제거
class CustomConstraintLayout(
    context: Context,
    attrs: AttributeSet? = null,
    defStyleAttr: Int = 0)
: ConstraintLayout(context, attrs, defStyleAttr) {
}
```

## abstract

```kotlin
abstract class Base(val a: Int)

class Sample(a: Int) : Base(a)
```

주의해야할점은, 추상클래스 안에 존재하는 함수여도 재정의가 필요하다면 `open` 키워드를 붙여야한다

## interface

#### java

- `default` : 기본 함수를 구현할 수 있다
- `static` : 기본 함수를 구현하고, `static` 으로 접근할 수 있다
- 항상 상속받을 수 있는 형태
- final 변수 선언 가능(상속시 값을 변경할 수 없음)

#### kotlin

- final 정의를 하지 못하고, 반드시 상속에서 구현해야함
- 별도의 키워드 없이 default 메소드와 정의 가능
  - open 정의 없이 모두 확장 가능
