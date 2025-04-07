## 오토 레이아웃(AutoLayout) 이란?

AutoLayout이란, 뷰들 사이의 **제약 조건(Constraints)** 을 이용해 뷰의 위치와 크기를 설정하는 방식이다.

아이폰의 **다양한 해상도와 화면 크기**를 지원하기 위해 나온 개념이며, 기기의 크기가 달라져도 일관된 UI를 보여줄 수 있도록 도와준다.

또한, AutoLayout은 세로보기 뿐 아니라 가로보기 화면도 지원한다.

Xcode의 오른쪽 아래 **Add New Constrains** 버튼을 통해 설정이 가능하며, 아래 이미지를 기준으로 **시계 방향 순서대로 Top -> Trailing -> Bottom -> Leading**이다. 

![image](https://user-images.githubusercontent.com/59376200/150970054-a90fbf21-c822-4212-a405-9bc4e4cfcfe1.png) 

![image](https://user-images.githubusercontent.com/59376200/150969468-ed5ea037-bd0d-4671-bafd-e59d56261489.png)

<br>

## Top, Bottom vs Leading, Trailing

Top, Bottom은 각각 위쪽과 아래쪽의 제약을 설정하는 것이고, Left, Right는 왼쪽, 오른쪽의 제약을 설정하는 것이다.

하지만 Auto Layout에서는 Left, Right보다 **보통 Leading, Trailing을 사용**한다. 

### Left, Right
우리나라는 왼쪽 -> 오른쪽으로 글을 쓰지만, 아랍권 같은 경우는 오른쪽 -> 왼쪽으로 글을 작성한다.
Left, Right는 언어 방향과 관계없이 항상 화면의 **"물리적인" 왼쪽, 오른쪽 방향을 의미**한다.


### Leading, Trailing
Leading, Trailing은 왼쪽, 오른쪽의 개념이 아닌, **텍스트의 시작과 끝**이 기준이다.
- Leading: Text가 시작되는 지점
- Trailing: Text가 끝나는 지점

그로인해 아래와 같이 **언어마다 방향이 바뀐다.**
- 한국어: Leading -> 왼쪽, Trailing -> 오른쪽
- 아랍어: Leading -> 오른쪽, Trailing -> 왼쪽

위에서 말한 Leading, Trailing을 더 많이 사용하는 이유는 아래와 같다.
- **다국어 지원**을 고려한 레이아웃을 설계할 수 있음
- 애플도 Auto Layout에서 Left/Right는 가능한 사용하지 말고, **Leading/Trailing을 사용하길 권장함**

즉, 특별한 경우를 제외하고는 Auto Layout에서는 **Leading과 Trailing을 표준으로 사용하는것이 좋다.**




