- Swift 조건문에는 대표적으로 if-else와 switch-case문이 있다.
- 이번에는 Switch-case문을 정리한다.


# Switch문
- 주어진 값에 따라 여러 경우 중 하나를 선택하여 실행하는 `조건 분기문`
- 모든 가능한 입력 처리를 해야하므로, `default`를 사용하거나 모든 범위를 커버해야한다. (모든 범위가 확실하게 커버된다면 default 없이도 작성할 수 있다)
- 다른 언어와 다르게 자동으로 다음 case로 넘어가지 않는다.
- 다음 case도 실행하려면, `fallthrough`를 사용해 주어야한다.
- 범위(1...3), 튜플, 조건(where절) 등을 사용 가능하다.
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
