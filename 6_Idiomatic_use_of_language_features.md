# 언어 기능의 관용적인 사용

## 불변성

변경 가능한 데이터보다는 변경불가능한 데이터를 사용하는 것이 선호된다. 초기화 이후에 수정하지 않는다면 `var`보다는 `val`을 사용하여 항상 로컬 변수와 매개변수를 선언해야 한다. 

변경하지 않는 컬렉션을 선언할 때는 항상 불변 콜렉션 인터페이스(`Collection`, `List`, `Set`, `Map`)를 사용해라.

콜렉션 인스턴스를 만들기 위해 팩토리 함수를 사용할 때 항상 가능한한 불변 콜렉션 유형으로 반환하는 함수를 사용해라. 

```kotlin
// 나쁜 예: 변경되지 않을 값에 대해 가변 컬렉션 유형을 사용
fun validateValue(actualValue: String, allowedValues: HashSet<String>) { ... }

// 좋은 예: 변경되지 않을 값에 대해 불변 컬렉션 유형을 사용
fun validateValue(actualValue: String, allowedValues: Set<String>) { ... }

// 나쁜 예: arrayListOf()는 ArrayList<T>를 반환하며, 가변 컬렉션 유형이다.
val allowedValues = arrayListOf("a", "b", "c")

// 좋은 예: listOf()는 returns List<T>를 반환한다.
val allowedValues = listOf("a", "b", "c")
```

## 기본 매개변수 값

오버로드된 함수를 선언하는 것보다 기본 매개변수 값을 가진 함수를 선언하는 것이 좋다.

```kotlin
// 나쁜 예
fun foo() = foo("a")
fun foo(a: String) { /*...*/ }

// 좋은 예
fun foo(a: String = "a") { /*...*/ }
```

## 타입 별칭

만약 함수형 유형 혹은 코드베이스에서 여러번 사용되는 유형 매개변수를 가진 유형을 가진다면 해당 타입에 타입 별칭을 정의하는 것이 좋다.

```kotlin
typealias MouseClickHandler = (Any, MouseEvent) -> Unit
typealias PersonIndex = Map<String, Person>
```

만약 이름 충돌을 피하기 위해 비공개(private) 혹은 내부(internal) 타입 별칭을 사용한다면 패키지(Packages) 및 임포트(Imports) 에서 `import … as …`로 사용하는 것이 좋다.

## 람다 매개변수

짧고 중복되지 않은 람다식에서는 명시적으로 매개변수를 선언하는 대신에 `it` 규칙을 사용하는 것을 추천한다. 매개변수를 가진 중첩된 람다식에서는 항상 명시적으로 파라미터를 선언해야 한다. 

## 람다식에서의 반환문

람다식에서 여러 레이블이 사용된 반환문을 피해라. 람다식을 재구조화하여 단일 종료 지점을 가지는 것을 고려하는 것이 좋다. 만약 불가능하거나 충분히 명확하지 않다면 람다식을 익명함수로 전환하는 것을 고려해라. 

람다식에서 마지막 문장을 레이블이 지정된 반환문을 사용하지 마라.

## 명명된 인자

여러 원시 타입 매개변수를 가지는 메서드나 Boolean 유형의 매개변수가 있는 경우,  매개변수의 의미가 문맥으로부터 명확하게 이해되지 않는다면 명명된 인자 구문을 사용해라. 

```kotlin
drawSquare(x = 10, y = 10, width = 100, height = 100, fill = true)
```

## 조건문

try, if, when 표현 형태를 사용하는 것이 좋다. 

```kotlin
return if (x) foo() else bar()
```

```kotlin
return when(x) {
    0 -> "zero"
    else -> "nonzero"
}
```

위의 방식이 더 선호된다.

```kotlin
if (x)
    return foo()
else
    return bar()
```

```kotlin
when(x) {
    0 -> return "zero"
    else -> return "nonzero"
}
```
## if vs when

단일조건에서는 when대신에 if를 사용하는 것이 선호된다. 예를 들어 해당 문법과 같이 if를 사용한다. 

```kotlin
if (x == null) ... else ...
```

when과 함께 문법을 사용하는 대신에 :

```kotlin
when (x) {
    null -> // ...
    else -> // ...
}
```

세 개 혹은 더 많은 경우 when을 사용하는 것이 좋다.

## 조건문에서 널 Boolean값을 사용하는 경우

만약 조건문에서 널 Boolean 값을 사용하는 것이 필요한 경우 `if (value == true)` 혹은 `if (value == false)` 체크를 사용해라. 

## 반복

반복문에서 고차 함수(`filter`, `map`)를 사용하는 것이 좋다. 

예외: `forEach`(nullable한 수신자 혹은 `forEach`가 긴 호출 체인의 일부로 사용되는 경우 `for` 루프를 사용하는 것이 좋다)

여러 고차 함수와 반복문을 사용한 복잡한 표현 사이에 선택지를 만들 때 각 경우 수행되는 운영 비용을 이해하고 성능 고려를 염두에 두어야 한다.

## 범위에서의 반복문

열린 범위를 반복하려면 `..<` 연산자를 사용해라. 

```kotlin
for (i in 0..n - 1) { /*...*/ }  // 나쁜 예
for (i in 0..<n) { /*...*/ }  // 좋은 예
```
## 문자열

문자열 연결대신 문자열 템플릿을 선호해라.

정규 문자열 리터럴에 `\n` 이스케이프 시퀀스를 하는 것 보다 여러줄 문자열이 선호된다. 

여러 줄 문자열에서 들여쓰기를 유지하기 위해 결과 문자열이 내부 들여쓰기를 요구하지 않을 때 trimIndent, 내부 들여쓰기가 요구된다면 trimMargin을 사용해라. 

```kotlin
fun main() {
    println("""
    Not
    trimmed
    text
    """
           )

    println("""
    Trimmed
    text
    """.trimIndent()
           )

    println()

    val a = """Trimmed to margin text:
          |if(a > 1) {
          |    return a
          |}""".trimMargin()

    println(a)
}
```

[Java와 Kotlin의 다중 문자열](https://kotlinlang.org/docs/java-to-kotlin-idioms-strings.html#use-multiline-strings) 차이점을 학습해라. 

## 메소드 vs 속성

몇몇의 경우에 인수가 없는 메소드는 읽기 전용 속성과 교환하여 사용할 수 있다. 의미가 비슷함에도 불구하고, 어떤 것을 선호해야 하는지 스타일 관례가 있다. 

기본 알고리즘일 때 함수보다 속성이 선호된다.

- 예외가 없는 경우
- 계산이 적은 경우(혹은 첫 번째 실행 시 캐시되는 경우)
- 객체 상태가 변하지 않는다면 호출에 대해 같은 결과를 반환하는 경우

## 확장 함수

확장함수를 자유롭게 사용해라. 항상 객체에서 주요하게 작동되는 함수를 가지면, 리시버로서 객체를 수용하는 확장 함수로 만드는 것을 고려해라. API 오염을 최소화하기 위해 가능한한 확장함수의 가시성을 제한해라. 필요에 따라 로컬 확장함수, 멤버 확장 함수, 혹은 비공개 가시성을 가진 최고 레벨 확장함수로 사용해라 

## 인픽스 함수

두개의 객체가 비슷한 역할로 작동할 때만 함수 선언을 `infix`로 해라. 좋은 예: `and`, `to`, `zip`. 나쁜 예: `add`

만약 리시버 객체가 변화하는 경우 `infix`로서 메서드 선언하지 마라.

## 팩토리 함수

만약 클래스에 대한 팩토리 함수를 선언할 경우, 클래스 자체와  동일한 이름을 사용하는 것을 피해라. 고유한 이름을 사용한다면 팩토리 함수의 동작이 특별한 이유가 명확해진다. 오직 특별한 의미가 없을 경우에만 클래스와 동일한 이름을 사용할 수 있다. 

```kotlin
class Point(val x: Double, val y: Double) {
    companion object {
        fun fromPolar(angle: Double, radius: Double) = Point(...)
    }
}
```

만약 여러개의 오버로드된 구조를 가진 생성자를 가진다면 서로 다른 슈퍼클래스를 호출하지 않고 기본 인수 값으로 단일 생성자로 줄일 수 없다면 오버로딩된 생성자 대신 여러개의  팩토리 함수를 가진 오버로드된 구조로 대체하는 것이 좋다. 

## 플랫폼 타입

플랫폼 타입의 표현식을 반환하는 공개 함수/메서드는 코틀린 형식을 명시적으로 선언해야 한다. 

```kotlin
fun apiCall(): String = MyJavaApi.getProperty("name")
```

플랫폼 타임의 표현식으로 초기화된 모든 속성(패키지 레벨 혹은 클래스 레벨)은 코틀린 형식을 명시적으로 선언해야 한다. 

```kotlin
class Person {
    val name: String = MyJavaApi.getProperty("name")
}
```

플랫폼 타입의 표현식으로 초기화된 지역 변수는 형식 선언을 가져도 되고 아니여도 된다. 

```kotlin
fun main() {
    val name = MyJavaApi.getProperty("name")
    println(name)
}
```

## 스코프 함수 apply/with/run/also/let

코틀린은 주어진 객체의 컨텍스트에서 코드 블럭을 실행하는 함수 세트를 제공한다: `let`, `run`, `with`, `apply`, `also` 

케이스에 적합한 스코프 기능을 선택할 수 있도록 가이드를 제공하는데 [Scope Functions](https://kotlinlang.org/docs/scope-functions.html)를 참고해라.
