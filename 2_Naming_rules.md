# 명명 규칙

코틀린에서 패키지와 클래스의 명명 규칙은 꽤 간단하다.

- 패키지의 이름은 항상 소문자이고 밑줄을 사용하면 안된다.(org.example.project) 여러 단어 이름을 사용하면 일반적으로 권장되지 않지만 여러 단어를 사용해야 한다면 단어들을 그냥 연결하거나 카멜 케이스를 사용해서 할 수 있다. (org.example.myProject)
- 클래스와 객체의 이름은 대문자로 시작하고 카멜 케이스를 사용한다.

```kotlin
open class DeclarationProcessor{ /*...*/ }
object EmptyDeclarationProcessor : DeclarationProcessor() { /*...*/ }
```

## 함수 이름

함수, 프로퍼티, 로컬 변수의 이름은 소문자로 시작하고 카멜 케이스를 사용하며 밑줄을 사용하지 않는다.

```kotlin
fun processDeclarations() { /*...*/ }
var declarationCount = 1
```

예외: 클래스의 인스턴스를 생성하는데에 사용되는 팩토리 함수는 추상 리턴 타입과 동일한 이름을 가질 수 있다. 

```kotlin
interface Foo { /*...*/ }
class FooImpl : Foo { /*...*/ }
fun Foo(): Foo { return FooImpl() }
```

## 테스트 메소드 이름

테스트에서, 백틱이 포함된 공간에서 메소드 이름을 사용할 수 있다.  이러한 메소드 이름들은 현재 안드로이드 런타임에서 지원되지 않고 있는 것을 기억해라. 테스트 코드 내에서 메소드 이름에 밑줄 허용된다. 

```kotlin
class MyTestCase {
	@Test fun `ensure evertything works`() { /*...*/ }
	@Test fun ensuerEverythingWorks_onAndroid() { /*...*/ }
}
```

## 프로퍼티 이름

상수의 이름(const로 표시되는 프로퍼티 혹은 최고 레벨 혹은 깊은 불변 데이터를 가지는 사용자 지정 get 함수가 없는 val 객체 프로퍼티)대문자(snack case)로 구분된 이름을 사용해야 한다. 

```kotlin
const val MAX_COUNT = 8
val USER_NAME_FIELD = "UserName"
```

행동 혹은 가변 데이터를 가지는 최고 레벨 혹은 객체 프로퍼티 이름은 카멜 케이스 이름을 사용해야 한다. 

```kotlin
val mutableCollection: MutableSet<String> = HashSet()
```

싱글톤 객체에 대한 참조를 가지는 프로퍼티 이름은 객체(object) 선언과 네이 스타일이 동일하게 사용될 수 있다. 

```kotlin
val PersonComparator: Comparator<Person> = /*...*/
```

enum 상수에서 사용에 따라 대문자로 구분된 이름 혹은 상위 카멜 케이스 이름 사용이 가능하다.

## 백업 프로퍼티(속성) 이름

만약 클래스가 하나는 공동 API의 일부이고 다른 하나는 구현 세부정보인 개념적으로 동일한 두개의 프로퍼티를 가진다면 private 프로퍼티의 이름 접두사에 밑줄을 사용해라.

```kotlin
class C {
    private val _elementList = mutableListOf<Element>()

    val elementList: List<Element>
         get() = _elementList
}
```

## 좋은 이름 선택하기

클래스 이름은 보통 명사나 클래스가 무엇인지 설명하는 명사구이다. : List, PersonReader

메서드 이름은 보통 동사나 메서드가 하는 것이 무엇인지 말하는 동사구이다. : close, readPersons. 이름은 객체 변환 혹은 새로운 객체를 반환한다면 또한 제안해야 한다. 예를 들어 sort는 공간에서 컬랙션을 정렬하는것이고 sorted는 컬랙션의 정렬된 복사본을 반환하는 것이다.

이름은 개체의 목적이 무엇인지 명확하게 만들어야하므로  이름에 의미없는 단어(Manager, Wrapper)를 사용하는 것을 피하는 것이 좋다. 

선언 이름의 일부로 약어를 사용할 때, 두개의 문자(IOStream)로 구성된다면 대문자로; 만약 길다면(XmlFormatter, HttpInputStream) 첫번째 글자만 대문자로 시작한다.
