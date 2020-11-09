# 비교

메모리의 비교에는 `===` 사용

```kotlin
val a: Int = 10_000
print(a === a)    // 'true'
val b: Int? = a
val c: Int? = a
print(b === c)    // 'false'
```

값의 비교에는 `==` 사용

```kotlin
val a: Int = 10_000
print(a == a)    // 'true'
val b: Int? = a
val c: Int? = a
print(b == c)    // 'true'
```

# var / val

var (mutable)

- read / write 모두 가능

val (immutable)

- java 의 final. read 가능하나 write 불가능함

# null

자료형 뒤의 ?

- Nullable! 심지어 safecall 하지 않으면 `.length` 호출도 안됨  
  자료형 뒤에 ?가 없는 경우
- @NotNull

# Nothing 과 Any

Nothing

- 어떤 값도 가질(초기화 할) 수 없음
- `val nul = null` 은 `val nul:Nothing? = null` 과 같음

Any

- 어떤 값이라도 가질(초기화 할) 수 있음
- java 의 Object와 같음

# 늦은 초기화

`by lazy`

- 호출 시점에 초기화.
- val (immutable)과 함께 사용

```kotlin
val name: String by lazy {
    "-"
}
```

`lateinit`

- 사용 전에 초기화 하지 않으면 에러 발생
- var (mutable)과 함께 사용

```kotlin
lateinit var name:String
```
