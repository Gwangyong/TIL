stride라는 함수는 원래는 몰랐는데, 백준의 2741번째 문제를 풀고 기찍N 이라는 2742번을 풀다가 오류가 계속나서 찾아보다가 stride라는 함수를 찾게 되었다.

역순으로 하려면 어떠한 방법들이 있을까 생각이 안나서 stride함수를 찾았다.

그냥 공부만해두고 넘어가기엔 잊어버릴 것 같아서 정리하기로 하였다.

## stride() 함수

<img width="770" alt="스크린샷 2021-10-11 오전 4 09 35" src="https://user-images.githubusercontent.com/59376200/136709915-eadb73ed-7066-47d1-ad93-3c409c4f20ba.png">

우선, stride가 무슨뜻인지 궁금해서 검색을 해보았다. 보폭이라는 뜻으로 나오고 인터넷에서 찾다보니, 보폭만큼 다가간다는 것같다.

그러면 **stride(from: a, to: b, by: c)** 라는 예시를 보았을 때, 번역을 해보면 **a부터 b까지 c(보폭?)만큼 다가간다.** 라는 뜻으로 해석했다.

그렇기에, 2742번에 있는 5를 입력받았을 경우에, **5부터 1까지 역순**으로 출력하는 코드를 작성한다면,
```swift
import Foundation

let number = Int(readLine()!)!

for i in stride(from: number, to: 0, by: -1) {
    print(i)
}
```
위의 코드와 같이 작성할 수 있을 것이다. 

readLine()을 사용하므로, import Foundation이 필수이고 stride 함수를 사용하여, **입력받은 `number`부터 시작해서 `0`의 바로 앞인 1까지 `-1`씩 다가간다는 뜻이다.** 그래서 5부터 시작해서 0의 앞인 1까지 -1씩 가기 때문에, `5, 4, 3, 2, 1`이 출력되게 되는것이다.

여기서 **"5부터 1까지 역순으로 나오는건데, 왜 to에 1이 아닌, 0을 적어야하지?"** 라며 햇갈리는 사람들이 있을 것 같은데, 위에 공식문서에 **Return Value** 부분을 보게되면 **"from의 숫자는 포함하지만 to의 값은 포함하지 않는다"** 고 작성되어있다.

그래서 5부터 포함되지 않는 0까지로 작성해주어서 5부터 1까지 출력되도록 하는 것이다.

<br>

## to대신, through?

<img width="376" alt="스크린샷 2021-10-11 오전 3 39 57" src="https://user-images.githubusercontent.com/59376200/136709079-7ddea12f-18fe-4115-bd82-6501e4509a11.png">

코드를 작성해보니, 궁금한것이 생겼다. to대신 through로 비슷한게 하나 더 있었다.

그럼 through는 뭐가다른가 하고 to대신 through를 작성해 보았는데,

<img width="249" alt="스크린샷 2021-10-11 오전 3 44 26" src="https://user-images.githubusercontent.com/59376200/136709231-1cc9ac4b-c667-4f8a-ae56-ccb4e1764cc0.png">

사진에서 보이듯이, 1이 아닌 0까지 출력되었다. to는 그 파라미터값까지 포함하지 않는것 같은데, through는 포함하는듯하다.

그래도 확신이 필요하여 공식문서를 확인해보았다.

<img width="770" alt="스크린샷 2021-10-11 오전 4 09 25" src="https://user-images.githubusercontent.com/59376200/136709922-5c29e5d6-cb8d-4196-8781-1ecf6bf96f10.png">

여기서도 위에 작성한것과 동일하지만, 여기서도 **Return Value**를 보게되면 `end`도 포함한다. 즉, 위에 작성되어있는 **through의 파라미터는 포함한다는 뜻**이다.

그러면, to대신 through를 사용해서 위와같이 5부터 역순으로 1까지 출력하려면, **through: 0이 아닌, through: 1**로 작성하면 5부터 1까지 제대로 출력이 된다.

<br>

### Plus!!

여기서는 역순으로 하는것이 목표였기 때문에, by: -1을 해주었는데 **당연히 양수로도 가능**하다.
```swift
import Foundation

let number = Int(readLine()!)!

for i in stride(from: number, through: 7, by: 2) {
    print(i)
}
```
라는 코드를 작성해 주었을 경우, 

<img width="223" alt="스크린샷 2021-10-11 오전 4 25 10" src="https://user-images.githubusercontent.com/59376200/136710394-a1e9cd3f-7111-4de6-a249-f2b467087a17.png">


위의 사진과 같이 1, 3, 5, 7이 출력된다.

이유는 알겠지만, `number(1)부터 7까지 2보폭 만큼 다가간다`는 뜻이므로, 1부터 2씩 커지며 6까지인 1, 3, 5, 7가 출력되는 것이다. 

through를 7로 작성해주어서 7이 포함되었지만, **만약 through대신 to: 7로 작성했다면 어떻게 될까?**

당연하게도 to: 7로 작성하면 그 파라미터 값까지 포함하지 않으므로, 1부터 6까지 다가가는걸로 되어서 1, 3, 5만 출력될 것이다.

결론으로는, to와 through는 **"적어준 숫자까지 포함을 하냐, 포함을 하지 않냐"** 의 차이인 것 같으니, 햇갈리지 않게 편한것을 골라서 사용하면 될 것 같다.