# 고차함수
먼저, 고차함수에 대해 알아보자.

고차함수는 **다른 함수를 전달 인자로 받거나 함수 실행의 결과를 함수로 반환하는 함수**이다.

스위프트에서 제공하는 고차함수는 `map, filter, reduce` 3가지가 있으며, 컨테이너 타입 (Array, Set, Dictionary 등)에 구현되어 있다.

<br>

# map(변형)
`map`은 컨테이너 내부에 **기존 데이터를 변형(transform)하여 새로운 컨테이너를 생성한다.** 

다만, 새로운 컨테이너를 생성한 것이기 때문에, **기존의 데이터는 변하지 않는다.**

map은 for-in 구문과 큰 차이점은 없지만, map을 사용하면 **코드의 간결성, 재사용 용이성, 컴파일러 최적화 성능이 좋다**는 장점이 있다.

<br>

for-in 과 map 메서드를 비교해보자.

**for-in**
```swift
let numbers: [Int] = [0, 1, 2, 3]
var doubleNumbers: [Int] = [Int]()

for number in numbers {
    doubleNumbers.append(number * 2)
}

print(doubleNumbers) // [0, 2, 4, 6]

// 아래와 같이 기존의 데이터는 변하지 않음.
print(numbers) // [0, 1, 2, 3]
```

**map**
```swift
let numbers: [Int] = [0, 1, 2, 3]
let doubleNumbers: [Int] = numbers.map { (number: Int) -> Int in
    return number * 2
}

print(doubleNumbers) // [0, 2, 4 ,6]
```

위의 코드처럼, map 메서드를 사용하면 코드가 더욱 간결해지는걸 볼 수 있다.

<br>

위의 코드에서 **매개변수 및 반환 타입, 반환 키워드(return)** 를 생략하고, **후행 클로저**를 사용하면 아래와 같이 코드가 더 간략해질 수 있다.

**map 축약**

```swift
let numbers: [Int] = [0, 1, 2, 3]
let doubleNumbers: [Int] = numbers.map { $0 * 2 }

print(doubleNumbers) // [0, 2, 4, 6]

// 동일하게 numbers의 값은 [0, 1, 2, 3]으로 기존의 데이터는 변하지 않음.
```

<br>

# filter(추출)
`filter`는 **컨테이너 내부에 값을 걸러서 새로운 컨테이너로 추출한다.**  **반환 타입은 `Bool`** 이며, `true`이면 값을 포함하고, `false`이면 값을 포함하지 않는다.

<br>

for-in 과 filter 메서드를 비교해보자.

**for-in**

```swift
let numbers: [Int] = [0, 1, 2, 3, 4, 5]
var evenNumbers: [Int] = [Int]()

for number in numbers {
    if number % 2 == 0 {
        evenNumbers.append(number)
    }
}

print(evenNumbers) // [0, 2, 4]
print(numbers) // [0 ,1, 2, 3, 4, 5]
```

이처럼 2의 배수를 찾거나 하는 식으로 값을 걸러내어 사용할 수 있다.

<br>

**filter**

```swift
let numbers: [Int] = [0, 1, 2, 3, 4, 5]
let evenNumbers: [Int] = numbers.filter { (number: Int) -> Bool in
    return number % 2 == 0
}

print(evenNumbers) // [0, 2, 4]
print(numbers) // [0, 1, 2, 3, 4, 5]
```

이처럼 filter 메서드를 사용하면 for-in 문에 비해 코드가 보기쉽고 간략화된 것을 볼 수 있다. 또한, 아래와 같이 map 메서드와 동일하게 생략도 할 수 있다.

**filter 축약**

```swift
let numbers: [Int] = [0, 1, 2, 3, 4, 5]
let evenNumbers: [Int] = numbers.filter { $0 % 2 == 0 }

print(evenNumbers) // [0, 2, 4]
print(numbers) // [0, 1, 2, 3, 4, 5]
```

<br>

# reduce(결합)
`reduce`는 **컨테이너 내부의 요소를 하나로 통합**시켜준다.

첫 번째 매개변수를 통해 **초기값**을 지정해줄 수 있으며, 정수 배열이라면 연산 결과를 합치고 문자열 배열이라면 문자열을 하나로 통합하는 일을 해준다.

<br>

for-in 과 reduce 메서드를 비교해보자.

**for-in**
```swift
let numbers: [Int] = [0, 1, 2, 3, 4, 5]
var reduceResult: Int = 0

for number in numbers {
    reduceResult += number
}

print("reduceResult: \(reduceResult)") // reduceResult: 15
print(numbers) // [0, 1, 2, 3, 4, 5]
```

**reduce**

```swift
let numbers: [Int] = [0, 1, 2, 3, 4, 5]
let reduceResult: Int = numbers.reduce(0) {
    (result: Int, next: Int) -> Int in
    print("\(result) + \(next)")
    return result + next
}

print("reduceResult: \(reduceResult)")
// 0 + 0
// 0 + 1
// 1 + 2
// 3 + 3
// 6 + 4
// 10 + 5
// reduceResult: 15

print(numbers)
// [0, 1, 2, 3, 4, 5]
```
`numbers`배열에 초기값을 만들어준 후, `reduce` 메서드 첫 번째 매개변수의 초기값을 0으로 설정해주었으며, 두 번째 매개변수 클로저를 보면 `result`와 `next`를 더해서 Int형태로 반환해준다.

이렇게 되면 `numbers`배열에 있는 각 요소들은 더해지며 `reduceResult` 변수에 대입된다.

여기서 **result 매개변수는 누적값**을 뜻하며, **next 매개변수는 배열의 요소값**을 뜻한다. 

<br>

만약, 초기값인 `numbers.reduce(0)` 를 `numbers.reduce(5)` 로 변경해 주었을 경우, 초기값이 0이 아닌 5이기 때문에 출력 결과는 아래와 같이 나오게된다.
```swift
print("reduceResult: \(reduceResult)")
// 5 + 0
// 5 + 1
// 6 + 2
// 8 + 3
// 11 + 4
// 15 + 5
// reduceResult: 20

print(numbers)
// [0, 1, 2, 3, 4, 5]
```

또한, reduce도 map과 filter와 마찬가지로 여러가지 생략이 가능하다.

**reduce 축약**
```swift
let numbers: [Int] = [0, 1, 2, 3, 4, 5]
let reduceResult: Int = numbers.reduce(0) { $0 + $1 }

print(reduceResult) // 15
print(numbers) // [0, 1, 2, 3, 4, 5]
```
