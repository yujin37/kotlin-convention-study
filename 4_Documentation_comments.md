# 문서 주석

긴 문서 주석의 경우 여는 표시인 `/**` 를 별도의 줄에 넣고 이후의 각  줄을 별표로 시작해라.

```kotlin
/**
 * This is a documentation comment
 * on multiple lines.
 */
```

짧은 주석은 단일 줄에 위치할 수 있다. 

```kotlin
/** This is a short documentation comment. */
```

일반적으로 `@param`과 `@return` 태그를 사용하는 것을 피해라. 대신에, 매개변수와 반환 값 설명을 문서 주석에 직접적으로 포함시키고 언급할 때마다 매개변수에 링크를 추가해라. `@param`과 `@return` 는 긴 설명이 요구되고 본문 내용의 흐름에 맞지 않을 때에만 사용해라. 

```kotlin
// Avoid doing this:

/**
 * Returns the absolute value of the given number.
 * @param number The number to return the absolute value for.
 * @return The absolute value.
 */
fun abs(number: Int): Int { /*...*/ }

// Do this instead:

/**
 * Returns the absolute value of the given [number].
 */
fun abs(number: Int): Int { /*...*/ }
```
