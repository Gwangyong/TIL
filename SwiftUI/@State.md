# [SwiftUI] @State란?
> **Status**: ✅ **학습 완료**<br>**Blog**: 

SwiftUI의 View가 기본적으로 struct 즉, 값 타입이라서 내부 프로퍼티를 마음대로 변경할 수 없다. 그래서 사용되는 `@State`에 대해서 정리했다.

## 그 전에, @는 뭘까?

`@state`, `@Binding`, `@ObervedObject` 등에 붙는 `@`는 **Property Wrapper** 문법이다.

말 그대로 변수에 추가적인 기능을 감싸준다는 개념인데, 값이 읽히거나 쓰일떄 내부적으로 확장된 동작을 수행할 수 있게 해준다.



## `@State`가 하는 일

`@State`가 하는 일은 크게 2가지이다.

첫 번째는 struct 안에서도 프로퍼티를 수정할 수 있게 해주는 것. 원래 값 타입이라 불가능한걸 가능하게 만들어준다.

두 번째는 **`@State` 변수가 변경되면 그 변수를 쓰고 있는 View의 body 전체를 다시 그린다.** 이게 UIKit과 다른 SwiftUI에서 UI 업데이트가 일어나는 핵심 원리이다.

> **Apple 공식 예시**

```swift
struct PlayButton: View {
	@State private var isPlaying: Bool = false // Create the state.
	
	var body: some View {
		Button(isPlaying ? "Pause" : "Play") { // Read the state.
			isPlaying.toggle() // Write the state.
		}
	}
}
```

위 예시는 Apple 공식 문서의 예시를 가져왔다.

버튼을 누르면 → `isPlaying`이 바뀌고 → `@State`라서 View가 다시 그려지고 → 버튼 텍스트가 “Play” ↔ “Pause”로 자동으로 바뀐다.

## 정리

정리하면, `@State` 변수를 보면 이렇게 읽으면 된다.

> “이 변수가 바뀌면, 이 변수를 쓰는 View는 자동으로 다시 그려진다.”

선언 → 변경 → 리렌더링, 이 세 단계가 `@State`의 전부다. 단순하지만 SwiftUI의 반응형 UI가 동작하는 기본 원리이다.