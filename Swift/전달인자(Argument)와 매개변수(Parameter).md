[이 내용을 정리한 개인 기술 블로그](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-%EC%A0%84%EB%8B%AC%EC%9D%B8%EC%9E%90Argument%EC%99%80-%EB%A7%A4%EA%B0%9C%EB%B3%80%EC%88%98Parameter)

아래의 명령어를 예시로 해서, 전달인자(Argument)와 매개변수(Parameter)를 설명하겠다.
```swift
func sum(a: Int, b: Int) -> Int {
    return a + b
}

sum(a: 5, b: 10)
```

<br>

# 전달인자(Argument)
전달인자 라는 말은 말 그대로 "전달"하는 인자이다.
```swift
sum(a: 5, b: 10)
```
위의 예시 코드중에 한 부분인 바로 위의 코드에서 5, 10이 전달인자. 즉, Argument이다.<br>
**"인자"** 즉,  **"값"을 의미**한다.

<br>

# 매개변수(Parameter)
매개변수도 코드로 예시를 들면
```swift
func sum(a: Int, b: Int) -> Int {
    return a + b
}
```
이 부분에서 a, b를 의미한다.<br>
이름부터 매개"변수"이다. 위에서 **전달되는 인자를 받아들이는 "변수"이다.**

<br>

이름은 어렵게 느껴졌지만, 한 번 공부해보면 엄청 간단한 내용이라는걸 알 수 있다.

간단히 정리하면, "전달인자(Argument)"는 **값을 전달**하고, "매개변수(Parameter)"라는 **"변수"가 전달된 값을 받는다.**