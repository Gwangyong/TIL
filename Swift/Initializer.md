# 지정 이니셜라이저(Designated Initializer)

Designated init은 Swift의 초기화 이니셜라이저이다.
```swift
init(매개변수: 타입, ...) {
    // 프로퍼티 초기화
    // 인스턴스 생성 시 필요한 설정을 해주는 코드 작성
}
```

`이니셜라이저(생성자)`를 사용하는 이유는 **인스턴스의 프로퍼티마다 초기값을 설정해주고 새로운 인스턴스를 사용하기 전에 필요한 설정을 해주기 위해 사용**하며, 클래스 내부에는 반드시 한 개 이상의 지정 이니셜라이저가 있어야 한다.

이름은 `Designated init`이지만, 아래의 예시 코드와 같이 `init`으로 사용한다.

```swift
class Person {
    var name: String
    var age: Int
    
    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
    
    // 매개변수로 받지 않고, 프로퍼티의 값을 대입해서 초기화도 가능
    init(age: Int) {
        self.name = "Juuuud"
        self.age = age
    }
}

// 인스턴스 생성
var person = Person(name: "Jud", age: 22)
person.name   // "Jud"
person.age    // 22

// 프로퍼티 값 대입해서 초기화한 인스턴스 생성
var person2 = Person(age: 25)
person2.name   // "Juuuud"
person2.age    // 25
```

여기에서 하나의 프로퍼티(name, age, gender)라도 빠지게 된다면, `Return from initializer without initializing all stored properties` 라는 오류가 발생한다.

<br>

# 편의 이니셜라이저(Convenience Initializer)

convenience init은 `보조 이니셜라이저`이다.
```swift
convenience init(매개변수: 타입, ...) {
    // 구현부
}
```

편의 이니셜 라이저는 지정 이니셜라이저의 일부 매개 변수의 기본 값을 설정하여 초기화한다.

클래스의 지정 이니셜라이저인 init을 도와주는 역할이라고 생각하면 되며, 도와주는 역할이다 보니 init가 꼭 먼저 선언되어 있어야지 사용이 가능하다.

Designated init의 파라미터 중 일부를 기본값으로 설정해서, 호출하여 초기화를 진행할 수 있다.

아래의 예시 코드와 같이 `convenience init`을 사용한다.
```swift
class Person {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }

    convenience init(name: name) {
        self.init(name: name, age: 22) // 지정 이니셜라이저 호출
    }
}

let jud = Person(name: "Jud") // Person(name: "Jud", age: 22)
```




<!-- 
> Reference
- [Swift ) init과 convenience init의 차이](https://zeddios.tistory.com/141)
- [오늘의 Swift 상식 (Initializer 2편. 클래스의 Initializer)](https://medium.com/@jgj455/%EC%98%A4%EB%8A%98%EC%9D%98-swift-%EC%83%81%EC%8B%9D-initializer-2%ED%8E%B8-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-initializer-7141cda4ecf2)
 -->