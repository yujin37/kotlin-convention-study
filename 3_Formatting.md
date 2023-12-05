# 형식

## 들여쓰기

들여쓰기를 위해 4개의 공간을 사용한다. 탭을 사용하지 마라.

중괄호에 대해서는, 개념이 시작되는 줄의 끝에 열리는 괄호를, 그리고 열린 개념과 수평적으로 정렬된 분리된 줄에 닫히는 괄호를 두어라.

```kotlin
if (elements != null) {
    for (element in elements) {
        // ...
    }
}
```

<aside>
⚠️ 코틀린에서, 세미콜론은 선택적이고, 그래서 줄 바꿈이 중요하다. 언어 디자인은 자바 스타일 괄호를 가정하고 당신은 만약 다른 형식 스타일을 사용하려고 한다면 놀라운 태도를 직면할 것이다.

</aside>

## 가로 공백

- 이항 연산자(`a + b`) 주위에 공백을 두어라. 예외: 범위 연산자(`0..i`)주위에는 공백을 두지 마라
- 단항 연산자(`a++`) 주위에 공백을 두지마라.
- 제어 흐름 키워드(if, when, for, while)와 대응하는 여는 괄호  사이에 공백을 두어라.
- 주 생성자 선언, 메서드 선언, 메서드 호출에서 여는 괄호 전에 공백을 두지 마라.

```kotlin
class A(val x: Int)

fun foo(x: Int) { ... }

fun bar() {
    foo(1)
}
```

- `(`, `[`  뒤 혹은 `]`, `)` 전에 공백을 절대로 두지 마라
- `.` 혹은 `?.` 주위에 공백을 절대로 두지 마라 : `foo.bar().filter { it > 2 }.joinToString()`, `foo?.bar()`
- `//` 뒤에 공백을 두어. :  // 이것은 주석이다.
- 특정한 형식 파라미터를 사용하는 < > 주위에 공백을 두지 마라 : `class Map<K, V> { ... }`
- `::` 주위에 공백을 두지마라 : `Foo::class`, `String::length`
- nullable 타입을 표시하는데 사용되는 `?` 전에 공백을 사용하지 마라 : `String?`
- 일반적인 규칙에서, 어떤 종류의 수평 정렬을 피해라.

식별자의 이름을 길이가 다른 이름으로 바꾸는 것은 선언 혹은 사용되는 부분의 형식에 영향을 미치지 않아야 한다.

## 콜론

다음의 경우 `:` 전에 공백을 두어라 .

- 타입과 상위 타입을 구분하는 데에 사용할 때
- 상위 클래스의 생성자 혹은 같은 클래스의 다른 생성자로 위임할 때
- `object` 키워드 뒤에

선언과 해당 타입을 구분하는 `:` 전에 공백을 두지 마라.

항상 `:` 뒤에는 공백을 두어라.

```kotlin
abstract class Foo<out T : Any> : IFoo {
    abstract fun foo(a: Int): T
}

class FooImpl : Foo() {
    constructor(x: String) : this(x) { /*...*/ }

    val x = object : IFoo { /*...*/ }
}
```

## 클래스 헤더

몇 개의 주요한 생성자 파라미터를 가지는 클래스는 한 줄로 작성할 수 있다. 

```kotlin
class Person(id: Int, name: String)
```

더 긴 헤더를 가진 클래스는 주요한 생성자의 각 파라미터는 구분된 줄에 들여쓰기로 작성되어야 한다. 또한, 닫는 괄호는 새로운 줄에 있어야 한다. 만약 상속을 사용한다면 상위 클래스 생성자 호출 혹은 구현된 인터페이스 목록은 위치해야 한다. 괄호와 같은 줄에 위치해야 한다.  

```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name) { /*...*/ }
```

다중 인터페이스에서 슈퍼 클래스 생성자 호출은 처음에 위치해야 하고 각 인터페이스는 다른 줄에 위치해야 한다. 

```kotlin
class Person(
    id: Int,
    name: String,
    surname: String
) : Human(id, name),
    KotlinMaker { /*...*/ }
```

긴 상위 타입 목록을 가진 클래스에서 콜론 뒤에 줄 바꿈을 두고 모든 상위 타 이름과 수평으로 정렬해야 한다. 

```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne {

    fun foo() { /*...*/ }
}
```

클래스 헤더가 길 때 클래스 헤더와 본문을 명확히 구분하기 위해 클래스 헤더에 빈칸 줄을 두거나 별도의 줄에 여는 중괄호를 두어야 한다. 

```kotlin
class MyFavouriteVeryLongClassHolder :
    MyLongHolder<MyFavouriteVeryLongClass>(),
    SomeOtherInterface,
    AndAnotherOne
{
    fun foo() { /*...*/ }
}
```

생성자 파라미터에서 일반 공백(4칸 공백)을 사용해라. 이렇게 하면 주요한 생성자에서 선언된 프로퍼티들이 클래스 본문에서 선언된 프로퍼티와 동일한 들여쓰기를 가진다.
