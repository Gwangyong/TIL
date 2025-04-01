## mutating

- 구조체는 값 타입이며, 기본적으로 구조체 내부의 메서드는 자신의 프로퍼티 값을 수정할 수 없다.
- 하지만, mutating 키워드를 사용하면 **구조체 내부에서도 프로퍼티의 값을 수정**할 수 있다.

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
    
    func changeAge() {
        age = 23
    }
}
```

위의 코드를 작성하면 아래의 사진처럼 오류가 나는 것을 볼 수 있다.

![Error](https://github.com/user-attachments/assets/ae99dfa3-3a45-45a5-8d4e-d5c13af0d6b9)


이유는 앞서 말한 것처럼 **구조체 내부의 프로퍼티 값을 수정할 수 없기 때문**이다. 

이 문제를 해결하려면 mutating 키워드를 함수 앞에 붙이면, 프로퍼티 값을 수정할 수 있게 되어 오류가 발생하지 않는다.

<br>

![Error 해결](https://github.com/user-attachments/assets/90e9c9c4-8bde-401f-842f-049550fec12d)



그러면 아래의 이미지대로 `student.changeAge()` 메서드를 호출할 경우에, **age의 값이 20에서 23으로 변경**된 것을 볼 수 있다.

![3](https://github.com/user-attachments/assets/98773172-c24a-40f8-b6d7-c845960a81db)

![4](https://github.com/user-attachments/assets/608d318c-a2ba-40ea-991f-5047c8684d1f)

