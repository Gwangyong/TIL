[이 내용을 정리한 개인 기술 블로그](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-if-let-%EA%B3%BC-guard-let%EC%9D%98-%EC%B0%A8%EC%9D%B4%EB%8A%94?category=1010119)

guard let과 if let은 공통적으로 `옵셔널 바인딩` 이라는 특징을 가지고있다.

우리는 변수에 값이 있을지 없을지 모르는 상황에서 optional을 사용하지만, 그 값을 가져오려면 optional binding을 사용하여 값을 unwrap해와야 한다. 

이럴 때 안전하게 값을 추출하기 위해 사용하는게 `guard let`과 `if let`이다.

<br>

# if let이란?
`if let`은 **성공시와 실패시 2가지 경우로 나눠서, 두 분기 모두에 우리가 원하는 코드를 작성해줄 수 있다.**  즉, 코드에서 nil 일 때와, nil이 아닐 때 2가지로 나누어서 코드를 작성해줄 수 있다. 

하지만, if let은 `지역변수`로만 사용이 가능하기 때문에, **구문 밖에서 접근이 불가능하다.**

```swift
func printName() {
    var name: String?
    name = "Jud"
    print(name) // Optional("Jud")

    if let myName = name {
        print(myName) // "Jud"
    } else {    // name의 값이 nil일 경우.
        print("nil")
    }
}
```

<br>

아래와 같이 name에 nil을 넣게 되면, if let 구문의 안에 있는 print(myName)이 실행되지 않고, else 구문으로 넘어가서 "nil"이 출력된다.
```swift
func printName() {
    var name: String?
    name = nil
    print(name) // nil

    if let myName = name {
        print(myName) // 실행되지 않음.
    } else {
        print("nil") // "nil"
    }
}
```

<br>

# guard let은?
`guard`는 뒤에 따라붙는 bool 타입의 값이 `참(true)`일 경우 코드가 계속 실행되며, `거짓(false)`일 경우는 else의 블록 내부 코드가 실행된다.

또한, else 내부 코드에는 `return, break, continue, throw` 등의 `제어문 전환 명령어` 사용해야 한다.

if let 구문과는 다르게 guard 구문은 항상 `else` 구문이 뒤에 따라와야 하며, guard문은 **함수 전체에서 추출된 `상수`나 `함수`를 사용 가능하다.**

```swift
func printName() {
    var name: String?
    name = "Jud"
    print(name)     // Optional("Jud")
    
    guard let myName = name else { return }
    print(myName)   // "Jud"
}
```

<br>


## 정리

### if let
- 성공과 실패 2가지로 나누어서 원하는 작업이 가능하다.
- 지역 변수로만 사용이 가능하다.
- else문을 생략할 수 있다.
- 조건을 가지고 나뉘어서 처리하려면 if let을 사용한다.

### guard let 
- if let 구문과 다르게, else문을 생략할 수 없다.
- guard는  return, break, continue, throw 등의 `제어문 전환 명령어`를 반드시 넣어주어야 한다.
- 요구사항만을 반영해서 예외처리를 하려면 guard let을 사용하는 것이 더욱 간결한 코드가 될 것이다.
- guard문은 함수 전체에서 optional로 추출된 상수나 함수를 사용할 수 있다.





