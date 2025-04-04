> 추가할 내용이 있을 때마다 수정하면서 늘려나갈 예정.

## 값 입력 프로젝트 생성

swift 언어로 알고리즘을 풀 경우(특히 백준 알고리즘에서 값을 입력받는 경우)에는 `readLine()`을 사용해야한다.

<img src="https://user-images.githubusercontent.com/59376200/135711221-4e25e334-b883-4843-9569-5f148176acbb.png" width="550" height="400">

## 키보드 값 입력받기
```swift
var input = readLine() // return 값은 Optional String 형식

var input = readLine()! // return 값은 String 형식
```

## Int 값 입력받기
```swift
var input = Int(readLine()!)! // return 값은 Int

var input = Int(String(readLine()!))! // 위보다 조금 더 속도가 빠르다고함.
```

<br>

## 키보드 입력받은 값 공백으로 구분하기

1. **split( )** 으로 구분 (예시: 1 2 3 4)
```swift
var nums = readLine()!.split(seperator: " ") // ["1", "2", "3", "4"]
```

2. **components( )** 로 구분 (예시: 1 2 3 4)
```swift
var nums = readLine()!.components(seperatedBy: " ") // ["1", "2", "3", "4"]
```

코드 예시로는 다를 게 없어 보이지만, components()를 사용할 경우에는 Foundation을 import 해주어야 하지만, split() 함수는 Swift Standard library 에 속해있기 때문에 별도로 Foundation을 import 해주지 않아도 된다.

- [components와 split 함수 정리한 글](https://jud00.tistory.com/entry/Swift-%EB%AC%B8%EC%9E%90%EC%97%B4-%EB%82%98%EB%88%84%EA%B8%B0-split%EA%B3%BC-Components-%EB%A5%BC-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90)

<br>

## N개의 줄만큼 입력받기
```swift
var N = Int(readLine()!)!
var lines = [Int]()
for _ in 0..<N { lines.append(Int(readLine()!)!) }

print(lines)
// 입력
// 4 (N개의 줄)
// 5
// 7
// 2
// 9

// 출력 : [5, 7, 2, 9]

```

<br>

## 배열(Array) 사용

**1. 배열 만들기**
```swift
let arr = [Int]() // 빈 배열
let arr : Array<Int>

let arr = [Int](repeating: 2, count: 5) // 원하는 데이터 타입으로
let arr = Array(repeating: 2, count: 5)
// repeating에 들어간 요소를 count만큼 반복하여 만듦.
// ex) [2, 2, 2, 2, 2]
```

**2. 2차원 배열 만들기**
```swift
let arr = [[Int]]() // 빈 2차원 배열

let arr = [[Int]](repeating: Array(repeating: 2, count: 3), count: 4)
let arr: [[Int]] = Array(repeating: Array(repeating: 2, count: 3), count: 4) 
// ex) [[2, 2, 2], [2, 2, 2], [2, 2, 2], [2, 2, 2]]
```

**3. 임의의 Data 넣어서 만들기**
```swift
let arr = Array(1...5)  // [1, 2, 3, 4, 5]
```

**4. 배열 역순으로 출력**
```swift
arr.reversed()
arr = arr.reversed()
```

**5. 배열 정렬하기**
```swift
// 오름차순. default도 오름차순 (1, 2, 3, 4...)
arr.sort()
arr.sort(by: <)
arr.sorted(by: <) 


// 내림차순 (..., 4, 3, 2, 1)
arr.sort(by: >)
arr.sorted(by: >) 
```

6. 배열 다룰 때 가장 중요한 **map, filter, reduce 고차함수!!**

**map**
```swift
let string = ["1", "2", "3", "4"]
string.map { Int($0)! } // [1, 2, 3, 4] 각 원소를 전부 Int로 맵핑
```

**filter**
```swift
let array = [1, 2, 3, 4]
array.filter { $0 % 2 == 0 } // [2, 4] 조건에 맞는 수만 뽑아냄
```

**reduce**
```swift
let array = [1, 2, 3, 4]
array.reduce(0, +) // 숫자 합이 나타남. 문자열 합치기도 가능
```
[고차함수 자세히 정리](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-%EA%B3%A0%EC%B0%A8-%ED%95%A8%EC%88%98-map-filter-reduce?category=1010119)

<br>

## ETC!

**무한 루프**
```swift
while true {
    ...
}
```

**타입 범위**
```swift
Int, Int64 = 2의 8승 - 1 (9223372036854775807) // 19자리
Int32      = 2의 6승 - 1 (2147483647)          // 10자리
Float      = 소수점 6자리까지 표현 가능
Double     = 소수점 15자리까지 표현 가능
```

**아스키코드(ASCII) 변환**
```swift
// Character to Ascii
Character("a").asciiValue! // return 타입은 UInt8 이며, 값은 97

// Ascii to Character, String
let char = Character(UnicodeScalar(65)) // A
let str = String(UnicodeScalar(97)) // a
```

**절대값 변환**
```swift
abs(-31) // 29
abs(31) // 31
```

**print 줄 바꿈 안하기**
```swift
for i in 1...5 {
    print(i, terminator: " ")
}
// 1, 2, 3, 4, 5
```

**print 중간에 값 넣기**
```swift
print("my", "name", "is", "Miro", separator: "___")
// 출력: my___name___is___Miro
```

**대/소문자 구별**
```swift
let x = "x" as Character
let y = "Y" as Character

print(x.isLowercase) // true
print(x.isUppercase) // false

print(y.isLowercase) // false
print(y.isUppercase) // true
// 두 메서드 모두 Bool을 반환한다.
```

**대/소문자 변경**
```swift
let americano = "AmerICaNo"
print(americano.lowercased()) // "americano" (소문자로 변환)
print(americano.uppercased()) // "AMERICANO" (대문자로 변환)

// 두 메서드 모두 String을 반환한다.
// lowercased()와 uppercased() 모두 시간 복잡도는 O(n)이다.
```

**joined() 메서드를 사용한 값 합치기**
- joined()메서드는 배열 안의 시퀀스(배열, 문자열 등)를 하나로 이어 붙인다. 
```swift
let words = ["Hello", "World"]
let result = words.joined()
print(result) // HelloWorld
```

```swift
// separator(구분자)를 넣는 방법도 있다.
let words = ["Hello", "World"]
let result = words.joined(separator: "-")
print(result) // Hello-World
```

```swift
// 2차원 배열을 1차원 배열로 평평하게 만들기
let numbers = [[1, 2], [3, 4], [5, 6]]
let flattened = numbers.joined()
print(Array(flattened))  // [1, 2, 3, 4, 5, 6]
```

- 프로그래머스 문제 풀면서 작성한 코드 (arr 원소들을 순서대로 이어붙인 문자열로 만들기)
```swift
func solution(_ arr:[String]) -> String {
    return arr.joined()
}

print(solution(["a", "b", "c"]))
// 출력 : abc
```

**for문과 stirde 함수 같이 사용**
```swift
let input = Int(readLine()!)!

for i in stride(from: input, to: 0, by: -1) {
    print(i, terminator: " ")
}
// 입력(input): 5일 경우
// 출력 : 5 4 3 2 1

for i in stride(from: input, through: 0, by: -1) {
    print(i, terminator: " ")
}
// 입력(input): 5일 경우
// 출력: 5 4 3 2 1 0
```

위 아래의 차이는, **to이냐 through이냐의 차이**점이다. 자세한 내용을 알고싶다면, [stride 함수](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-stride-%ED%95%A8%EC%88%98-%EB%B0%B1%EC%A4%80-2742%EB%B2%88-%EA%B8%B0%EC%B0%8D-N-%EC%97%AD%EC%88%98-%EA%B5%AC%ED%95%98%EA%B8%B0?category=1010119)을 보자.
