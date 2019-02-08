# HTTP 프로토콜

## HTTP란 무엇인가?

- HTTP란 ***Hyper Text Transfer Protocal***의 약자로 하이퍼텍스트 문서를 교환하기 위한 프로토콜입니다.

- **TCP/IP 기반**으로 한 지점에서 다른 지점으로 요청과 응답을 전송합니다.

  - 한 지점에서 다른 지점으로 HTTP 프로토콜에 맞춘 **문자열**을 전송합니다.

  - ex)

    ```http
    GET  HTTP/1.1
    Host: www.naver.com
    cache-control: no-cache
    
    ```

- HTTP는 많은 정보들이 필요하지만 보통 우리가 웹 프레임워크나 라이브러리들이 HTTP 프로토콜 쉽게 사용할 수 있도록 지원하기 때문에 손쉽게 사용할 수 있는 것입니다.



## HTTP의 특징

- TCP/IP를 이용하는 **응용 계층** 프로토콜.
  - TCP/IP의 **socket**을 이용해 연결된다.
- 연결 상태를 유지하지 않는 **비연결성(Connectionless) 프로토콜**
  - 요청을 받은 서버가 응답하게 되면 소켓을 유지하지 않고 연결을 disconnect한다.
  - 연결을 유지하게 되면 리소스가 계속 사용되고 리소스가 부족하면 다른 사용자가 이용하지 못하기 때문에 결과적으로 더 많은 연결을 위해 비연결 지향으로 설계
  - HTTP 1.1 부터는 *keep-alive* 헤더를 통해 연결을 유지할 수 있음.
- **Stateless**하다.
  - 클라이언트가 사용자 인증을 하더라도 상태가 유지되지 않기 때문에 Cookie(쿠키) 혹은 Session(세션)을 이용해 인증 등을 해결하기도 한다.



## HTTP 메세지

### 메세지 타입

- **요청(Request)**
  - 사용자가 서버에게 원하는 데이터를 요구할 때 사용
- **응답(Response)**
  - 서버가 요청받은 대로 사용자에게 데이터를 줄 때 사용



### 메세지 구조

- **시작줄 / 헤더 / 바디** 로 나눌 수 있다.

  - **시작줄**
    - Request 시, 메서드와 요청 URL, HTTP version ( GET /exam/help.txt HTTP/1.1 )
    - Response 시, HTTP version, 상태 코드 및 사유 구절 ( HTTP/1.1 200 OK )
  - **헤더** 
    - 요청과 응답 메세지에 대한 추가적인 정보를 담고 있다.
    - Key/Value 형식으로 나타냄
  - **바디**
    - 전송하고 싶은 실질적인 데이터를 나타냄
    - 헤더를 마치고 \n 후에 나타남.

- **요청** 메세지 구조 예제

  ```http
  GET /hello.txt HTTP/1.1 		// 시작줄
  User-Agent: curl/7.16.3 libcurl/7.16.3 OpenSSL/0.9.7l zlib/1.2.3	// 헤더
  Host: www.example.com												// 헤더
  Accept-Language: en, mi												// 헤더
  
  
  ```

- **응답** 메세지 구조 예제

  ```http
  HTTP/1.1 200 OK
  Date: Mon, 27 Jul 2009 12:28:53 GMT
  Server: Apache
  Last-Modified: Wed, 22 Jul 2009 19:15:56 GMT
  ETag: "34aa387-d-1568eb00"
  Accept-Ranges: bytes
  Content-Length: 51
  Vary: Accept-Encoding
  Content-Type: text/plain
  
  Hello World! My payload includes a trailing CRLF.	// 바디
  ```



## HTTP 1.1 vs HTTP 2.0

- 처리 방식
  - HTTP 1은 앞에 날렸던 요청의 응답을 받아야만 다음 요청이 처리될 수 있었다. (1 요청당 1 리소스)
    - 따라서 HOL(Head of Line) 블로킹 문제가 발생했다.
  - HTTP 2에서는 Multiplexing 방식이 도입되어 동시에 여러 리소스를 받아올 수 있게 되었다.
- 데이터
  - 기존 HTTP 1은 문자열로 전송되었다.
  - HTTP 2는 바이너리로 인코딩하여 압축해서 전송한다.
    - 헤더 또한 압축할 수 있다.
- Server Push
  - 브라우저에서 필요한 리소스들을 서버가 찾아서 내려준다.
  - 따라서 HTTP 1에서 html을 파싱하고 필요한 리소스를 찾아 요청할 필요 없이 HTTP 2에서는 필요한 리소스를 찾는 과정 없이 요청할 수 있다.



자세한 내용은 다음 링크에 아주 자세히 설명되어있음. [[HTTP] HTTP 2의 탄생 배경과 특징](https://americanopeople.tistory.com/115)



참고: 

- https://feco.tistory.com/7
- https://www.zerocho.com/category/HTTP/post/5b344f3af94472001b17f2da
- https://americanopeople.tistory.com/115



