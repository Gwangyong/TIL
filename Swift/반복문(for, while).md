## 반복문이란?
- 반복문이란 코드가 반복적으로 실행되게 만드는 구문을 뜻한다.
- Swift에는 for-in문과 while문이 대표적이다.

<br>

## for-in문

```swift
for element in input {
    // 본문 실행 코드
}
```
for-in문은 범위 연산자를 사용해서 `a...b` 또는 `a..<b` 등으로도 표현해서 사용한다. a...b는 a ~ b까지를 의미하며, a..<b 는 a ~ b -1까지를 의미한다.

스위프트는 다른 언어에서 주로 사용되는 for문과 다르게, for-in을 사용한다.

<br>

## forEach()

```swift
func forEach(_ body: (Int) throws -> Void) rethrows
```
forEach는 위의 형태로 되어있으며, for-in문과 동일하게 각각의 Element 들을 호출한다.

아래의 예시를 보면 금방 이해할 수 있을것이다.
```swift
// for-in
let array = [1, 2, 3, 4]

for num in array {
    print(num)
}
// 1
// 2
// 3
// 4

// forEach
array.forEach {
    print($0)
}
// 1
// 2
// 3
// 4
```

<br>

### for-in과 forEach의 차이점

**forEach**에서는 `break`, `continue` 구문을 사용할 수 없고, return을 통해 빠져나갈 수 있다. 

반면, **for-in**에서는 break, continue를 사용할 수 있고, return을 이용해서 빠져나오려면 에러가 발생한다.

<br>

## while문

```swift
while 조건 {
    // 본문 실행 코드
}
```

<br>

## repeat while문

```swift
repeat {
    // 본문 실행 코드
} while 반복 조건
```

repeat while문은 while문과 조금 다르다.

이는 반복문을 시작시에 일단 본문 실행 코드를 실행시킨 후에 조건을 확인한다. 즉, 조건에 맞지 않으면 for-in문이나 while문에서는 바로 종료되지만, repeate while문은 일단 조건에 맞던 맞지않던 "무조건 1한번은 실행"시킨다는 뜻이다.

<br>

while문은 위와같이 사용하며, 조건식을 검사한 후에 true면 진행하며 false일 경우에는 while문을 종료한다. 또한, 조건문에 true를 넣어주면 `무한 반복`된다.

<br>

### for-in문과 while문, repeat while문의 차이
- for-in문 : 일정 횟수동안 반복해야 하는 경우. (하나씩 꺼내서 처리할 경우)
- while문 : 일정 조건이 유지되는 동안 반복을 계속해야 하는 경우.
- repeat while문 : while문이지만, 무조건 한번은 실행시켜야 하는 경우.