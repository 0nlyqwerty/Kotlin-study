# Kotlin 에서 `findViewById` 시

```Kotlin
// 1
val navView1 = findViewById(R.id.nav_view) as BottomNavigationView

// 2
val navView2 = findViewById<BottomNavigationView>(R.id.nav_view)

// 3
val navView3: BottomNavigationView = findViewById(R.id.nav_view)
```

위와 같이 세가지 모두 사용 가능함.

> 단, 첫번째 방법으로 `findViewById` 시도 시 두번째 방법을 추천함.

사실,

```Kotlin
apply plugin: 'kotlin-android-extensions'
```

를 사용하면 `findViewById` 할 필요도 없음.

```Kotlin
message.text = "set text"
```

처럼.
