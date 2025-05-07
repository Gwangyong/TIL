# 아키텍처를 사용하는 이유

앱을 개발할 때 아키텍처를 설계하는 이유는 코드의 가독성, 유지보수성, 그리고 향후 기능 확정을 쉽게 만들기 위해서이다. iOS에서는 대표적으로 MVC(Model-View-Controller)와 MVVM(Model-View-ViewModel) 두 가지 패턴이 많이 사용된다.


<br>


# MVC(Model-View-Controller) 

> MVC는 오랫동안 사용되어 온 아키텍처 패턴으로, 앱의 구조를 모델(Model), 뷰(View), 컨트롤러(Controller)의 세 개의 역할로 분리한 것이다.

## MVC 패턴 구조
- Model : 데이터 및 비즈니스 로직을 담당
- View : 사용자에게 보여지는 UI 요소
- Controller : 사용자의 입력(Action)을 받고 처리하는 부분 (Model과 View의 중개자 역할)


## MVC 패턴 동작
1. 사용자가 UI에서 동작을 수행하면
2. Controller가 그 요청을 받아 Model에 전달하고
3. Model이 처리한 결과를 Controller를 통해 View에 전달하여
4. View가 업데이트된다.

## MVC 패턴의 장/단점

- 장점
    - 직관적이고 간단한 구조
    - iOS에서 기본적으로 권장하는 패턴
    - 소규모 프로젝트에 적합
    - 많은 개발자들에게 친숙한 패턴이기 때문에 개발자들이 쉽게 유지보수 가능

- 단점
    - 코드 재사용성이 떨어지고, 유닛 테스트를 진행하기 어렵다.
    - 대부분의 코드가 Controller에 밀집되어 크기가 비대해지고 구조가 복잡해진다. (Massive View Controller 문제)
    - 프로젝트의 규모가 커질수록 유지보수가 힘들어진다.



<br>



# MVVM(Model-View-ViewModel)

> MVVM은 MVC의 복잡한 Controller 문제를 개선하기 위해 나온 구조로, View와 Model 사이에 ViewModel을 두어 UI 관련 로직을 분리한다.

## MVVM 패턴 구조
- Model : 데이터 및 비즈니스 로직을 담당
- View : 사용자에게 보여지는 UI요소
- ViewModel : UI와 모델을 연결하는 중간 계층, 비즈니스 로직과 UI 로직을 처리

## MVVM 패턴 동작
1. 사용자가 UI에서 동작을 수행하면  
2. View는 ViewModel에 데이터를 요청하고  
3. ViewModel은 Model에 요청을 전달해 데이터를 처리하고  
4. 처리된 데이터를 다시 View에 전달해 UI를 자동으로 갱신한다.

## MVVM 패턴의 장/단점
- 장점
    - 코드 재사용성이 높음
    - UI 로직을 ViewModel에서 처리하여 컨트롤러가 가벼워짐
    - 테스트하기 쉬움 (ViewModel을 단위 테스트 가능)

- 단점
    - UIKit에서는 데이터 바인딩이 기본 제공되지 않기 때문에, RxSwift나 Combine 등의 프레임워크가 필요할 수 있음
    - View Model의 설계가 쉽지 않다. (구조가 상대적으로 복잡함)


# MVC vs MVVM 비교

| 비교 항목 | MVC | MVVM |
|--------|--------|--------|
| 구조 | Model-View-Controller | Model-View-ViewModel |
| 컨트롤러 역할 | 크고 복잡해질 수 있음(Massive View Controller) | ViewModel이 UI 로직을 분리하여 컨트롤러가 가벼워짐 |
| 코드 재사용성 | 낮음 | 높음 (ViewModel 재사용 가능) |
| 유지 보수성 | 코드가 많아지면 어려움 | ViewModel을 통한 분리가 되어 유지 보수 용이 |
| 테스트 가능성 | 어렵고 제한적 | 용이(ViewModel 단위 테스트 가능) |


# 언제 어떤걸 선택해야할까?
- 소규모 프로젝트, 빠른 개발이 필요할 때 -> MVC 패턴
- 유지 보수성과 확장성이 중요한 경우 -> MVVM 패턴
- RxSwift와 결합하여 반응형 UI를 구현할 경우 -> MVVM 패턴

<br>

> RxSwift가 뭘까?
> RxSwift는 iOS앱에서 비동기 작업(예: 버튼 클릭, API 호출 등)을 간결하고 직관적으로 처리할 수 있도록 도와주는 라이브러리다.