## self

self 키워드는 클론코딩을 하면서 많이 사용했는데, **self 프로퍼티는 자기 자신을 가리키는 프로퍼티**이다. Java에서는 this와 같이 자기 자신을 가리키는 것이다.

self 프로퍼티를 사용해서 자체 인스턴스 메소드 내에서 현재 인스턴스를 참조할 수 있다.

```swift
Class Person {
    var name: String = ""
    func SetName(name: String) -> () {
        self.name = name
    }
}
```
위의 코드를 보자. 이 예시에서 Person 클래스의 멤버변수 'name'과 함수 SetName 메서드의 매개변수 이름인 'name'이 동일하다.

여기서 setName 함수 내에 'self.name'은 클래스의 멤버변수 'name'을 의미하며, 그 뒤의 name은 매개변수로 받은 'name'을 의미한다.

self는 인스턴스는 매개변수 이름과 저장 인스턴스 프로퍼티 이름이 같으면, swift 매개변수 이름을 우선적으로 적용하기 때문에 self를 붙여서 이것이 **해당 타입의 저장 인스턴스 프로퍼티인지 구별**해줘야 하기 때문에 사용한다.

<br>

self와 Self는 다르다는데, 아직까지 써본적도 본 적도 없으니 나중에 사용하게되면 알아보자..