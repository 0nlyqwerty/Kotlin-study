# Companion

## class companion object

일반적인 클래스의 변수와 메소드를 직접 접근할 수 있도록 만들어주는것.  
간단히 말하면 `java의 static` 형태로 접근이 가능한 변수와 메소드를 만들어주는것

- class 내에 정의할 수 있음
- Java 에서처럼 Class.TYPE 형태로 직접 접근 가능
- static은 아님

```kotlin
// class 내에 직접 접근을 위한 함수와 변수 정의
class Sample {
    val name: String = "Name"

    companion object {
        val type: Int = 0

        fun isTypeZero(): Boolean {
            return type == 0
        }
    }
}
```

## interface와 함께 사용

```kotlin
interface Base {
    val name: String
    fun newDefaultMethod()

    companion object {
        val TYPE: Int = 0
        fun isTypeZero(): Boolean {
            return TYPE == 0
        }
    }
}
```

## companion object 접근

```kotlin
// 변수 접근
Base.TYPE

// function 접근
Base.isTypeZero()
```

Companion 사용않고 java static 변수처럼 접근하기 위해서는

- 변수 : const/@JvmField
- function : @JvmStatic

코틀린에서 제공하는 위 어노테이션 사용

```kotlin
class Base {
    companion object {
        const val TYPE: Int = 0
        @JvmField val NAME: String = "Name"
        @JvmStatic fun isTypeZero(): Boolean {
            return TYPE == 0
        }
    }
}
```

## companion object 이름 지정

```kotlin
class MyClass {
    companion object Factory {
        fun create(): MyClass = MyClass()
    }
}

// Kotlin에서 접근 시
MyClass.create()
// Java에서 접근 시
MyClass.Factory.create()
```
