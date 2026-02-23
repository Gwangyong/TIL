# iOS에서 웹 페이지를 여는 3가지 방식
> **Status**: 🎯 **블로그 발행**<br>**Blog**: [iOS에서 웹 페이지를 여는 3가지 방식](https://velog.io/@key4168/iOS%EC%97%90%EC%84%9C-%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80%EB%A5%BC-%EC%97%AC%EB%8A%94-3%EA%B0%80%EC%A7%80-%EB%B0%A9%EC%8B%9D)


## 1. 외부 Safari로 열기 (앱 밖으로 전환)

버전 제약이 사실상 없다고 봐도 무방하며 **가장 구현하기 간단한 방식**이다.

iOS 전반에서 동작하며, 일반적으로 `iOS 10.0+API` 사용을 권장한다고 한다.

> 코드 예시

```swift
let url = URL(string: "https://example.com")!
UIApplication.shared.open(url) // iOS 10+ 오버로드 사용 권장
// 또는:
UIApplication.shared.open(url, options: [:], completionHandler: nil)
```

현재 설명하는 세 가지 방식 중 가장 단순한 방법이다. URL만 넘겨주면 iOS가 알아서 Safari로 열어주기 때문에 별도로 처리할 것이 거의 없다.

#### **장점**
- 탭, 북마크, 리더 모드, 확장 프로그램, 로그인 상태 등 Safari의 모든 기능을 그대로 활용할 수 있다.
- 앱이 웹 콘텐츠를 직접 관리하지 않아도 되므로 메모리 부담과 예외 처리가 줄어든다.

#### **단점**
- 앱을 완전히 벗어나기 때문에 사용 흐름이 끊기고, 그만큼 이탈률이 높아질 수 있다.

사용자가 Safari에서 계속 탐색하거나 북마크/공유를 원할만한 정보성 페이지에 적합하다.
장시간 웹 브라우징이 필요하거나, 확장 프로그램/북마크 활용이 중요한 경우, 혹은 의도적으로 **앱 밖으로 내보내도 무방한 상황에서 사용할 때 추천**된다.

→ 예: 긴 문서나 블로그 글을 읽고, 저장/공유까지 이어지기를 원할 경우

<br>

## 2. WKWebView (완전 인앱 임베드 웹뷰)

`WKWebView`는 `iOS 8.0+`부터 지원한다.

> 코드 예시
> 

```swift
import WebKit

final class WebVC: UIViewController, WKNavigationDelegate {
  private let webView = WKWebView()

  override func viewDidLoad() {
    super.viewDidLoad()
    view.addSubview(webView)
    webView.navigationDelegate = self
    webView.translatesAutoresizingMaskIntoConstraints = false
    NSLayoutConstraint.activate([
      webView.topAnchor.constraint(equalTo: view.topAnchor),
      webView.leadingAnchor.constraint(equalTo: view.leadingAnchor),
      webView.trailingAnchor.constraint(equalTo: view.trailingAnchor),
      webView.bottomAnchor.constraint(equalTo: view.bottomAnchor)
    ])
    let url = URL(string: "https://example.com")!
    webView.load(URLRequest(url: url))
  }
}
```

화면에 꽉 차게 붙이고 URL 하나 로드만 한 코드이다. 커스터마이징은 전혀 건들지도 않았지만, 앞선 방식에 비해 작성할 코드가 많다.

다만, 그만큼 **커스터마이징 여지도 가장 넓은 방식**이다.


#### **장점**
- UI, 네비게이션, 로딩 인디케이터, 에러 처리 등 **거의 모든 요소를 자유롭게 커스터마이징**할 수 있다.
- `WKScriptMessageHandler`를 통한 양방향 JS통신을 지원해 하이브리드 앱 구현에 적합하다.
- `WKNavigationDelegate`로 특정 요청을 가로채는 등 세밀한 제어가 가능하다.

#### **단점**
- **쿠키와 세션을 직접 관리**해야한다.
- 보안, 접근성, 성능(메모리/캐시, 다크모드, 텍스트 크기 대응 등)도 모두 직접 챙겨야한다.

앱 UI와 완전히 일체화된 웹 기능이 필요할때 사용하면 좋다. 다만, 웹 콘텐츠가 무거울 경우 성능 저하나 발열이 체감될 수 있다는 단점이 있다.

인앱 결제 전용 웹화면, 로그인 연동, 커스텀 툴바/뒤로가기 정책 등 깊은 수준의 제어가 필요한 상황에서 사용하면 좋다.

<br>

## 3. SFSafariViewController (인앱 Safari)

마지막은 `SFSafariViewController` 방식으로, 지원 버전은 `iOS 9.0+` 이다.

> 코드 예시

```swift
import SafariServices

guard let url = URL(string: "https://jud00.tistory.com") else { return }
let safariViewController = SFSafariViewController(url: url)
present(safariViewController, animated: true, completion: nil)
```

위와같이 사용 방법은 매우 단순하다. 그냥 주소를 `SFSafariViewController`에 넣어서 `present`만 해주면 된다.

#### **장점**
- 쿠키/세션 등 Safari와 공유 → 로그인 유지, 폼 작성이 편리하다.
- Apple 제공 보안/접근성/성능 최적화가 그대로 유지
- 앱 안에서 돌아가서 컨텍스트 전환이 최소화된다. (즉, 사용자 이탈이 적음)
- 뒤로가기/Done버튼, 스와이프 제스처, 새로고침 등의 기능을 **기본적으로 지원**한다.

#### **단점**
- 커스터마이징 제약(툴바 색 정도만 가능. 네비게이션 아이템 커스텀 불가능)
- 세밀한 네비게이션 제어가 불가능하다.

`SFSafariViewController`는 사용자 입장에서 **"앱 안에 내장된 Safari"** 같은 느낌을 준다. 실제 Safari 앱으로 빠져나가는게 아니라 앱 내부에서 웹 페이지를 보여주는 방식이라, 사용자가 익숙한 브라우저 UX를 그대로 느끼면서도 **앱으로 돌아오기가 매우 쉽다.**

추가로 문의/설문, 약관, 개인정보 처리방침, 블로그처럼 외부 페이지를 띄워야 할 때 사용하며, **앱 밖으로 사용자가 이탈하는걸 막고 흐름을 자연스럽게 유지하고 싶을 때 추천되는 방식**이다.

<br>

## 선택한 방식과 그 이유

이번에 Podoit 앱을 구현할 때 선택한 방식은 마지막에 설명한 `SFSafariViewController` 방식이다.

첫 번째로 `UIApplication.shared.open`의 Safari로 이동하는 방식은 구현이 가장 단순하지만, **사용자가 앱을 벗어나 이탈할 수 있는 확률**이 늘어나기에 "앱 내 체류 시간을 늘리고 싶다." 는 팀 내 공통된 의견이 있어서 제외했다.

다음으로 `WKWebView`는 커스터마이징 측면에서 가장 뛰어나지만, 구글 폼 하나를 띄우는 용도로 쓰기엔 **오버엔지니어링**이라고 판단했다.

결과적으로 `SFSafariViewController`는 구현도 간단하고, 사용자가 Done 버튼이나 스와이프 한 번으로 앱으로 바로 돌아올 수 있기에 이 상황에 가장 적합하다고 판단되어 최종적으로 이 방식을 선택했다.


> 아래는 구현한 GIF (임시 블로그 주소로 테스트한 모습)

![문의 건의하기](https://velog.velcdn.com/images/key4168/post/8d34ae4c-af1a-41f6-911c-84d801dad597/image.gif)
