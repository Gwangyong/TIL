- 아래 내용은 블로그 내용을 수정하면서 함께 수정함.
- [정리한 블로그 글 주소](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-stride-%ED%95%A8%EC%88%98-%EB%B0%B1%EC%A4%80-2742%EB%B2%88-%EA%B8%B0%EC%B0%8D-N-%EC%97%AD%EC%88%98-%EA%B5%AC%ED%95%98%EA%B8%B0)

## stride( ) 함수

![스크린샷 2021-10-11 오전 4 09 35](https://user-images.githubusercontent.com/59376200/136709915-eadb73ed-7066-47d1-ad93-3c409c4f20ba.png)



먼저 stride가 무슨 뜻인지 궁금해서 검색을 해보았는데요. 사전적인 의미는 "보폭"이라네요?

코딩에서는 이 의미를 그대로 적용해서 "특정 간격(보폭)만큼 이동"하는 반복을 의미하는 것 같습니다.

또한, 위에 있는 공식문서의 Return Value부분을 보면 "start(from)부터 end(to) 방향으로 가되, end(to)는 포함하지 않는다."라고 작성되어 있습니다.



즉, stride(from: to: by: )는 시작값(from)부터 종료값 바로 전까지(to), 지정한 간격(by)만큼 이동하며 반복하게 되겠네요.



그럼 이제 백준 2742번 "기찍 N" 문제 예시대로 보겠습니다. 
```swift
let number = Int(readLine()!)!

for i in stride(from: number, to: 0, by: -1) {
    print(i)
}
// 입력 : 5
// 출력 : 
// 5
// 4
// 3
// 2
// 1
```

위의 코드를 해설해보자면, number(from)에서 0(to)의 이전 값인 1까지 -1씩 감소하며 출력하는 코드입니다.

입력으로 5를 넣으면, 출력 값으로는 5, 4, 3, 2, 1을 출력하게 되겠네요.





## to: 대신, through: ?

![to:, through: ](https://user-images.githubusercontent.com/59376200/136709079-7ddea12f-18fe-4115-bd82-6501e4509a11.png)


코드를 작성하다가 위의 이미지처럼 to: 대신 through: 를 사용하는 방식이 있더라고요? 그럼 through는 뭐가 다른가 하고 to 대신 through를 사용해봤는데

![스크린샷 2021-10-11 오전 3 44 26](https://user-images.githubusercontent.com/59376200/136709231-1cc9ac4b-c667-4f8a-ae56-ccb4e1764cc0.png)



이미지에서 보이듯이 1이 아닌 0까지 출력되었습니다. 😳

그냥 사용만 해봐도 to: 는 파라미터 값을 포함하지 않고, through는 값을 포함하는거구나! 싶더라고요.



그래도 확신이 필요하여 공식문서를 확인해보았습니다.

![스크린샷 2021-10-11 오전 4 09 25](https://user-images.githubusercontent.com/59376200/136709922-5c29e5d6-cb8d-4196-8781-1ecf6bf96f10.png)



공식문서를 보니, 이번에는 "end(through) 값도 포함한다." 라고 쓰여있습니다. 그럼 정리해보면 아래와 같이 되겠네요.

- through: 는 종료값을 포함
- to: 는 종료값을 제외

따라서 어떤 함수를 써야할지는 문제의 조건과 상황에 따라서 골라 사용하면 될거같네요. 😎


<br>

예시로 오름차순 반복 문제로 to와 through를 한번 더 비교해보겠습니다.
```swift
let number = Int(readLine()!)!

for i in stride(from: number, through: 7, by: 2) {
	print(i)
}
```

위와 같이 코드를 작성하고 number의 값이 1이라면, 1부터 7(포함)까지 2씩 증가할 것이기 때문에, 1, 3, 5, 7이 출력되겠죠?

만약, through를 to: 로 바꾸면 어떻게 될까요? 그러면 to:는 본인을 포함하지 않으니, 7을 제외한 1, 3, 5까지만 출력이 될겁니다.





### 마무리 정리!
- stride(from: to: by: ) : 종료값을 ❌ 포함하지 않음
- stride(from: through: by: ) : 종료값을 ✅ 포함함
- 보폭을 설정해 반복할 수 있어, 오름차순/내림차순 모두 유용하게 사용할 수 있습니다.
- 종료값을 포함해야 하는지, 아닌지에 따라 to와 through를 선택하여 사용할 수 있습니다.

