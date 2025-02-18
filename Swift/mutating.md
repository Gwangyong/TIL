## mutating

구조체는 값 타입이며, 구조체의 메소드는 구조체 내부에서 프로퍼티들의 값을 수정할 수 없게 되어있다. 하지만, **mutating 키워드를 사용하면 구조체 내부에서도 프로퍼티들의 데이터를 수정할 수 있게된다.**

<br>

## 코드로 이해

```swift
struct CollegeStudent {
    let name: String
    var age: Int
    let studentId: Int

    init(name: String, age: Int, studentId: Int) {
        self.name = name
        self.age = age
        self.studentId = studentId
    }
    
    func mutating chageAge() {
        age = 23
    }
}
```

위의 코드는 언뜻 보기에는 문제가 없어 보이지만, 아래의 사진처럼 **오류**가 나는것을 볼 수 있다.

![스크린샷 2022-03-11 오후 3 44 30](https://user-images.githubusercontent.com/59376200/157816439-0037b6be-60bc-4d77-8b63-a2c9298c6539.png)


이유로는 위에서 말한것처럼 **구조체 내부의 프로퍼티 값을 수정할 수 없기 때문**이다. 이번에는 mutating 키워드를 넣어보자.

<br>

![스크린샷 2022-03-11 오후 3 50 01](https://user-images.githubusercontent.com/59376200/157817049-8744cb4f-38d3-4ddb-bb78-c3e4670ca91a.png)

이번에는 오류가 나오지 않는것이 보인다.

그러면 아래의 이미지대로 `Student.chageAge()` 메소드를 호출할 경우에, **age가 20이였던게 23으로 변경**된 것을 볼 수 있다.

![3](https://user-images.githubusercontent.com/59376200/157817267-8b67143b-f66a-40be-88cb-dfb783ed87ed.png)

![4](https://user-images.githubusercontent.com/59376200/157817285-15a75998-3194-4926-b860-d86d890d80dd.png)

