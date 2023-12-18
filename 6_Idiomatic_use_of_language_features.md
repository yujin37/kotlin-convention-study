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
