[이 내용을 정리한 개인 기술 블로그](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-Optional-Binding%EC%9D%B4%EB%9E%80-%F0%9F%A7%90?category=1010119)

# 옵셔널 바인딩(Optional Binding)이란?

Optional Binding은 Optional 타입으로 선언된 변수에 값이 있는지 없는지를 확인할 수 있도록 도와주는 기능이다.

`Optional Binding`은 optional의 값이 존재하는지 검사한 뒤, 값이 존재한다면 **"!(느낌표)" 없이** Optional 타입의 변수 값을 출력할 수 있어서, 좀 더 안전한 형태로 값을 얻을 수 있다.

`if let` 또는 `if var` 를 사용하는데, 옵셔널 값이 있다면 `if`문 안으로 들어가고, 값이 `nil` 이라면 그냥 통과 하게 된다.

아래의 예시 코드를 예시로 보자.
```swift
if let name = optionalName {
    print(name) // optionalName의 값이 존재하면 해당 값이 출력된다.
}

// optionalName의 값이 존재하지 않는다면, if문을 그냥 지나쳐서 이곳의 코드가 실행된다.
```

위의 코드에서 `optionalName`에 값이 존재한다면, `name`이라는 변수 안에서 실제 값이 저장되고, `if`문 내에서 그 값을 사용할 수 있다.

만약에 `optionalName`의 값이 `nil`이라면 `if`문은 그냥 지나치게된다.

<br>

아래의 코드처럼 하나의 `if`문에서 콤마(,)를 사용하여 여러개의 옵셔널을 바인딩할 수 있으며, 콤마(,)가 &&의 역할을 해준다.
```swift
var optionalName: String? = "홍길동"
var optionalCountry: String? = "Korea"

if let name = optionalName, country = optionalCountry {
    // name과 country 값이 존재
}
// name과 country 값이 존재하지 않는 경우
```

<br>

또한, 아래의 코드와 같이 optional binding 이후 그 값을 가지고 조건도 같이 지정해줄 수 있다.
```swift
if let age = optionalAge {
    if age >= 20 {
        // age의 값이 존재하고, 20살 이상이다.
    }
}
```

<br>

**`tip!!`** 코드가 많이 길어질 경우에는 아래와 같은 방법으로 작성하여 가독성을 높일 수 있다.
```swift
if let name = optionalName, 
    let country = optionalCountry {
        // name과 country 값이 존재
    }
// name과 country 값이 존재하지 않는 경우
```

<br>

# 옵셔널 체이닝(Optional Chaining)이란?

optional chaining은 이름에서 보이듯 체인처럼 이어진다는 느낌이다.

`옵셔널 체이닝(Optional Chaining)`은 하위의 property에 optional 값이 있는지 없는지 연속적으로 확인하면서, **중간에 하나라도 nil이 발견되면 그 즉시 nil이 반환**되는 형식이다.

또한, 옵셔널 체이닝의 속성은 일반적인 `Int`는 옵셔널 체이닝으로 접근할 때 `Int?`로 반환된다.

<br>

예제 코드는 [스위프트 언어가이드 - Optional Chaining](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html) 에 나와있는 예제이다.

처음으로, `Person`과 `Residence`라는 두 개의 클래스가 정의된다.
```swift
class Person {
    var residence: Residence?
}
// 두 개의 클래스가 호출되고, residence 라는 변수가 Residence 클래스를 상속받고있다. 또한 optional 기호 ?도 같이 작성해 주었다.

class Residence {
    var numberOfRooms = 1
}
// Residence 인스턴스는 기본 값 1을 가지는 numberOfRooms라는 Int형 속성을 하나 가지게 된다.
```

<br>
아래의 코드에서 Person 타입의 인스턴스를 Jud로 생성해 주었다.

```swift
let Jud = Person()
```

Jud의 프로퍼티로는 residence가 있는데, residence변수는 Residence클래스를 옵셔널의 형태로 상속받고 있다.

여기서 옵셔널 타입은 따로 초기화하지 않으면 nil로 초기화가 되기 때문에, 위의 코드의 Jud에서 residence 속성 값은 nil이 된다.


<br>

```swift
let roomCount = Jud.residence!.numberOfRooms
// this triggers a runtime error
```
위의 코드를 보면, 밑에 주석부분과 같이 오류가 생성된다.

그 이유는 위에서 설명한대로 Jud에서의 residence속성 값이 nil인데, `!`를 사용하여 주었기 때문이다.

<br>

아래의 코드도 Jud.residence의 값이 nil이기 때문에, else문으로 넘어가서 아래의 코드가 실행된다.
하지만 위와는 다르게 `!`가 아닌, `?`를 사용했기 때문에, 오류는 생성되지 않는다.

<br>

```swift
let roomCount = Jud.residence?.numberOfRooms {
    print("Jud's residence has \(roomCount) room(s).")
} else {
    print("Unable to retrieve the number of rooms.")
}
// 출력 결과 : "Unable to retrieve the number of rooms."
```
여기까지 사용해봤는데 어느 부분에 옵셔널 체이닝을 사용한건지는 설명하지 않았다. 어느 부분에서 옵셔널 체이닝을 사용했을까?

```swift
let roomCount = Jud.residence?.numberOfRooms
```

바로 이 부분에 옵셔널 체이닝 방법을 적용한 것이다.

`property`를 통해 체인처럼 이어져있는데, `Jud`의 `residence`가 `nil`이 아니라면 `numberOfRooms`를 확인하여 `roomCount`에 방 번호가 포함되어 저장된다.

<br>

만일, 위의 코드가 if문의 조건을 수행하여 **Jud's residence has 1 room(s).** 라는 결과가 나타나도록 하려면 
```swift
Jud.residence = Residence()
```
라는 코드를 추가하면 된다.

<br>

Optional에서 설명했지만, 다시 한번 강조하자면 `!`를 사용하는 `강제 언래핑(Froced Unwrapping)`은 가능하면 사용하지 않는것이 좋다.

위의 이유와 !(강제 언래핑)을 언제 사용하는지가 궁금하다면, Optional에 대해 정리한걸 먼저 보고오는게 좋을 것이다.


<!-- >  참고한 자료 & 블로그
> - [Swift3 ) Optional 개념 정리](https://zeddios.tistory.com/16)
> - [The Swift Programming Language - Optional Chaining](https://docs.swift.org/swift-book/LanguageGuide/OptionalChaining.html)
> - [40시간만에 Swift로 iOS 앱 만들기 - 옵셔널 (Optional)](https://devxoul.gitbooks.io/ios-with-swift-in-40-hours/content/Chapter-2/optionals.html) -->