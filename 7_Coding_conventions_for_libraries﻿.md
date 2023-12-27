# 라이브러리 코딩 컨벤션

라이브러리를 작성할 때, API 안정성을 보장하기 해 추가적인 규칙을 따르는 것이 추천된다. 

- 멤버의 가시성을 항상 명시적으로 지정해라.(의도치 않게 공개 API로 노출하는 것을 피하기 위해)
- 항상 함수 반환 타입과 속성 타입이 명시적으로 지정되도록 해라.(구현 변경될 때 반환 타입이 실수로 변경하는 것을 피하기 위해)
- 새로운 문서화가 요구되지 않는 오버라이드를 제외하고 모든 공개 멤버에 [KDoc](https://kotlinlang.org/docs/kotlin-doc.html) 코멘트를 제공해라.(라이브러리에 문서 생성을 지원하기 위해)

라이브러리를 작성할 때 API에 대한 최상의 관례와 이이디어에 대해 더 알고싶다면 [library creators' guidelines](https://kotlinlang.org/docs/jvm-api-guidelines-introduction.html) 을 참고해라
