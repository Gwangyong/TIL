## 문자열 리터럴

문자열은 큰 따옴표(`"`)로 묶어 표현한다.
```swift
let something = "Some string literal value"
```

<br>

## 여러줄 문자열 리터럴
여러줄의 문자열을 사용하고 싶은 경우 큰 따옴표 3개(""")로 묶어서 사용할 수 있다.
```swift
let quotation = """
The White Rabbit put on his spectacles.  "Where shall I begin,
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on
till you come to the end; then stop."
"""
```

<br>

여러줄 문자열을 사용할 때는 첫 시작의 `"""` 다음 줄부터 마지막 `"""`의 직전까지를 문자열로 본다.
그래서 아래 두 줄의 표현으로 이루어진 `singleLineString`과 `multilineString`은 같은 값을 갖는다.

```swift
let singleLineString = "These are the same."
let multilineString = """These are the same."""
```

<br>

여러줄 문자열을 사용하며 줄바꿈을 사용하고 싶으면 백슬래쉬(`\`)를 사용한다.
```swift
let softWrappedQuotation = """
The White Rabbit put on his spectacles.  "Where shall I begin, \
please your Majesty?" he asked.

"Begin at the beginning," the King said gravely, "and go on \
till you come to the end; then stop."
"""
```

<br>

## 빈 문자열 초기화

아래의 두 변수의 문자열 값은 같다.
```swift
var emptyString = ""
var anotherEmptyString = String()
```

<br>

문자열이 비어있는지 여부를 확인하기 위해서는 `isEmpty` 프로퍼티를 사용한다.
```swift
if emptyString.isEmpty {
    print("Nothing to see here")
}
// Prints "Nothing to see here"
```

<br>

## 문자
문자열의 개별 문자를 `for-in` loop를 사용해 접근할 수 있다.
```swift
for character in "Dog!" {
    print(character)
// D
// o
// g
// !
```

<br>

다음과 같이 문자 상수를 선언할 수 있다.
```swift
let exclamationMark: Character = "!"
```

<br>

## 문자열과 문자의 집합

```swift
let stringA = "Hello"
let stringB = ", World!"
var Hi = stringA + stringB
// Hi : "Hello, World!" 
```

<br>

## 문자열 삽입
```swift
let name = "Jack"
let message = "Hi! my name is \(name)!"
// message = "Hi! my name is Jack!"
```

<br>

## 문자의 삽입과 삭제
문자의 삽입과 삭제에는 `insert(: at:)`, `insert(contentsOf: at:)`, `remove(at:)`, `removeSubrange(:)` 메소드를 사용할 수 있다.

```swift
var welcome = "hello"
welcome.insert("!", at: welcome.endIndex)
// welcome : hello!

welcome.insert(contentsOf: " there", at: welcome.index(before: welcome.endIndex))
// welcome : hello there!
```

```swift
welcome.remove(at: welcome.index(before: welcome.endIndex))
// welcome : hello there

let range = welcome.index(welcome.endIndex, offsetBy: -6)..<welcome.endIndex
welcome.removeSubrange(range)
// welcome : hello
```