[이 내용을 정리한 개인 기술 블로그](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-Optional%EC%9D%B4%EB%9E%80-%F0%9F%A4%94)

## Optional이란??

swift언어는 type-safety한 언어입니다. optional은 그 중요한 요소 중 하나이죠. <br>
optional은 `"?"`키워드로 사용되며, 그 의미는 `이 변수에는 값이 들어갈 수도 있고, 아닐 수도 있어` 라는 뜻입니다.

우선 아래의 예시를 봅시다.
```swift
var name: String = "Jack"   // OK
name = nil                  // Error ('nil' cannot be assigned to type 'String')
```

자 우리는 아래와같이 변수에 값을 넣어주고, 그 값에 다시 nil을 할당해주었는데 오류가 났네요... 이유가 뭘까요?

그 이유는 바로 `optional이 아닌데 nil을 할당해주었기 때문`입니다.
기본적으로 swift에서 변수를 선언할 경우에는 optional이 아닌 값(non-optional)을 지정해주어야 합니다.

즉, 변수를 선언할 경우 nil이 아닌 값(non-nil)을 할당해주어야 한다는 뜻이죠
만약, 옵셔널이 아닌 변수에 nil을 설정해주면, 위와 같이 컴파일러는 nil 값을 할당할 수 없다며 오류를 발생시키는 것 입니다.

<br>

> 여기서 잠깐, nil은 무엇일까?
1. swift에서 nil은 optional변수 이외에 사용할 수 없다. 
2. nil은 value가 없는 것 이라는 의미라고 생각하면 된다.
3. nil값은 optional변수에서 따로 초기화하지 않아도 기본 디폴트값이다.

<br>

### 자 그럼 마저 이 오류를 없애보자!
```swift
var name: String? = "Jack"   // OK
name = nil                   // OK
```

String 타입의 뒤에 `"?"`을 붙여주니 오류가 사라졌네요! 이유는 optional의 `"?"`키워드를 사용하여 optional 변수로 만들어주었기 때문입니다.
풀어 얘기하면, 이 변수의 안에는 값이 있을 수도, 없을 수도 있다는 것을 명시해준 것이 되겠네요.

변수에 ?키워드가 붙으면 그 안에 값이 있는지 물어보게되고, 그 안에 값이 있으면 값을 얻게되지만, 아무것도 없으면 nil을 얻게 되는것입니다.

아 `?`를 붙여서 오류가 사라졌지만, 그 위치에 `!`를 넣어주어도 오류가 사라지게됩니다. 이유는 바로 밑에서 설명할게요 :)

<br>

## ! (Forced Unwrapping) 

자 이제 `?`는 optional의 기호라는건 다들 아실겁니다. 하지만 위에서 말했듯이 !를 써도 오류가 사라지는데요. !은 무엇일까요??<br>
!는 강제 언래핑(Forced Unwrapping)이라고 부릅니다. ?와 다르게 친절하게 물어보는 느낌이 아닌, 값이 있든 말든 다 무시하고 강제로(?) 값을 가져온다고 생각하시면 될거같네요

이번에도 코드로 보면서 설명해봅시다.
```swift
var num: Int? = 300
print(num)              // Optional(300)

print(num!)             // 300
```

<br>

위의 코드가 `!`을 쓰고 안쓰고의 차이입니다.<br>
우리가 코드를 작성할때 일반적으로 원하는 값은 `Optional(300)`이 아닌, 그냥 `300`일겁니다.

이럴때 원하는 값인 `300`만 출력하도록 하기 위해 사용하는 것이 `!(exclamation mark)`입니다.<br>
변수명 뒤에 느낌표를 사용해서 optional을 Forced unwrap해주는 것 입니다. optional은 Forced unwrap를 한 상태에서만 위와 같이 제대로된 값만을 출력할 수 있습니다.

즉, 우리가 optional로 `있을 수도 있고, 없을 수도 있다.` 라고 선언했지만, 
`무조건` 변수에 값이 있는게 보장된 경우, `!`를 쓰면 우리가 원하는 값 만을 출력할 수 있게됩니다.

<!-- > 참고 자료 : https://medium.com/@codenamehong/swift-optional-1-54ae4d37ee09 -->