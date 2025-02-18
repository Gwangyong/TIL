
### @State와 @Binding을 활용한 상태 관리

SwiftUI에서 뷰의 상태를 관리할 때는 `@State`와 `@Binding`을 활용한다. 각각의 역할과 차이를 이해하면 효율적으로 상태를 제어할 수 있다.

#### @State: 현재 뷰에서만 관리되는 상태 프로퍼티

`@State`는 값의 변화를 감지하여 뷰를 다시 렌더링하도록 하는 속성이다. 주로 현재 뷰 내부에서만 필요한 상태를 저장할 때 사용되며, `String`, `Int` 같은 간단한 타입을 다룰 때 적합하다. 

- `@State` 프로퍼티는 현재 뷰에서만 사용되므로 `private`으로 선언해야 한다.
- 값이 변경되면 SwiftUI가 이를 감지하고 뷰를 자동으로 업데이트한다.
- 값을 저장하는 용도로 사용되며, 다른 뷰와 공유하려면 `@Binding`을 활용해야 한다.

예를 들어, `TextField`는 사용자가 입력하는 값을 저장해야 하므로 `@State` 프로퍼티가 필요하다.

```swift
struct ContentView: View {
    @State private var notificationsEnabled = true
    @State private var email = ""

    var body: some View {
        VStack {
            TextField("이메일 입력: ", text: $email)
            Toggle("알림 활성화", isOn: $notificationsEnabled)
        }
        .padding()
    }
}
```

- `@State private var email = ""` 선언을 통해 상태를 저장할 변수를 만든다.
- `TextField`의 `text` 파라미터에 `$email`을 전달하여, 값이 변경될 때 상태 프로퍼티가 자동으로 업데이트되도록 한다.
- `$email`처럼 앞에 `$`를 붙이면 바인딩(binding)된 값으로 전달할 수 있으며, 값을 읽을 때는 `email`처럼 `$` 없이 사용한다.

---
#### @Binding: 하위 뷰에서 상위 뷰의 상태를 변경할 때 사용

`@State`는 현재 뷰에서만 사용할 수 있지만, 다른 뷰에서도 해당 상태를 사용하려면 `@Binding`을 활용해야 한다. 

예를 들어, `Toggle`을 별도의 뷰로 분리하고, 상위 뷰의 상태를 변경하도록 하려면 다음과 같이 작성할 수 있다.

```swift
struct ToggleView: View {
    @Binding var isEnabled: Bool

    var body: some View {
        Toggle("알림 활성화", isOn: $isEnabled)
    }
}

struct ContentView: View {
    @State private var notificationsEnabled = true

    var body: some View {
        VStack {
            ToggleView(isEnabled: $notificationsEnabled)
        }
        .padding()
    }
}
```

- `@Binding var isEnabled: Bool`을 선언하여 상위 뷰에서 전달받은 값을 바인딩한다.
- `ContentView`에서 `$notificationsEnabled`를 `ToggleView`에 전달하면, `ToggleView`에서 값을 변경해도 `ContentView`의 `notificationsEnabled` 값이 자동으로 업데이트된다.

### @State와 @Binding 정리
| 속성 | 역할 | 사용 예시 |
|------|------|---------|
| `@State` | 현재 뷰에서만 상태 관리 | TextField 입력값, Toggle 상태 |
| `@Binding` | 상위 뷰의 상태를 하위 뷰에서 조작 | 커스텀 Toggle, 버튼 클릭 이벤트 |

이처럼 `@State`와 `@Binding`을 적절히 활용하면, SwiftUI에서 상태를 효율적으로 관리할 수 있다.

