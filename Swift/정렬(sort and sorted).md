[이 내용을 정리한 개인 기술 블로그](https://jud00.tistory.com/entry/%EC%98%A4%EB%8A%98%EC%9D%98-Swift-%EC%A7%80%EC%8B%9D-%EC%A0%95%EB%A0%AC-sort%EC%99%80-sorted)

# sort

`sort`는 기본적으로 **"원본 배열"** 을 가지고 **오름차순**으로 정렬한다.<br>
**내림차순**으로 정렬하고 싶다면, `sort(by: )` 함수를 사용해서 `sort(by: >)`로 작성해주면 된다.

물론 오름차순으로 정렬하는 방법도 있다. `sort(by: <)`이다. 하지만 그냥 sort만 사용해도 오름차순이니 사용할 일은 없을 것 이다.

아래의 예시 코드를 보자.
```swift
var arr = [2, 24, 45, 36, 9]

// 기본 오름차순 정렬
arr.sort()
print(arr) // [2, 9, 24, 36, 45]

// 내림차순 정렬
arr.sort(by: >)
print(arr) // [45, 36, 24, 9, 2]
```

<br>

# sorted
`sorted`는 `sort`와 다르게 원본 배열은 건드리지 않고, **"사본"** 을 만들어서 오름차순으로 정렬한 후 정렬된 요소를 반환한다.<br>
sorted 또한 **내림차순**으로 정렬하고 싶다면 `sorted(by: )` 함수를 사용해서 `sorted(by: >)`로 작성해주면 된다.

물론 sort와 동일하게 기본 정렬은 `sorted(by: <)` 이지만, sort와 동일한 이유로 사용할 일은 없을 것 이다.

이번에도 예시 코드를 보자.
```swift
var arr = [2, 24, 45, 36, 9]

// 기본 오름차순 정렬
var sortedArr = arr.sorted()
print(arr)  // [2, 24, 45, 36, 9]
print(sortedArr)  // [2, 9, 24, 36, 45]

// 내림차순 정렬
var sortedArrDown = arr.sorted(by: >)
print(sortedArrDown) //[45, 36, 24, 9, 2]
```

<br>

## sort & sorted 주의할 점
위에서 말했듯이, `sort`는 원본 "배열 자체의 순서를 변경"하기 때문에 기존의 배열 순서가 중요한 경우, `sort`를 사용하면 문제가 발생할 것이다.

또한 `sorted`는 값을 복제하여 사용하는 만큼 "메모리의 사용량이 2배"가된다. 그러므로 큰 사이즈의 배열에 사용하면 메모리가 많이 사용되므로 주의해야한다.

<br>

## Other types
위의 예시 코드에서는 전부 `정수(Int)`를 예시로 들었지만, 정수에만 적용되는 것이 아니라 `Double`, `String`등의 타입에서도 적용된다.<br>
예상이 가겠지만, String형에서는 한글은 '가나다'순서 영어는 'abc'순서로 정렬이 된다.