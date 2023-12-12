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

## 수정자 순서

만약 선언이 여러 개의 수정자를 가진다면 항상 아래의 순서로 두어야 한다. 

```kotlin
public / protected / private / internal
expect / actual
final / open / abstract / sealed / const
external
override
lateinit
tailrec
vararg
suspend
inner
enum / annotation / fun // as a modifier in `fun interface`
companion
inline / value
infix
operator
data
```

모든 어노테이션을 수정자 전에 두어라.

```kotlin
@Named("Foo")
private val foo: Foo
```

라이브러리에서 작업을 하지 않는다면 중복된 수정자는 생략해라(예를 들면 `public` )

## 어노테이션

어노테이션은 선언 전에 위치하고 같은 들여쓰기로 별도의 줄에 둔다.

```kotlin
@Target(AnnotationTarget.PROPERTY)
annotation class JsonExclude
```

인자가 없는 어노테이션은 같은 줄에도 가능하다.

```kotlin
@JsonExclude @JvmField
var x: String
```

인자가 없는 단일 어노테이션은 해당 선언과 같은 줄에 둘 수 있다. 

```kotlin
@Test fun foo() { /*...*/ }
```

## 파일 어노테이션

파일 어노테이션은 파일 어노테이션(있는 경우) 뒤, package 문 전에 위치하며 패키지와 빈 줄로 구분된다. (파일 대상이며 패키지에 대한 대상이 아닌 것을 강조하기 위해)

```kotlin
/** License, copyright and whatever */
@file:JvmName("FooBar")

package foo.bar
```

## 메소드

메소드의 시그니처가 단일 줄에 맞지 않는 경우 아래와 같은 문법을 사용해라. 

```kotlin
fun longMethodName(
    argument: ArgumentType = defaultValue,
    argument2: AnotherArgumentType,
): ReturnType {
    // body
}
```

메소드 파라미터는 일반적인 들여쓰기(4칸 공백)를 사용해라.  생성자 파라미터와 일관성을 보장하는데에 도움이 된다. 

본문이 단일 표현식으로 구성된 메소드에는 표현식 본을 사용하는 것이 좋다.  

```kotlin
fun foo(): Int {     // bad
    return 1
}

fun foo() = 1        // good
```

## 표현식 본문

만약 함수가 선언과 같은 줄에 들어가지 않는 경우, = 표시를 첫번째 줄에 두고 표현식 분문을  4개의 공백으로 들여쓰기 해라. 

```kotlin
fun f(x: String, y: String, z: String) =
    veryLongFunctionCallWithManyWords(andLongParametersToo(), x, y, z)
```

## 속성

매우 간단한, 읽기 전용 속성은 한 줄에 포맷 하는 것을 고려해라.

```kotlin
val isEmpty: Boolean get() = size == 0
```

더 복잡한 속성은 항상 get과 set 키워드를 별도의 줄에 두어야 한다. 

```kotlin
val foo: String
    get() { /*...*/ }
```

초기 값이 있는 속성에서 만약 초기 값이 길다면 `=` 기호 뒤에 줄 바꿈을 추가하고 4칸 공백으로 초기 값을 들여쓰기 해라 

```kotlin
private val defaultCharset: Charset? =
    EncodingRegistry.getInstance().getDefaultCharsetForPropertiesFiles(file)
```

## 제어 흐름문

`if`혹은 `when` 문 조건이 여러 줄이라면 항상 중괄호를 본문 주변에 사용해야 한다. 조건의 각 다음 줄은 시작문과 비교하여 4칸 공백으로 들여쓰기를 해야 한다. 조건의 닫는 괄호는 구분된 줄에 열린 괄호와 함께  두어야 한다. 

```kotlin
if (!component.isSyncing &&
    !hasAnyKotlinRuntimeInScope(module)
) {
    return createKotlinNotConfiguredPanel(module)
}
```

이것은 조건과 문의 본문을 정렬하는 데에 도움을 준다. 

`else`, `catch`, `finally` 키워드와 `do-while` 반복문의  while 키워드 또한 이전 중괄호와 같은 줄에 두어야 한다. 

```kotlin
if (condition) {
    // body
} else {
    // else part
}

try {
    // body
} finally {
    // cleanup
}
```

`when` 문에서 분기가 한 줄보다 더 많은 경우, 인접 케이스 블럭으로부터 빈 줄로 분리하는 것을 고려해라.

```kotlin
private fun parsePropertyValue(propName: String, token: Token) {
    when (token) {
        is Token.ValueToken ->
            callback.visitValue(propName, token.value)

        Token.LBRACE -> { // ...
        }
    }
}
```

짧은 분기는 중괄호 없이 조건과 같은 줄에 두어라. 

```kotlin
when (foo) {
    true -> bar() // good
    false -> { baz() } // bad
}
```

## 메서드 호출

긴 인자 목록에서, 열란 괄호 뒤에 줄 바꿈을 해라. 4칸 공백으로 인자 들여쓰기를 해라. 매우 관련있는 여러 인자는 같은 줄에 그룹화해라. 

```kotlin
drawSquare(
    x = 10, y = 10,
    width = 100, height = 100,
    fill = true
)
```

인자 이름과 값 사 구분되는 `=` 기호 주변에 공백을 두어라. 

## 연결된 호출 감싸기

연결된 호출을 감쌀 때, . 문자 혹은 ?. 연산자를 단일 들여쓰기와 함께 다음 줄에 두어라.

 

```kotlin
val anchor = owner
    ?.firstChild!!
    .siblings(forward = true)
    .dropWhile { it is PsiComment || it is PsiWhiteSpace }
```

체인에서 첫번째 호출은 보통 그 전에 줄 바꿈을 가져야하고, 하지만 그 방법이 더 의미가 있다면 생략해도 괜찮다. 

## 람다

람다 표현에서 공백은 중괄호 주변, 본문에서 매개변수를 구분하는 화살표 주변에도 사용되어야 한다. 만약 호출이 단일 람다라면 가능한 괄호 밖으로 넘긴다. 

```kotlin
list.filter { it > 10 }
```

만약 람다에 레이블을 지정하는 경우 라벨과 여는 중괄호 사이에 공백을 두지 마라. 

```kotlin
fun foo() {
    ints.forEach lit@{
        // ...
    }
}
```

여러줄로 이루어진 람다에서 매개변수 이름을 선언할 때, 첫번째 줄에 이름을 두고 화살표와 줄바꿈을 추가해라. 

```kotlin
appendCommaSeparated(properties) { prop ->
    val propertyValue = prop.get(obj)  // ...
}
```

만약 매개변수 목록이 한 줄에 맞지 않을 정도로 긴 경우, 구분된 줄에 화살표를 두어라. 

## Trailing commas(마지막 쉼표)

마지막 쉼표는 요소들 시리즈에서 마지막 항목 뒤에 있는 쉼표이다.

```kotlin
class Person(
    val firstName: String,
    val lastName: String,
    val age: Int, // trailing comma
)
```

마지막 쉼표를 사용하는 것은 여러 이점을 가진다. 

- 모든 초점은 변경된 값에 집중되어 버전 관리 차이점이 더 깔끔해진다.
- 요소를 조작하여 쉼표를 추가하거나 삭제할 필요 없이 쉽게 추가하고 순서를 바꿀 수 있다.
- 예를 들어 코드 생성을 단순하게 한다. 마지막 요소는 또한 쉼표를 가질 수 있다.

마지막 쉼표는 전체적으로 선택적이다. - 코드는 여전히 마지막 쉼표없이 작동이 될 것이다. 코틀린 스타일 가이드는 선언된 위치에서 마지막 쉼표를 사용하도록 하고 호출 위치에서  자율에 그것을 맡긴다. 

IntelliJ IDEA 포멧터에서 마지막 쉼표를 사용 가능하게 하려면 **Settings/Preferences | Editor | Code Style | Kotlin** 으로 가서 **Other** 탭을 열고 **Use trailing comma** 옵션을 선택해라. 
