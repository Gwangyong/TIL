백준 문제를 풀다보면, 프로그램 종료 지점을 정하지 않은채로 무한 입력을 받고 EOF를 기점으로 종료되는 경우가 있다.

아래의 예시는 [백준 10951번 문제](https://www.acmicpc.net/problem/10951)의 예시이다.

while문에서 true등의 조건으로 무한반복하지 말고 while문에서 아래와같이 조건을 달아서 해주어야한다.

```swift
while let input = readLine() {
    let nums = input.split(separator: " ").map { Int($0)! }
    print(nums[0] + nums[1])
}
```

위와같이 while에 조건문을 걸면 EOF를 받을 때, readLine()자체가 nil이 아니면 true, nil이면 false가 되며 종료된다.

또한, Control + D를 누르면 EOF가 send되어서 종료된다.