# 유용한 null 처리 방법

## 안전한 형 변환

1. Java 의 경우  
   `instanceof` 키워드를 사용하여 안전하게 처리

```java
Object object = "name"; // String
int index = 0;
if (object instanceof Integer) {
    index = (int) object;
}
System.out.println("index " + index);
// output: 0
```

2. Kotlin 의 경우

- `as`(casting) 뒤에 `?` 키워드를 붙여 안전하게 형 변환

```kotlin
val a: Any? = "ABC"

val b: Int? = a as Int
// Cast Exception 발생

val b: Int? = a as? Int
// output: null

val b: Int? = a as? Int ?: 0
// output: 0
```

- `when` 을 사용하여 안전한 처리

```kotlin
val a: Any? = "ABC"
when (a) {
    is Int -> println(a)
    is String -> println(a)
    else -> println("nothing")
}
```

## list에서 null 아이템 제외하기

```kotlin
val listWithNulls: List<String?> = listOf("A", null, "B")
for (item in listWithNulls) {
    if (item != null) {
        println("Text : $item")
    }
}

// lambda
val listWithNulls: List<String?> = listOf("A", null, "B")
listWithNulls.filter { it != null }.forEach { println("Text : $it") }
```

## filterNotNull 이용하기

코틀린에서는 필터를 별도로 정의하지 않아도 `null`을 체크할 수 있는 `filterNotNull()`가 제공이 됨

```kotlin
val listWithNulls: List<String?> = listOf("A", null, "B")
val itemList: List<String> = listWithNulls.filterNotNull()
itemList.forEach {
    println("Text : $it")
}
```

## block 을 이용한 null 예외처리

```kotlin
data class Sample(val name: String, val age: Int, val id: String)

fun test() {
    val sample: Sample? = Sample("User name", 20, "userId")

    // case 1
    tvName.text = sample?.name ?: ""
    tvAge.text = sample?.age ?: 0
    tvId.text = sample?.id ?: ""

    // case 2 : use let
    sample?.let {
        tvName.text = it.name
        tvAge.text = it.age
        tvId.text = it.id
    } ?: let {
        println("sample is null")
        tvName.visibility = View.GONE
        tvAge.visibility = View.GONE
        tvId.visibility = View.GONE
    }
}
```

## 1개 이상의 null 체크

```kotlin
// 1개 변수의 null 체크
val a: String? = "ABC"

// a가 null 이 아닐 때 block 내부 실행. it과 this의 차이
a?.let { println(it.length) }
a?.run { println(this.length) }
a?.apply { println(this.length) }
```

**1개 이상의 null 체크 라이브러리 ↓**

1. Safe Let  
   [Multiple variable let in Kotlin](https://stackoverflow.com/a/35522422)
2. Unwrap  
   [kotlin-unwrap](https://github.com/importre/kotlin-unwrap)
