# 📘 Swift 알고리즘에 자주 사용되는 문법 정리

> ✏️ 알고리즘 문제 풀이에서 자주 쓰는 Swift 문법, 메서드, 함수 정리 

## 입/출력 처리 (Input / Output)


### 키보드 값 입력받기

```swift
let input = readLine() // return 값은 Optional String 형식

let input = readLine()! // return 값은 String 형식

// Int 값 입력받기
let input = Int(readLine()!)!
```

### 키보드 입력받은 값 공백으로 구분하기

1. **split()** 으로 구분 (예시: 1 2 3 4)
```swift
var nums = readLine()!.split(separator: " ") // ["1", "2", "3", "4"]
```

2. **components()** 로 구분 (예시: 1 2 3 4)
```swift
import Foundation

var nums = readLine()!.components(separatedBy: " ") // ["1", "2", "3", "4"]
```

components()를 사용할 경우에는 Foundation을 import 해주어야 하지만, split() 함수는 Swift Standard library 에 속해있기 때문에 별도로 Foundation을 import 해주지 않아도 괜찮다.

- [components와 split 함수 정리한 글](https://jud00.tistory.com/entry/Swift-%EB%AC%B8%EC%9E%90%EC%97%B4-%EB%82%98%EB%88%84%EA%B8%B0-split%EA%B3%BC-Components-%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)


### N개의 줄만큼 입력받기
```swift
let line = Int(readLine()!)!
var result: [Int] = []

for _ in 0..<line { result.append(Int(readLine()!)!) }

print(result)

// 입력
// 4 (n개의 줄)
// 5
// 7
// 2
// 9

// 출력
// [5, 7, 2, 9]
```


### print(_:separator:terminator:)

- separator: 각 항목 사이에 출력할 문자열. 기본값은 공백(" ")
- terminator: 모든 항목이 출력된 후 출력될 문자열. 기본값은 줄바꿈("\n")

```swift
// separator 사용 예시 (공백대신 -을 넣어줌)
print(1, 2, 3, 4, separator: "-") // 1-2-3-4
```

```swift
// terminator 사용 예시 (줄 바꿈 대신 ...을 넣어줌)
print("Loading", terminator: "...")
print("Done!")
// Loading...Done!
```





## 배열 관련(Array)


### 오름차순/내림차순 정렬
- 기본으로는 `sort(by: <)`의 형태이다.
- `sort(by: <)`는 오름차순 정렬이며, Swift의 기본 정렬 기준이 오름차순(<)이기 때문에 `sort()`로 생략하여 사용이 가능하다.
- `sort(by: >)`는 내림차순 정렬이며, 기본 정렬 기준이 아니기 때문에 ()안에 `by: >`를 반드시 명시해야한다.
- 원본 배열을 변경하는데, `sorted()`를 사용하면 복사본을 반환하게 된다,
```swift
// sort() 예시
var a = [5, 1, 4, 2, 3]

a.sort()
print(a) // [1, 2, 3, 4, 5] - 생략된 오름차순

a.sort(by: <)
print(a) // [1, 2, 3, 4, 5] - 명시된 오름차순

a.sort(by: >)
print(a) // [5, 4, 3, 2, 1] - 명시된 내림차순 (생략 불가)
```

```swift
// sorted() 예시
var b = [5, 1, 4, 2, 3]

let sortedArr = b.sorted() // 생략된 오름차순 복사본
print(sortedArr) // [1, 2, 3, 4, 5]

let sortedArr = b.sorted(by: <) // 명시된 오름차순 복사본
print(sortedArr) // [1, 2, 3, 4, 5]

let sortedArr = b.sorted(by: >) // 명시된 내림차순 복사본 (생략 불가)
print(sortedArr) // [5, 4, 3, 2, 1]
```

### 배열 뒤집기
- `reverse()`, `reversed()`를 사용하여 배열을 뒤집음
- `reverse()`는 반환값이 없고, 원본 배열을 직접 뒤집는다.
- 원본 배열을 변경하지 않고, 뒤집힌 복사본을 반환하려면 `reversed()`를 사용하면 된다.

```swift
// reverse() 예시
var arr = [1, 2, 3, 4]
arr.reverse()
print(arr) // [4, 3, 2, 1]
// reverse()는 반환값이 없기에, let result = arr.reverse()를 작성하게 되면
// print(result)로 출력하면 결과로 Void 값인 ()만 출력된다.
```

```swift
// reversed() 예시
let arr = [1, 2, 3, 4]
let reversedArr = arr.reversed()
print(Array(reversedArr)) // [4, 3, 2, 1]
```
- reversed()는 `ReversedCollection<Array<Element>>` 타입을 반환함
- 그렇기에 보통 Array()로 감싸 배열로 변환해서 사용한다.


### joined() 메서드를 사용한 값 합치기
- joined() 메서드는 배열 안의 시퀀스(문자열, 배열 등)를 하나로 이어 붙인다. 

```swift
let words = ["Hello", "World"]
let result = words.joined()
print(result) // HelloWorld
```

```swift
// separator(구분자)를 지정하면 원하는 문자열로 연결할 수 있다.
let words = ["Hello", "World"]
let result = words.joined(separator: "-")
print(result) // Hello-World
```

```swift
// 2차원 배열을 1차원 배열로 펼치기
let numbers = [[1, 2], [3, 4], [5, 6]]
let flattened = numbers.joined()
print(Array(flattened))  // [1, 2, 3, 4, 5, 6]
```

> 문자열 배열의 모든 원소를 순서대로 이어붙인 결과를 반환하는 코드 (프로그래머스 문제 예시)
```swift
func solution(_ arr:[String]) -> String {
    return arr.joined()
}

print(solution(["a", "b", "c"]))
// 출력 : abc
```

## 수학 관련 (Math)

### 절대값 변환

```swift
abs(-31) // 31
abs(31) // 31
```

### max(), min() 함수
- max(): 전달인자 중 가장 큰 값을 옵셔널로 반환함
- min(): 전달인자 중 가장 작은 값을 옵셔널로 반환함
- max(_:_:), min(_:_:)는 두 값을 비교할 때 사용하는 전역 함수이며, 반환값은 옵셔널이 아니다.

```swift
let heights = [67.5, 65.7, 64.3, 61.1, 58.5, 60.3, 64.9]
let greatestHeight = heights.max()!
print(greatestHeight) // 67.5

let smallestHeight = heights.min()!
print(smallestHeight) // 58.5
```

```swift
// 값 비교에도 사용 가능 max(_:_:)
let a = 100
let b = 20

let bigger = max(a, b)
print("더 큰 값은:", bigger) // 더 큰 값은: 100

// min(_:_:)
let smaller = min(a, b)
print("더 작은 값은:", smaller) // 더 작은 값은: 20
```


### 제곱 쉽게 구하기(pow)
- `pow(_:_:)`는 **Double 타입을 인자로 받는 함수**이다.
- pow(_:_:)는 Foundation 프레임워크에 정의되어 있는 함수이므로, 사용하려면 `import Foundation`이 필요하다
- Int 타입에는 직접 사용할 수 없으며, 필요하다면 Double로 형 변환해야 한다.
- Float 타입을 사용하고 싶다면, powf(_:_:)를 사용해야 한다.

```swift
import Foundation

var number: Double = 2.0
print(pow(number, 3)) // 8.0 -> (2의 3제곱)
```


### 배수인지 확인하는 메서드 isMultiple(of: )
- 해당 값이 주어진 수의 배수인지 여부를 Bool로 반환한다.
```swift
let number = 10
if number.isMultiple(of: 2) {
    print("\(number) is a multiple of 2")
}
```

- isMultiple(of: ) 메서드로 짝수와 홀수를 구분할 수 있다.
```swift
// 짝수인지 확인
number.isMultiple(of: 2) // true

// 홀수인지 확인(느낌표)
!number.isMultiple(of: 2) // true
```


### stride()
- stride()는 숫자 범위를 일정한 간격으로 순회할 수 있도록 도와주는 함수이다.
- `stride(from:to:by:)`와 `stride(from:through:by:)` 두 가지 형태가 있다.
- `from`(시작 값)부터 `to`(도착 전 값) 또는 `through`(도착 값)까지 `by`(증가 또는 감소 간격)만큼 진행한다.
- `to`는 **끝 값을 포함하지 않으며**, `through`는 **끝 값을 포함한다**.

> for문과 stride 함수 같이 사용 
```swift
let input = Int(readLine()!)!

// stride(from:to:by:) -> 0은 포함되지 않음
for i in stride(from: input, to: 0, by: -1) { 
    print(i, terminator: " ")
}
// 입력: 5 -> 출력: 5 4 3 2 1

// stride(from:through:by:) -> 0까지 포함
for i in stride(from: input, through: 0, by: -1) { 
    print(i, terminator: " ")
}
// 입력: 5 -> 출력: 5 4 3 2 1 0
```

위 아래의 차이는, **to이냐 through이냐의 차이**점이다. 자세한 내용을 알고 싶다면, [stride 함수](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-stride-%ED%95%A8%EC%88%98-%EB%B0%B1%EC%A4%80-2742%EB%B2%88-%EA%B8%B0%EC%B0%8D-N-%EC%97%AD%EC%88%98-%EA%B5%AC%ED%95%98%EA%B8%B0?category=1010119)를 보자.







## 반복문 (Loops)
- forEach
- while
- enumerated

## 조건문 / 흐름 제어
- guard let 
- switch

## 고차함수

### map (각 요소를 변형하기)
```swift
let numbers = [1, 2, 3, 4, 5]
let squared = numbers.map { $0 * $0 }
print(squared) // [1, 4, 9, 16, 25]
```

### filter (조건에 맞는 요소만 걸러내기)
```swift
let numbers = [1, 2, 3, 4, 5]
let even = numbers.filter { $0 % 2 == 0 }
print(even) // [2, 4]
```

### reduce (값을 하나로 합치기)
```swift
let numbers = [1, 2, 3, 4, 5]
let sum = numbers.reduce(0, +) // reduce(초기값, 수식)
print(sum) // 15
```

- compactMap
- flatMap

## 문자열 관련
- uppercased
- lowercased
- asciiValue

### 대/소문자 구별
```swift
let x = "x" as Character
let y = "Y" as Character

print(x.isLowercase) // true
print(x.isUppercase) // false

print(y.isLowercase) // false
print(y.isUppercase) // true
// 두 메서드 모두 Bool을 반환한다.
```

### 대/소문자 변경
```swift
let americano = "AmerICaNo"
print(americano.lowercased()) // "americano" (소문자로 변환)
print(americano.uppercased()) // "AMERICANO" (대문자로 변환)

// 두 메서드 모두 String을 반환한다.
```


