# get, set 문법
> **Status**: ✅ **학습 완료**<br>**Blog**: 

## get, set

위에서 사용된 `get`과 `set`에 대해서도 알아보자

우선, 위에서 사용되었던 아래의 코드는 get을 생략한 코드로

```swift
// 기본 get을 생략한 형태
var fullName: String {
	firstName + lastName
}
```

get을 생략하지 않는다면 아래와 같은 형태이다. 

```swift
// 기본 get을 생략한 형태
var fullName: String {
	get {
		firstName + lastName
	}
}
```

기본적으로 **“읽기 전용 연산 프로퍼티”** 로 `get`은 생략이 가능하다.

다만, `set`이 있다면, `get`을 생략할 수 없게된다.

## 그럼, get과 set은 “언제” 호출되어 사용될까

<aside>

### get

```swift
let name = fullName
```

`get`은 **값을 읽는 순간 자동 호출**되며, 함수처럼 호출하지 않는다.

### set

```swift
fullName = "Name"
```

`set`은 **값을 대입하는 순간 자동 호출**된다. 내부에서 `newValue` 사용이 가능하다.

- `newValue`는 **`set` 블록 안에서 자동으로 제공되는 임시 상수**로,
- 외부에서 해당 프로퍼티에 **대입한 값 그 자체**를 의미함.
</aside>

## 이제 get과 set의 접근 방식에 따라 실행되는 코드를 보자

> **get만 있는 경우 (읽기 전용)**
> 

```swift
struct User {
	let firstName: String
	let lastName: String
	
	var fullName: String {
		firstName + lastName
	}
}
```

```swift
let user = User(firstName: "길동", lastName: "홍")
print(user.fullName) // "길동홍"
```

- 동작 흐름 설명
    - `user.fullName` 접근
    - `get` 실행
    - 계산결과 반환

> **get과 set 둘 다 있는 경우**
> 

```swift
struct User {
	var firstName: String
	var lastName: String
	
	var fullName: String {
		get {
			firstName + lastName
		}
		set {
			let parts = newValue.split(separator: " ") // parts = ["철수", "김"]
			firstName = String(parts.first ?? "")
			lastName = String(parts.last ?? "")
		}
	}
}
```

```swift
var user = User(firstName: "길동", lastName: "홍")

print(user.fullName)
// get 호출 -> "길동홍"

user.fullName = "철수 김"
// set 호출 -> firstName, lastName 변경
// firstName = "철수"
// lastName  = "김"
```

## 왜 이런 구조를 사용할까?

이 구조의 목적으로는, **인터페이스는 단순**하게 하면서 **내부 구현은 숨기는 것**이 목적이다.

```swift
user.fullName = "홍길동"
```

겉으로만 보면 매우 단순한 대입이다.

하지만 내부에서는 여러 저장 프로퍼티를 안전하게 변경할 수 있다. (대입은 단순하지만, `set`에 쓰인 `parts`쪽 코드는 3줄이다.)

**→ “캡슐화!”**