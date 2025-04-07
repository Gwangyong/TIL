- Swift 조건문에는 대표적으로 if-else와 switch-case문이 있다.
- 이번에는 switch-case문을 정리한다.


# Switch문
- 주어진 값에 따라 여러 경우 중 하나를 선택하여 실행하는 `조건 분기문`
- 모든 가능한 입력 처리를 해야하므로, `default`를 사용하거나 모든 범위를 커버해야한다. (모든 범위가 확실하게 커버된다면 default 없이도 작성할 수 있다)
- 다른 언어와 다르게 자동으로 다음 case는 실행되지 않는다.
- 다음 case도 실행하려면, `fallthrough`를 사용해야 한다.
- 범위(1...3), 튜플, 조건(where 구문) 등을 사용 가능하다.
- switch문은 단순 조건이 아닌, 여러 경우를 나눌 때 if문 보다 유리하다


```swift
// 예시
let number = 3

switch number {
case 1:
    print("One")
    
case 2, 3, 4:
    print("Two, Three or Four")
    
default:
    print("Other number")
} // Two, Three or Four
```

<br>

## if문과 switch문 사용 비교

```swift
// if문
let score = 80

if score >= 90 {
    print("A")
} else if score >= 75 {
    print("B")
} else {
    print("C")
} // B

```

```swift
// switch문
let score = 80

switch score {
case 90...100:
    print("A")
case 75..<90:
    print("B")
default:
    print("C")
} // B

```

<br>

## where문 
- where문의 추가로 더욱 세부화 가능

```swift
// where문 예시
let point = (2, -2)

switch point {
case let (x, y) where x == y:
    print("x와 y와 같다.")
case let (x, y) where x == -y:
    print("x와 y는 서로 반대다.")
default:
    print("기타")
} // x와 y는 서로 반대다.
```

<br>

## fallthrough문
- fallthrough를 사용하여 다음 case도 실행할 수 있다.
- 단, 오직 바로 다음 case 하나만 실행 가능하며, 조건 검사는 생략된다.

```swift
// fallthrough 예시
let number = 1

switch number {
case 1:
    print("1입니다.")
    fallthrough
case 2:
    print("2입니다.")
default:
    print("기타.")
}
// 1입니다.
// 2입니다.
```