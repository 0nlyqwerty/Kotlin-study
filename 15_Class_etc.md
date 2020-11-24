# Class etc

## Data class

`getter`, `setter`, `toString` 등을 자동으로 생성시켜주는 `data` 키워드 존재

```kotlin
data class UserInfo(var temp: String?, var name: String?, var age: Int?)
```

## 싱글톤 구현

기본 싱글톤은 `object` 를 사용하여 간단하게 구현 가능하다.

```kotlin
object Eager
```

클래스가 생성될때 자동으로 `instance`가 초기화됨

> 단 위와 같이 구현 할 경우 `생성자` 를 가질 수 없다. 디컴파일 시 `private` 으로 정의되어있고, `object` 클래스는 생성자를 가질 수 없도록 구현되어있기때문임.

그렇기에, 아래(구글 샘플 - Singleton)와 같이 구현 시 생성자를 가질 수 있으며 일반 클래스에서도 사용 할 수 있다

```kotlin
class Singleton private constructor(val name: String) {
    companion object {
        @Volatile private var INSTANCE: Singleton? = null

        fun getInstance(name: String): Singleton =
            INSTANCE ?: synchronized(this) {
                INSTANCE ?: Singleton(name).also { INSTANCE = it }
            }
    }
}
```

또, 아래와 같이 `Lazy` 패턴을 사용하여 초기화 할 수 있으나, 위 `val name: String` 처럼 값을 넘겨줄수는 없으니 잘 선택해서 구현하면 된다

```kotlin
class Lazy {
    companion object {
        private val INSTANCE: Lazy by lazy {
            lazy()
        }

        @JvmStatic fun getInstance() = INSTANCE
    }
}
```

## class 안에 class 정의하기

### Nested class

java 의 `static class` 와 같음

```kotlin
class Outer {
    private val bar: Int = 1
    class Nested {
        fun foo() = 2
    }
}

// 접근
val demo = Outer.Nested().foo() // == 2
```

`Outer` 의 객체는 생성하지 않으나 `Nested` 의 객체는 생성해야 `foo` 에 접근이 가능하다

> 즉, 기본값이 `Nested class` (`static class`) 이다.

### inner class

`Nested class` 가 기본값인 상태에서, `inner class` 를 정의하기 위해서는 아래와 같이 `inner` 키워드를 사용해준다

```kotlin
class Outer {
    private val bar: Int = 1
    inner class Inner {
        fun foo() = bar
    }
}

// 접근
val demo = Outer().Inner().foo() // == 1
```

### Anonymous inner classes (익명클래스, object class)

명시적으로 object를 받아 상속임을 표시해줘야하며, 이때 object는 해당 추상클래스 혹은 인터페이스에 해당된다  
이는 `OnClickListener` 혹은 직접 구현한 `Listener` 에서 많이 사용하게될것이다  
또한 `Glide 라이브러리` 에서도 사용할때 `obeject` 키워드 하나로 유용하게 사용된다

```kotlin
fun test() {

    setOnClick(object : OnClick {
        override fun onClickTwo() {
            // TODO finish implement
        }
    })
}

fun setOnClick(onClick: OnClick) {
}

interface OnClick {
    fun onClickTwo()
}
```
