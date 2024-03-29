# 스택(Stack)의 개념

![LIFO(Last In First Out)](https://user-images.githubusercontent.com/59376200/127250787-bc69ec8e-573e-4f9c-91ee-39409598da00.png)


`스택(Stack)`은 '쌓다' 라는 의미로, 데이터를 차곡차곡 쌓아 올린 형태의 자료구조이다.
간단한 예시로는 책상에 책을 쌓아두는걸 예시로 들 수 있을 것이다.

스택은 사진과 같이 정해진 방향으로만 쌓을 수 있으며, `top`으로 정한 곳을 통해서만 접근할 수 있다.

top의 가장 위에있는 자료는 가장 최근에 들어온 자료이며, 새로 삽입되는 자료는 top이 가리키는 가장 맨 위에 쌓이게 된다.

자료를 삭제할 때도 top을 통해서 삭제가 가능하다.

스택에서는 삽입 연산을 `push`, 삭제 연산을 `pop`이라고 부르며, 둘 다 top을 통해 사용된다.

스택의 이러한 구조는, 데이터가 순서대로 쌓이며 가장 마지막에 삽입된 자료가 가장 먼저 삭제되는 구조를 가지고 있다.

이러한 스택의 구조를 `후입선출(Last In First Out)`의 구조라고 부르며, 줄여서 `LIFO` 구조라고 부른다. 


<br>

## 스택(Stack)의 사용 사례
- 웹 브라우저 방문기록 (뒤로가기)
- 실행 취소(undo)
- 역순 문자열 만들기
- 후위 표기법 계산

<br>

## Stack Code

**Stack 기본 형태. (pop 메소드 부분 제외하면 동일)**

- popLast() 라는 메소드 함수 자체를 Swift 배열에서 지원해줌. 그렇기에 굳이 배열을 Stack 처럼 쓰면되지, Stack은 굳이 안만들어도 괜찮은 것 같다.

```swift
struct Stack<T> {
    private var stack: [T] = []
    
    public var count: Int {
        return stack.count
    }
    
    public var isEmpty: Bool {
        return stack.isEmpty
    }
    
    public mutating func push(_ element: T) {
        return stack.append(element)
    }
    
    public mutating func pop() -> T? {
        return isEmpty ? nil : stack.popLast()
    }
}

var myStack = Stack<Int>()
myStack.push(10)
myStack.push(3)
myStack.push(13)
print(myStack) // Stack<Int>(stack: [10, 3, 13])
myStack.pop()
print(myStack) // Stack<Int>(stack: [10, 3])
```

---

<br>

# 큐(Queue)의 개념
![FIFO(First In First Out)](https://user-images.githubusercontent.com/59376200/127253000-528edd13-59d3-4cd5-a7c9-8529cc9dae34.png)

`큐(Queue)`는 스택과 비슷하지만 다른 자료구조이다. Swift 에서는 Queue를 따로 지원하지 않는다. (시스템적인 DispatchQueue 이런건 제외..)

큐는 스택과 다르게, `FIFO(First In First Out)`의 구조를 가진다.

먼저 들어온 것이 먼저 나간다는 뜻으로, 카페에서 먼저 온사람이 음료를 먼저 받고 나가는 것을 예시로 들면 이해가 될 것이다.

**삭제 연산이 수행되는 곳을 `프론트(front)`, 삽입 연산이 이루어지는 곳은 `리어(rear)`** 로, FIFO 구조를 위해서 스택과 다르게 큐의 한쪽 끝에는 삽입 작업이, 다른 한쪽 끝에서는 삭제 작업이 나뉘어져서 이루어진다.

큐는 `리어(rear)`에서 이루어지는 삽입 연산을 `인큐(Enqueue)`라고 부르며, `프론트(Front)`에서 이루어지는 삭제 연산을 `디큐(Dequeue)`라고 부른다.

<br>

## 큐(Queue)의 사용 사례

큐는 순서대로 작업을 수행할때 활용할 수 있다.
- 은행 업무
- 대기열 순서와 같은 우선 순위의 작업 예약 등
- 서비스 센터의 대기시간
- 프로세스 관리

<br>

## Queue Code

```swift
struct Queue<T> {
    private var queue: [T] = []

    public var count: Int {
        return queue.count
    }

    public var isEmpty: Bool {
        return queue.isEmpty
    }

    public mutating func enqueue(_ element: T) {
        queue.append(element)
    }

    public mutating func dequeue() -> T? {
        return isEmpty ? nil : queue.removeFirst()
    }
}

var myQueue = Queue<Int>()
myQueue.enqueue(10)
myQueue.enqueue(8)
print(myQueue) // Queue<Int>(queue: [10, 8])
myQueue.dequeue()
print(myQueue) // Queue<Int>(queue: [8])
```

위의 코드는 Stack 코드의 pop 부분을 제외하고는 동일하다.

하지만 여기서는 dequeue를 할 경우, 처음 값이 빠지기 때문에 비어버린 공간에 자리를 한 칸씩 당겨야하기 때문에 **O(1)이 아닌, O(n)의 시간 복잡도가 필요**하게된다.

그래서 아래의 코드를 통하여 그걸 방지해줄 수 있다. **dequeue를 하면 head가 값을 가지고있다가, 어느정도 조건에 채워지면 비워주는 것이다.**

```swift
struct Queue<T> {
    private var queue: [T?] = []
    private var head: Int = 0

    public var count: Int {
        return queue.count
    }

    public var isEmpty: Bool {
        return queue.isEmpty
    }

    public mutating func enqueue(_ element: T) {
        queue.append(element)
    }

    public mutating func dequeue() -> T? {
        guard head <= queue.count, let element = queue[head] else { return nil }  // element : 10
        queue[head] = nil
        head += 1

        if head > 30 {
            queue.removeFirst(head)
            head = 0
        }
        return element
    }
}

var myQueue = Queue<Int>()
myQueue.enqueue(10)
myQueue.enqueue(8)
print(myQueue)
myQueue.dequeue()
print(myQueue)
```

<br>


[Stack 코드 출처](https://babbab2.tistory.com/85?category=908011)
[Queue 코드 출처](https://babbab2.tistory.com/84?category=908011)
