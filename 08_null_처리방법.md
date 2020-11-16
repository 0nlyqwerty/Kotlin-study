# null 처리방법

## Null 처리

**자바**

- (기본적으로)null을 허용한다
- Annotation 으로 `@NonNull`, `@Nullable` 지정 가능

```java
public void set(@NonNull String a, @Nullable String b) {
    // ...
}
```

Annotation을 사용할 수 있으나 아래 코드 또한 사용 가능

```java
set(null, null);
```

**코틀린**

- (기본적으로)null을 허용하지 않음
- null을 명시적으로 나타내기 위해서 `?`을 추가해야한다
- 자바와 달리 IDE 에서 null을 사용할 수 없음을 즉시 알려줌

```kotlin
fun set(a: String, b: String?) {
    // ...
}
```

null을 허용하지 않은 변수인 `a` 에 null을 대입하면 IDE 단에서 즉시 오류가 발생함. 아래와 같은 코드 사용 불가

```kotlin
set(null, null)
```

## Null 체크 - safe Calls

기존 자바에서처럼 `if` 문을 쓸 수 있으나

```kotlin
var temp: String? = null
var size = 0
if (temp != null) {
    size = temp.length
}
```

아래와 같이 safe call을 사용하면 더 편하다

```kotlin
var temp: String? = null
val size = temp?.length
// output: null
```

### safe calls 의 장점

기존 java의 null check

```java
if (aaa != null && aaa.bbb != null && aaa.bbb.ccc != null) {
    return aaa.bbb.ccc.name;
}
return null;
```

코틀린의 null check

```kotlin
return aaa?.bbb?.ccc?.name  // 어느 하나라도 null 인 경우 null 리턴
```
