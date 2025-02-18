# 타입 캐스팅이란?

타입 캐스팅이란, 인스턴스의 타입을 확인하거나 어떠한 클래스의 인스턴스를 해당 클래스 계층 구조의 슈퍼 클래스나 서브 클래스로 취급 하는 방법이다.

"is"와 "as"라는 연산자를 사용하여, 값의 타입을 확인하거나 값을 다른 타입으로 변환하는데 사용함.

<br>

# 타입 확인(Checking Type)
타입 확인은 "is" 키워드를 사용해서 특정 클래스의 인스턴스의 타입을 확인할 수 있다.

Swift Language Guide에 있는 예제를 살펴보자.

```swift
class MediaItem {
    var name: String
    init(name: String) {
        self.name = name
    }
}
```
우선 String 형식의 name 프로퍼티와 생성자를 하나 가지는 `MediaItem` 이라는 클래스를 선언해준다.

```swift
class Movie: MediaItem {
    var director: String
    init(name: String, director: String) {
        self.director = director
        super.init(name: name)
    }
}

class Song: MediaItem {
    var artist: String
    init(name: String, artist: String) {
        self.artist = artist
        super.init(name: name)
    }
}
```
<br>

`MediaItem` 클래스를 상속받는 서브 클래스인 `Movie`와 `Song` 두 개의 클래스를 선언해준다.


```swift
let library = [
    Movie(name: "기생충", director: "봉준호"),
    Song(name: "Six Feet Under", artist: "Billie Eilish"),
    Movie(name: "올드보이", director: "박찬욱"),
    Song(name: "Closure", artist: "Faime"),
    Song(name: "If I Die Young", artist: "The Band Perry")
]
```
그리고 위의 코드와 같이 배열을 하나 만들어준다. 이 안에 처음 정의해준 `MediaItem` 클래스의 상속을 받는 `Movie`와 `Song` 타입 인스턴스를 넣어준다.
그러면 `library`배열은 타입 추론에 의해 `[MediaItem]` 배열의 형태를 가지게 된다.

<br>

이제 "is" 연산자를 사용한 `타입 확인(Checking Type)`을 사용해보자.

아래 코드는 `library` 배열을 순회하여 `item`이 특정 타입일 때마다 그에 맞는 숫자를 증가시키는 코드이다. 

```swift
var movieCount = 0
var songCount = 0

for item in library {
    if item is Movie {
        movieCount += 1
    } else if item is Song {
        songCount += 1
    }
}

print("Media library에는 \(movieCount)개의 영화와 \(songCount)개의 노래가 있다.")
// Media library에는 2개의 영화와 3개의 노래가 있다.
```

`library`배열에서 정의해준 `Movie`는 2개이며, `Song`은 3개이므로, `movieCount`에는 2가 더해지고, `songCount`에는 3이 더해져서 **Media library에는 2개의 영화와 3개의 노래가 있다.** 라는 출력이 나오게된다.

<br>

# 다운캐스팅(Downcasting)

다운 캐스팅은 `부모 클래스`에서 `자식 클래스`로 `형 변환` 하는것을 의미한다. 쉽게 말하자면 **업캐스팅된 인스턴스를 다시 원래의 서브 클래스 타입으로 참조하고자 할때 사용한다.**

표현식의 타입이 변환할 Type과 호환된다면, 변환할 Type으로 캐스팅된 인스턴스를 리턴함.
상속 관계인 업캐스팅(Upcasting)와 다운 캐스틍(Downcasting)에서 사용되는데, Any와 AnyObject 타입을 사용하는 경우, 상속 관계가 아니라도 사용이 가능하다.

다운캐스팅은 **실패할 수 있기 때문에, "as?"와 "as!" 연산자를 이용한다.**

Optional 조건부 형식 `as?`는 다운캐스트를 시도하여 타입의 옵셔널 값을 반환하며, 강제 형식인 `as!`를 사용하면 강제 언래핑(Forced-Unwrap)을 하여 강제로 값을 반환하게 된다.

Optional Binding에서 `!`를 사용하면 값이 없는 경우에도 값을 가져오려다가 런타임 에러가 발생하므로, 가능하면 사용하지 말고 값이 확실히 있을때만 사용하라고 주의했었다. 그러므로 다운캐스팅도 마찬가지로 **확실히 성공한다는 확신이 있을때만 `!`를 사용하자.**

<br>

```swift
for item in library {
    if let movie = item as? Movie {
        print("Movie: \(movie.name), dir. \(movie.director)")
    } else if let song = item as? Song {
        print("Song: \(song.name), by \(song.artist)")
    }
}

// Movie: 기생충, dir. 봉준호
// Song: Six Feet Under, by Billie Eilish
// Movie: 올드보이, dir. 박찬욱
// Song: Closure, by Faime
// Song: If I Die Young, by The Band Perry
```

위의 예제를 보면 if let을 사용하였으며 `as?`로 조건부 형식을 사용하였다.

`library`는 `MediaItem`타입 배열이며, `as?` 조건부 형식 뒤에 있는 `Movie`와 `Song` 모두 `MediaItem`의 서브클래스이기 때문에, 차례대로 Movie와 Song의 이름과 감독/아티스트 이름을 출력하게 된다.


<br>


# Any, AnyObject

Swift는 두 가지 특별한 타입을 제공한다. 바로 `Any`와 `AnyObject`이다.

- `Any`는 함수 타입을 포함해 `모든 타입의 인스턴스`를 나타낸다.
- `AnyObject`는 `모든 클래스 타입`의 인스턴스를 나타낸다.


`things`라는 `Any`타입의 배열을 선언하여 아래와 같이 여러 타입의 값을 저장한다. `Int`, `String`, 함수, 클로저 등 여러가지 타입이 가능하다.
```swift
var things: [Any] = []

things.append(0)
things.append(0.0)
things.append("Jud")
things.append({ (name: String) -> String in "Hello, \(name)" })
things.append(Movie(name: "Black Widow", director: "Cate Shortland"))
```

<br>

하지만 아래의 코드와 같이 `Any` 타입에서 `AnyObject`타입으로 변경해주면 **클래스 타입인 Movie를 제외하고는 모두 에러가 뜬다.**
```swift
var things: [AnyObject] = []

things.append(0)
things.append(0.0)
things.append("Jud")
things.append({ (name: String) -> String in "Hello, \(name)" })
things.append(Movie(name: "Black Widow", director: "Cate Shortland"))
```

그 이유로는 `AnyObject`는 위에서 설명했듯이, 모든 `클래스 타입`의 인스턴스만을 저장할 수 있다. 따라서 위의 코드와 같은 경우, **클래스 타입이 아니기 때문에** 오류가 나는 것이다.

<br>

## as?, as!를 이용한 다운캐스팅(Downcasting)

Any와 AnyObject가 모든 타입을 지정해주어서 매우 편해보일 것이다. 하지만, 예시를 하나 들어서 단점을 보자.

```swift
var name: Any = "Jud
```
위의 코드를 보면, 누가봐도 name의 타입은 String 타입일 것이다. 하지만, `name.`을 해서 자동완성을 하려해도 값이 나오지 않으며, `name.append("Jud2")`를 작성해도 에러가 날 것이다.

이유는, **Any, AnyObject 타입은 런타임 시점에서 타입이 결정**되기 때문에, 컴파일 시점에서 해당 타입에 대해 알 수가 없다.

그래서, Any타입인 name을 String으로 사용하고 싶다면,
```swift
if var name = name as? String {
    name.append("Jud2")
}
```
이런식으로 다운 캐스팅을 해주어야한다.

<br>
<br>

> Reference
> - [The Swift Language Guide - Type Casting](https://docs.swift.org/swift-book/LanguageGuide/TypeCasting.html)
> - [Any와 AnyObject 알아보기](https://babbab2.tistory.com/128?category=828998)

