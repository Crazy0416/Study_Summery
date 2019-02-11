# REST API란?

## REST란?

- **Re**presentational **S**tate **T**ransfer의 준말이다.
  - **Representation (표현)**: Resources(이미지, 페이지, 비디오, 프로필)는 HTML, 이미지, JSON, XML 등과 같은 어떤 형식(format)으로든 웹 서버에 의해 클라이언트에게 표현된다.
    - Resources는 데이터베이스의 데이터나 웹서버의 물리적인 정보를 의미한다.
    - 리소스를 사람이 읽을 수 있거나 프로그래밍할 수 있도록 정형화된 형식으로 transfer하여 클라이언트에게 전달.
  - **State (상태)**: 클라이언트 컴퓨터의 어플리케이션(웹 사이트) 상태가 한 링크에서 다른 링크로 클릭할 때 변경된다.
  - **Transfer(전이)**: Representational state (표현 상태)의 Resources(자원)을 웹 서버에서 클라이언트로 전송하는 것을 의미 
- **REST**란 '**소프트웨어 아키텍쳐 모델**'이다. 자원을 정의하고 자원에 대한 주소를 지정하는 방법에 대한 방법론이다.



## REST의 제한 조건(혹은 특징)

다음 자료를 참조: [REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)

1. **Uniform (유니폼 인터페이스)**
   - URI로 지정한 리소스에 대한 조작을 **통일되고 한정적인 인터페이스로 수행**하는 아키텍처 스타일을 말합니다.
2. **Stateless (무상태성)**
   - 작업을 위한 상태 정보를 저장하거나 관리하지 않는다. 따라서 쿠키 정보나 세션 정보를 별도로 저장하지 않기 때문에 들어오는 요청만을 단순히 처리하기만 하면 된다.
3. **Cacheable (캐시 가능)**
   - REST는 HTTP 웹 표준을 그대로 따르기 때문에 웹에서 사용하는 기존 인프라를 그대로 사용 가능.
4. **Client-Server (클라이언트-서버 구조)**
   - 클라이언트와 서버 구조로 일관적인 분리가 되어야 한다. 그러면 클라이언트와 서버가 개발해야될 내용이 명확해지고 서로간의 의존성이 줄어든다.
5. **Layerd System (계층형 구조)**
   - REST 서버는 다중 계층으로 구성될 수 있다. (프록시 서버나 로드 밸런서 등이 중간 계층에 존재할 수 있다.)
6. **Code on Demand** -optional
   - 기능 확장을 위해 코드를 전송하여 실행할 수 있다.



## REST API란?

### 용어 설명

- **REST** **A**pplication **P**rogramming **I**nterface의 준말이다.
- API는 "응용 프로그램에서 사용할 수 있도록 다른 시스템이 제공하는 기능을 제어할 수 있게 만든 인터페이스"를 의미한다.
- 따라서 REST API는 REST 시스템의 기능을 이용할 수 있도록 인터페이스를 제공하는 것을 말한다.
- REST API를 만드는 방법은 명확한 기준은 없고 비공식적으로 의견들이 수렴되어 만들어졌다.



## REST API 한문장 요약

REST API를 한 문장으로 요약하자면 

> 정보의 Resources를 HTTP URI로 표현하며 Resources에 대한 기능을 Method로 표현한다. 인터페이스들은 일관된 형태로 나타나야 하며 이 URI를 통해 에플리케이션의 상태를 전이한다.

라고 표현할 수 있을 것 같다.



## 마무리

REST에 대한 정의와 REST API의 정의가 명확하지 않은 것 같아서 정리 차원에서 포스트를 작성했다. RESTful API의 디자인 가이드는 실력이 필자의 실력이 미천하기 때문에 다른 사람들의 정보들을 얻는 것이 좋을 것 같다.



참고: 

- https://ko.wikipedia.org/wiki/REST
- https://www.youtube.com/watch?v=LooL6_chvN4
- https://meetup.toast.com/posts/92

