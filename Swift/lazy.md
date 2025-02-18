저번에 swift 언어를 공부하다가, 메모리에 대한 내용을 몰랐기에 넘어갔었는데 이번에 ARC에 대해 공부를 하다가 lazy에 대해 공부하게 되었다.

lazy는 메모리에 관련되어있는 문법 중 하나이다. 간단하게 iOS 개발할 때 왜 메모리를 신경써야하는지 생각해보자.

## iOS 메모리
iOS 앱 개발을 하는 동안, 우리는 어플리케이션에서 사용하는 메모리 양에 대해서 알고있어야한다.

왜냐하면 메모리가 커지면 커질수록 어플리케이션에 **딜레이가 생기고 속도가 느려지거나 앱이 종료될 수 있기 때문**이다. 그렇기에 우리는 앱 개발을 하는 동안에는 메모리에 대해서 항상 신경을 써야하고, 꼭 필요한 경우가 아니라면 **메모리가 많이 사용되는 것은 피해야한다.**

<br>

## 그래서 lazy가 뭔데? 🧐

애플 공식 문서에는 이렇게 작성되어있다.

```
You must always declare a lazy property as a variable (with the var keyword), because its initial value might not be retrieved
until after instance initialization completes. Constant properties must always have a value before initialization completes, 
and therefore cannot be declared as lazy.
```

해석해보자면,

- **lazy는 인스턴스가 최초 사용되기 전까지 초기값이 계산되지 않는 property이다.** 
lazy 변수는 처음부터 사용할지 사용하지 않을지 모르는데 메모리에 올라가는 것 보다, 원할때 사용해서 메모리에 계산되도록 하는 방법이다.

- **lazy는 let 상수 키워드가 아닌, var 변수로 선언해야한다.** 이에 대한 이유는 아래의 lazy 특징에서 살펴보도록 하자.

<br>

## lazy 키워드는 어떠한 경우에 사용될까?

대부분의 사람들이 예시로 많이 드는 **인스타그램** 으로 예시를 들어보자. 
> 인스타그램에서도 이런 방법을 사용하는지는 모르겠지만, 찾아보니 이 예시가 설명하는데에 적합하다 생각해서 인스타그램의 스토리로 예시를 들어봤다.

인스타그램에는 **스토리** 라는 기능이 있다. 계정 주인이 영상이나 사진을 올려서 다른사람들이 볼 수 있도록 하는 기능이다.

이 기능에서 많은 사람들이 스토리를 올리지만, 그 스토리를 내가 꼭 다 볼거라는 그리고 본다해도 지금 당장 본다는 확신은 없다. 만약, **나는 절반정도의 스토리만 볼 것인데 스토리 전부의 메모리에 계산된다면?** _이건 너무 비효율적이지 않은가..._

그래서 이러한 경우에 lazy 키워드를 사용하여 내가 원해서 보는 내용만 메모리에 계산된다면 어플리케이션에 **딜레이나 불필요한 메모리 사용을 피할 수 있다.**

이렇게 생각하면 원하지 않는데 메모리가 올라가지 않고, 내가 원할때만 메모리에 올라가니 아주 좋은 예시라고 생각한다. (어느분이 처음 생각한건지 모르겠지만 이해하기 쉬웠....👍) 

<br>

## lazy 특징

1. **lazy는 let(상수)이 아닌, var(변수)와 함께 사용되어야한다.**
    이는 위에서도 말했었는데 그 이유로는, **최초 사용이 있기 전까지는 초기값이 계산이 되지 않아 초기값이 값이 없고, 초기화가 완료되는 시점이 언제인지 모르기 때문**에 let(상수)이 아닌, 값을 변경해줄 수 있는 **var(변수)로 선언**해야한다.

2. **struct와 class**
    기본적으로 lazy는 struct와 class 에서만 사용이 가능하다.

3. **computed properties와 함께 사용될 수 없다.**
    computed properties는 블록 내부의 코드를 실행한 후 접근을 시도할 때마다 값을 반환하는데, lazy 키워드는 처음에 메모리에 올린 초기값을 계속 사용하기 때문이다.
    
<br>


> Reference
> - [lazy var in ios swift](https://abhimuralidharan.medium.com/lazy-var-in-ios-swift-96c75cb8a13a)
> - [lazy keyword](https://velog.io/@hzw94/Swift-lazy-keyword)