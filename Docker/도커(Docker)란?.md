# 도커란?

도커는 **컨테이너 기반의 오픈소스 가상화 플랫폼**이다.

다들 `컨테이너`라는 말을 들으면, 배에 실어서 전자제품, 신발, 술 등의 화물들을 넣고 이동하는 화물 수송용 컨테이너들을 생각할 것이다. 여기에서 말하는 컨테이너도 비슷하다고 볼 수 있다. 다양한 OS환경과 프로그램들을 컨테이너로 추상화하여 동일한 환경에서 프로그램의 배포 및 관리를 쉽고 빠르게 해결해준다.

<br>

# VMware vs Docker

개인 프로젝트로 하나의 웹 서버를 만든다고 생각해보자. 개인 프로젝트이기 떄문에 모든 버전,환경을 내가 생각해서 정하고 개발한다. 후에 완성을해서 배포를한다고 생각해보자. 내가 만들어서 배포한 웹 서버가 과연 다 똑같은 환경에서 접속을 할까? os는 어떤가 전부 윈도우일까? 맥OS는? 아니면 리눅스?

그렇기에 `Vmware`나 `VirtualBox`등을 이용해서 OS를 다시 설치하고 테스트하고 다시 구축을 한다. 그래도 또 다른 예외와 오류는 있을 것이다. 배포가 처음부터 완벽하긴 힘들다. 또한, 이렇게 `VMware`나 `VirtualBox`에 OS를 또 설치하면 **OS위에 OS를 올리는것이 되어버려 더욱 무거워지고 속도도 느려질 것이다.** 그렇기에 사용하는 것이 바로 `Docker`인 것이다.

도커에서는 하나의 컴퓨터 안에서 각각의 격리된 환경에서 앱을 실행시킨다. 이때, 운영체제가 설치된 컴퓨터를 주인이라는 뜻으로 `host`라고 부르며, 격리된 각각의 실행환경을 `container`이라고 부른다.

각각의 컨테이너에는 운영체제 전체가 아닌, 앱을 실행하는데 사용되는 `실행 파일`과 `라이브러리`만이 들어가있다. 이러한 방식으로 **운영체제도 1개라서 더욱 빠르며 가볍고 다시 설정해줄 필요도 없으며, 이미 존재하는 운영체제를 공유하는 것이므로 무언가를 또 설치할 필요성도 없게된다.**
