## In-Out은 왜 사용하는 것 일까?
C, C++, Python, Java 등의 언어에서 함수의 파라미터는 변수로 사용된다. 그러면 Swift도 변수일까?

답은 그렇지 않다. Swift 에서는 `상수(Constant)`로 사용되며, 인자값을 변경해주려면 컴파일 오류가 발생한다.

그렇다면, 메서드 내에서 인자값을 변경하고, 원본 변수에도 영향을 주어서 그 변수에서 벗어나더라도 값이 유지가 되게 하려면 어떻게 해야할까??

위의 질문과 같이 인자값을 변경해주기 위해서는 함수 안에서 지역변수의 선언을 통해 값을 대입주는 과정이 필요한데, 그 값은 함수를 벗어나면 사라지기 때문에 그 값을 유지시켜주기 위하여 in-out 매개변수를 사용하는 것이다.

<br>

## In-Out Parameter
in-out 매개변수는 메서드 인자 앞에 `inout` 키워드를 붙여서 `in-out parameter`를 사용할 수 있으며, 상수와 리터럴 값은 in-out 매개변수로서 사용될 수 없기 때문에, in-out 매개변수를 사용하려면 매개 변수로는 상수가 아닌 `변수(variable)`을 넘겨주어야 한다.

또한, in-out 매개변수로 전달할 때, 전달한 변수 앞에는 `'&'` 문자를 표시하여 해당 변수가 in-out 매개변수로서 사용될 것이다. 라고 알려주어야 한다.

in-out 매개변수는 copy-in copy-out이라는 동작 방식으로 전달된다.

in-out parameter 예시
```swift
func swapTwoInts(_ a: inout Int, _ b: inout Int) { // a = 2, b = 16
	let temporaryA = a // temporaryA = 2
	a = b // a = b(16)
	b = temporaryA // b = a(2)
}

var firstInt = 2
var secondInt = 16
swapTwoInts(&firstInt, &secondInt)
print("firstInt is \(firstInt) and secondInt is \(secondInt)")

// "firstInt is 16 and secondInt is 2"
```

<br>

##  copy-in copy-out

copy-in copy-out 동작 방식은 아래와 같다.
1. 함수가 호출되면, 매개변수로 넘겨진 변수가 복사된다.
2. 함수 본문에서 복사한 값을 변화시킨다. (예시 코드에서 a와 b로 값을 바꿔주는 부분.)
3. 함수가 반환되면 복사본의 값이 원래 원본 변수에 할당된다.

copy-in copy-out은 안으로 복사되고, 다시 바깥으로 복사된다는 뜻이다.

<br>

> 참고 자료
> - [Swift 언어 가이드 - Functions](https://docs.swift.org/swift-book/LanguageGuide/Functions.html)
> - [Swift 문법, in-out 매개변수 특징 및 사용방법](https://0urtrees.tistory.com/128)