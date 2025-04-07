# Codable

![스크린샷 2021-11-08 오후 4 48 45](https://user-images.githubusercontent.com/59376200/140703378-56dba301-e01e-4725-9720-d241d9fa3df7.png)

Codable은 struct, enum, class에서 전부 채택이 가능한 프로토콜이다.

Codable은 위의 사진에 정의가있는데, 이를 해석해보면 **"자신을 변환하거나 외부표현으로 변환할 수 있는 타입입니다."** 라고 정의되어있다.

여기에서의 외부표현은 JSON으로 생각하면 될 것이다.



<br>

## Encodable & Decodable

Codable은 아래의 코드로 이루어져있는데, 보이는 것과 같이 Decodable과 Encodable이 합쳐져있는 것이다. 
```swift
typealias Codable = Decodable & Encodable
```

즉, Codable은 Decodable과 Encodable 프로토콜을 준수하는 타입이다.

<br>

`Decodable`은 자신을 외부표현에서 디코딩 할 수 있는 타입
`Encodable`은 자신을 외부표현으로 인코딩 할 수 있는 타입
이다.

json으로 예를 들자면, 
`Decodable` -> json을 원하는 모델로 디코드
`Encodable` -> 모델을 json으로 인코드