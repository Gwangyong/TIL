# [SwiftUI] @Binding이란?
> **Status**: ✅ **학습 완료**<br>**Blog**: 


## `@Binding`은 무엇인가

- `@Binding`은 데이터의 **양방향 바인딩**을 구현하기 위해서 사용되는 속성 래퍼이다.
- `@Binding`은 속성 값 자체를 저장하는 것이 아니라, **값의 참조를 저장**한다.
    - 따라서 **부모 뷰와 자식 뷰가 서로 같은 데이터를 참조**하게 된다.
- 뷰 간에 데이터를 공유하고 업데이트하는데 사용된다.
- `@Binding`으로 선언된 파라미터에 값을 넘길 때, `@State`변수 앞에 `$`를 붙여 `Binding`타입으로 변환해서 전달해야 한다.

<br>

## `$`는 뭐지?

`$`는 `Binding` 타입으로 바꿔주는걸로 보이는데 뭔가 더 있을까? 하고 찾아보니, 프로퍼티 래퍼의 `projectedValue`에 접근하는 문법이라고 한다.

`projectedValue`는 간단히 얘기하면, 그 프로퍼티 래퍼가 추가로 정의한 노출 값이다. 무엇을 반환할지는 래퍼마다 다르다.

`@State`의 경우 `projectedValue`가 `Binding<T>`를 반환하도록 정의되어 있어서 결과적으로 `Binding` 타입이 되는것이다.

즉, `$`는 단순히 타입을 바꿔주는 기호가 아니라, 프로퍼티 래퍼가 제공하는 `projectedValue`에 접근하는 문법이다. `@State`의 경우 그게 `Binding<T>`이기 때문에 양방향 연결이 가능한 것이다.

```swift
@State var count = 0

count // Int (wrappedValue)
$count // Binding<Int> (projectedValue)
```

<br>

## Int 예시

```swift
struct SubView: View {
  @Binding var number: Int
  
  var body: some View {
    Button("버튼 뷰2: \n현재숫자: \(number) -> 다음숫자: \(number + 1)") {
      number += 1
    }
    Text("텍스트뷰2: \(number)")
    Text("텍스트뷰3: \(number)")
  }
}

struct ContentView: View {
  @State var number = 0
  
  var body: some View {
    VStack {
      Button("버튼 뷰1: \n현재숫자: \(number) -> 다음숫자: \(number + 1)") {
        number += 1
      }
      Text("텍스트뷰1: \(number)")
      SubView(number: $number)
    }
  }
}
```

이러면 아래 영상처럼 `@Binding`으로 받은 number의 값이 @State와 연동되서 잘 바뀌는걸 확인할 수 있다.

https://github.com/user-attachments/assets/5fd2b40b-31ca-4182-b802-38df69e71d3b

<br>

## String 예시

```swift
struct ContentView: View {
  @State var word = ""
  
  var body: some View {
    Text("\(word)")
    TextField("글자 입력", text: $word)
  }
}
```

이처럼 `word`가 보이는 Text와 `$word`를 통해 `@State` 변수 `word` 와 양방향으로 연결된 TextField를 만들었다.

아래와같이 `TextField`의 값을 변경해주면 `@State`로 선언된 `word`의 값이 바뀌고, body가 재계산되면서 Text에 들어가는 `word`의 값도 변경되는걸 볼 수 있다.

https://github.com/user-attachments/assets/b2575a66-8c14-469e-bef0-df20b2bd0c2a