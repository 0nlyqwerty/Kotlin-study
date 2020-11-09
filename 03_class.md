# Class

## 생성자

```kotlin
class 클래스이름 constructor(변수){
}
```

또한 아래와 같이 다중 생성자를 가질 수 있음

```kotlin
class Sample constructor(val name: String, val arg: Int) {
	constructor(name: String) : this(name, 0)
}
```

class 를 정의함과 동시에 오는 생성자를 `primary constructor` 라 부르고,  
그 이외의 생성자들을 `secondary constructor` 라 부른다.

**`primary constructor`**

1. 아래와 같이 `constructor` 생략 가능하다

```kotlin
class Sample (val name: String, val age: Int) {
	...
}
```

2. 자바 생성자와 다르게 변수에 대한 타입을 바로 가질 수 있으며 이 변수들은 `전역변수` 로 취급된다.

**`secondary constructor`**

1. `constructor` 문구 생략 불가능하다
2. **반드시** `this` 에 값을 넘겨줘야함. 넘겨주지 않을 경우 오류 발생

---

## default 생성자

아래와 같이 생성자의 인자에 default 값을 넣을 수 있다

```kotlin
fun test() {
	Sample(age = 2)
}

class Sample(val name: String = "Name", val age: Int) {
}
```

---

## init

```kotlin
fun test() {
	Sample("me")
}

class Sample(val name: String, val age: Int) {
	constructor(name: String) : this(name, 0) {
		println("> name $name, age $age")
	}

	init {
		println(">> name $name, age $age")
	}
}
```

이때, 아래와 같은 출력이 나옴

```
>> name me, age 0
> name me, age 0
```

`init` 블럭이 먼저 호출됨

_주의해야할점_

- 생성자는 `primary constructor` 를 통해서만 전역변수 생성이 가능함. `secondary constructor` 는 단순히 생성자만 가지는게 유용함

---

## Class 생성자에서의 초기화

```kotlin
fun test() {
    Customer("name")
}
class Customer(name: String) {
    val customerName = name.toUpperCase()
    init {
        print("name $name, customerName $customerName")
    }
}
```

이때, 아래와 같은 출력이 나옴

```
name name, customerName NAME
```

---

## Class 상속 - kotlin:abstract

```kotlin
abstract class Base(age: Int)

class UseBase(age: Int) : Base(age)
```

---

## Class 상속 - kotlin:interface

```kotlin
interface Base {
	fun getName(): String
}

class UseBase : Base {
	override fun getName() = "name"
}
```

---

## 상속 종합 예제

```kotlin
class ExampleUnitTest {
    @Test
    @Throws(Exception::class)
    fun test() {
        var customerAge = Customer(23).getCustomerAge()
        print("CUSTOMER AGE : $customerAge")
    }

    abstract class AbstractBase(val age: Int)

    interface InterfaceBase {
        fun getCustomerAge(): Int
    }

    class Customer(age: Int) : InterfaceBase, AbstractBase(age) {
        override fun getCustomerAge(): Int = this.age
    }
}
```

---

## class open

코틀린에서는 abstract/interface 를 제외한 모든 클래스는 `final` 이다  
그렇기때문에 코틀린은 기본적으로 클래스와 메소드 확장이 불가능한 형태이나, 아래 코드와 같이 `open` 키워드로 가능하게 만들어 줄 수 있음

```kotlin
...
open class Customer(age: Int) : InterfaceBase, AbstractBase(age) {
	override fun getCustomerAge(): Int = this.age
}

class User(age: Int) : Customer(age) {

}
```
