## readLine()

swift로 알고리즘 문제를 풀 경우(특히 백준 알고리즘 입력 받을 경우)에는 `readLine()` 를 사용해야한다.

<img width="743" alt="스크린샷 2021-10-02 오후 4 22 22" src="https://user-images.githubusercontent.com/59376200/135711221-4e25e334-b883-4843-9569-5f148176acbb.png">

Playground에서는 이 readLine()를 사용할 수 없고 위의 사진처럼 Xcode에서 프로젝트를 생성할 때, `Command Line Tool`로 프로젝트를 생성해야한다.

readLine() 를 사용하면 콘솔창에 텍스트를 입력할 수 있다.

또한, 문제를 풀기 위해서는 nil을 입력받을 수 없기 때문에 `강제 언래핑(!)`을 사용해야한다.

<br>

### 1. 한 줄만 입력받는 경우
```swift
let input = readLine()!
// 물론, 두 줄을 입력받을 경우에는 위의 코드를 2번 작성해주면 된다.

// Int형태로 받는 경우
let input = Int(readLine()!)!

```

<br>

### 2. 한 줄에 2개 이상의 값을 입력받는 경우
```swift
let input = readLine()!.split(separator: " ") // 매개변수로 받아서 해당 인자를 기준으로 쪼개준다.
let input = readLine()!.components(separatedBy: " ") // 위와 동일

// map 함수를 이용해서 Int형태로
let input = readLine()!.split(separator: " ").map { Int($0)! }
let input = readLine()!.components(separatedBy: " ").map { Int($0)! }

// 위에서 split와 components 2가지 방식을 하였고 출력도 동일하다. 하지만 다른점이 있어서 밑에서 설명할 것이다.
```

<br>

## split VS components

위에서 입력받는 경우에 `split`와 `components` 2가지의 방법을 사용했지만, 무엇이 다른건지에 대해 설명하지는 않았다.

이번에는 split와 components의 차이점을 알아보도록 하자.

우선, split와 components의 다른점 중 하나는 타입이 다르다는 점이다. 

아래 사진을 확인해보자.

<img width="455" alt="스크린샷 2021-10-02 오후 7 20 23" src="https://user-images.githubusercontent.com/59376200/135712245-abfb32a9-7545-4661-a767-c3bd24cb8c8d.png"> <br>

<img width="219" alt="스크린샷 2021-10-02 오후 7 21 14" src="https://user-images.githubusercontent.com/59376200/135712265-29c67e6d-670c-4da6-87d1-f3cee273dbeb.png">

이렇게 결과만 확인했을 경우에 값이 동일하며 다른점은 보이지 않는다. 그러면 이제 타입을 확인해보도록 하자.

<img width="217" alt="스크린샷 2021-10-02 오후 7 27 11" src="https://user-images.githubusercontent.com/59376200/135712410-e6168cb4-d5f2-4ebf-9393-5b3f806098bc.png">


위의 사진과 같이, 값은 똑같을지 몰라도 타입이 다른것이 보인다. 

즉, **split로 출력한 값은 "Substring" 타입이며, components로 출력한 값은 "String" 타입** 이라는 것을 알 수 있다.

split로 나누어서 리턴된 Substring 타입을 변환하려면, map 함수를 이용해서 타입을 변환해주면 해결된다.

<br>


이 부분만 보게되면 String 타입으로 해주는 components를 사용하는게 좋아보이지만, **components를 사용하려면 Foundation 프레임워크를 import** 해주지않으면 사용하지 못한다.

그러니 사용에 유의해서 원하는 것을 사용하면 될 것이다.

<br>

## 간단 정리

|  `split`  |  `split`  |  `components`  |
|:----------:|:----------:|:-------------:|
| `import Foundation 여부 ` | import (X) |  import (O)  |
| `Return Type` | [Substring] |   [String]    |
| `장점` | Foundation을 없이 사용 가능, 더 빠름 | Return Type이 [String]이다. |
| `단점` | Return Type이 [Substring]이다. | 상대적으로 조금 느림 |