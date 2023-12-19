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
