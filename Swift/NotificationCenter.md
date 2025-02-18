## NotificationCenter(NSNotificationCenter)

NotificationCenter란, **등록된 이벤트가 발생되면 해당 event에 대한 행동을 행하는 데이터 전달 방식 중 하나**이다. 

NotificationCenter에 등록되어 있다면 그에 맞는 Notification이 발생할 경우, NotificationCenter에서 그에 맞는 일을 알아서 할당해준다.

이는 **적은 코드로 간단히 구현**할 수 있으며, 앱 내의 어떠한 곳에서 메시지를 던져주면 **다른 어떠한 곳에서든 이 메시지를 받아서 처리**할 수 있다는 장점이 있다.

<br>

## 📌 주요 메소드 설명

### post(name: object: userInfo: )

```swift
func post(name Name: NSNotification.Name, object Object: Any?, 
 userInfo UserInfo: [AnyHashable : Any]? = nil)
```

우선 post 메소드이다. 이 메소드는 **NotificationCenter에서 가장 중요한 핵심** 인데, 정해진 Name 이라는 Notification을 보내는 역할을 한다.

- name : 전달하고자 하는 **notification의 이름**이다. 일을 시킬 사람이나 팀을 부를때 사용되는 이름이라고 생각하면 된다.
- object : **옵저버에게 보내려 하는 객체**이다. 전달할 객체가 없다면 nil을 할당해주면 된다. 
- userInfo : Notification과 관련된 값을 뜻한다. 

<br>

### addObserver(_: selector: name: object: )

```swift
func addObserver(_ observer: Any, 
                selector selector: Selector, 
                name Name: NSNotification.Name?, 
                object Object: Any?)
```

다음은 **addObserver 메소드**이다. 이 메소드는 정해준 **Name의 Notification이 생기면, selector 안의 정해준 함수를 실행** 한다.

메소드에 대해서 보았으니, 예시를 보면서 더 이해해보도록 하자.

<br>

## NotificationCenter 예시!

A라는 사람이 혼자 자그마한 인터넷 쇼핑몰을 한다고 예시를 들어보자.

우선 물건에 대한 `주문(order)`이 들어오면, 그 주문 들어온 `물건(orderedObject)`을 가지고 우체국으로 가서 택배를 붙인다는 시나리오를 생각해보자.

### **1. Notification post**
아래의 코드는 `order` 이라는 notification이 들어오면, 주문 들어온 물건인 `orderedObject` 을 가지고 **post** 해주는 코드이다. (주문들어온 물건의 종류가 많다면 구별을 해줘야하겠지만, 여기서는 orderedObject로 통일해서 간단히 생각하자.)

```swift
NotificationCenter.default.post(name: NSNotification.Name("order"), object: orderedObject)
```

<br>

### **2. Notification Observer**

이제 쇼핑몰을 운영하는 A는 order notification 즉, **주문 알림**이 언제 올지 **관찰**하고 있어야 하므로, 아래의 코드를 작성하자.

```swift
NotificationCenter.default.addObserver(self, 
selector: #selector(checkOrder), 
name: NSNotification.Name("order"), 
object: nil)
```

코드에 대해서 알아보자.

- notification이 오는걸 **관찰하고 있어야 하는 observer**는 `self` 즉, 자기 자신 A씨 본인이 되는것이다.
- order 이라는 이름의 notification을 받았을 경우, 실행해야 하는 행동은 `checkOrder` 함수가 되는 것이다. (함수는 만들어져있다고 생각하자. 아래에 설명하겠다.)
- 마지막으로 어떠한 notification 인지 알아야하므로 그 이름이 `order`이 되는 것이다.

간단히 설명해보면, **A씨 자기자신(`self`) 이 관찰하다가 `order` 라는 notification이 관찰되면 `checkOder` 이라는 미리 만들어둔 함수를 통해 해야할 일을 하는것이다.**

위에서 말한 `checkOrder` 함수는, **post** 에 있던 `orderedObject` 객체를 사용하여 물건을 택배사를 통해서 고객에게 배송하는 코드가 되겠지만, 그 코드를 작성할 능력이 없으니 생략하겠다 ㅎㅎ..


<br>

## NotificationCenter는 왜 사용하지?

보다보면 이런 생각이 들 것이다. 데이터를 이런식으로 전달하는거면 **Delegate를 사용하는 것과 똑같은거같은데 굳이 이걸 왜 쓰지?** 이러한 생각이 들 수 있다.

예시를 하나 들어보자. 일기장 앱이 있는데, 작성한 일기장들을 모아두는 `일기장 목록` 화면과 하나의 일기를 자세하게 보는 `일기장 상세`화면, 즐겨찾기 한 목록들을 모아두는 `즐겨찾기`화면 이렇게 3가지가 있다고 생각하자.

여기에서 delegate를 사용하게 된다면, **일기장 목록에서 일기장 상세 화면으로 들어가는 경우**에 즐겨찾기를 풀거나 일기를 삭제할 수 있다. 이렇게하면 하면 화면상에서 삭제되니 아무런 문제가 없다. 

하지만, 여기에서 삭제한 기능들은 또 코드로 만들어주는 번거로운 작업을 하지 않으면 즐**겨찾기에서 일기장 상세로 들어가는 화면**에서는 원래 그대로 남아있을 것이다.

그렇기에 NotificationCenter을 사용해서 **1:1이 아닌, 1:N 의 상황**에서 사용하면 좋다는 것이다.

예시가 너무 길어서 한 번 요약해본다. 즉, delegate는 1:1의 상황에서 좋은 방법이지만 **VC가 여러개가 된다면 1:N의 상황에서 좋은 NotificationCenter을 사용**하는게 좋을 것이다.

<!-- Blog에 글 작성할 때는 예시 괜찮은지 보고, 수정할 수 있으면 수정해서 글 올리자. -->
<!-- 아래 예시 내가 Diary 만든 강의에 쓴거 보고, 그거 보면서 예시 코드 작성하면 좋을듯? -->

<!-- 

 > Reference
 > - [Notification, NotificationCenter](https://leeari95.tistory.com/49#%E2%9C%94%EF%B8%8F%C2%A0notificationcenter%EB%A1%9C-post%ED%95%98%EA%B8%B0-%EB%B0%9C%EC%86%A1%ED%95%98%EA%B8%B0)
 > - [Apple Developer Documentation](https://developer.apple.com/documentation/foundation/notificationcenter)
 > - [데이터 직접 전달 방식(4) - NotificationCenter을 통해 전달](https://roniruny.tistory.com/152)

  -->