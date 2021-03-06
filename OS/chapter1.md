# 소개

## 목차



## 운영체제 시스템이란?

- **하드웨어**와 **응용 프로그램** 사이의 **중개인 역할**을 하는 소프트웨어
- 운영체제의 **목표**
  - 사용자에게 컴퓨터에서 프로그램을 효율적이고 편리하게 실행할 수 있는 환경을 제공
  - 컴퓨터 자원의 할당. 이 할당은 공정해야 하며 효율적으로 이루어져야 함.
  - 제어 프로그램으로 사용자 프로그램의 실행을 감독하여 오류와 컴퓨터 오용을 방지하고 입출력 장치의 제어와 동작을 관리한다.



## 컴퓨터 시스템의 구조

### 컴퓨터 시스템의 동작

- ![컴퓨터 시스템 구조](https://raw.githubusercontent.com/Crazy0416/Study_Summery/master/OS/resource/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-11-01%20%EC%98%A4%ED%9B%84%201.21.43.png)
- 현대의 범용 컴퓨터는 공유된 주기억장치에 접근을 제공하는 공통 버스에 의해 연결된 CPU와 여러 개의 장치 제어기(device controller)로 구성되어 있다.
  - 장치 제어기: 각 장치(디스크, 오디오 장치, 비디오 디스플레이)를 관리한다.
- 컴퓨터가 처음으로 구동되면 초기에 실행될 프로그램이 필요하다. 이를 **부트스트랩(bootstrap)**이라고 한다. 이 프로그램은 보통 컴퓨터 하드웨어(ROM) 내에 저장되어 있다.
  - 부트스트랩은 모든 하드웨어를 초기화하고 운영체제 커널을 주기억 장치에 적재한 후 커널을 실행한다.
- 컴퓨터에서 사건의 발생은 **인터럽트(Interrupt)** 신호 또는 **트랩(Trap)**을 통해 운영체제로 통보된다.
  - **인터럽트**: 하드웨어 장치가 CPU의 인터럽트 라인을 세팅
  - **트랩**: 소프트웨어 인터럽트라고도 하며 소프트웨어가 CPU의 인터럽트 라인을 세팅. 대표적인 예로 시스템 콜(System call), 예외 상황(Exception)이 있다. 

### 인터럽트

1. **인터럽트의 일반적 기능**
   - 인터럽트가 발생하면 CPU는 하던 일을 멈추고 인터럽트를 처리하기 위한 루틴(운영 체제 커널 내부 코드)에 들어가서 정의된 일을 찾게 된다. 운영 체제는 할 일을 쉽게 찾아가기 위해 인터럽트 벡터(interrupt vector)를 가지고 있다. 인터럽트 벡터란 인터럽트 종류마다 번호를 정해서, 번호에 따라 처리해야 할 코드가 위치한 부분을 포인터로 가리키고 있는 자료 구조이다.
   - 인터럽트 서비스 루틴을 통해 해당하는 인터럽트를 처리하고 나면 원래 수행하던 작업으로 돌아가 정지되었던 일을 계속해서 수행한다. 인터럽트 처리 후 되돌아갈 위치를 알아야 하므로 인터럽트 처리 전에 수행 중이던 작업이 무엇이었는지 반드시 저장해 두어야 한다.
2. **인터럽트 처리 루틴**
   1. 장치가 인터럽트 신호를 보냄
   2. CPU는 현재 작업 중이던 명령을 멈춘 뒤 커널 모드로 바뀐 후 현재 PC(Program counter)와 다른 상태를 커널 스택에 저장한다.
   3. CPU는 벡터 테이블에서 인터럽트 벡터를 fetch한 뒤 그 주소로 분기한다.
   4. 인터럽트 루틴은 장치 데이터베이스를 검사하고 인터럽트가 요구한 명령을 수행합니다.
   5. 인터럽트 핸들러가 명령을 완료하고 이전 상태를 복구하고 유저 모드로 복귀합니다. (혹은 스케줄러에게 다른 프로그램으로 전환하도록 요청)

### I/O 구조

- 장치 제어기에 따라 하나 이상의 장치가 제어기에 연결될 수 있다.
- 장치 제어기는 로컬 버퍼와 몇가지 특수 레지스터를 유지한다.
- 장치 제어기는 연결된 주변장치와 로컬 버퍼간의 데이터 이동을 책임진다. 버퍼 크기는 주변 장치에 따라 다르다. 

1. **I/O 인터럽트**

   - I/O를 시작하기 위해 CPU는 장치 제어기 내에 있는 레지스터에 적절한 데이터를 적재한다. 제어기는 이것을 검사하여 어떤 행동을 취할지 결정한다. 입출력의 수행이 끝나면 보통 인터럽트를 통해 CPU에 그 사실을 통보한다.

   - **입출력의 두 가지 형태**
     - 동기식 입출력(Synchronous I/O): 입출력이 시작되면 요청한 **프로세서**는 입출력이 완료될 때까지 기다린다.
     - 비동기식 입출력(Asynchronous I/O): 요청한 **프로세서**는 입출력이 완료될 때까지 기다리지 않고 계속 다른 작업을 수행한다.

2. **I/O 방식**

   - 직접 I/O 방식: 주기억 장치와 장치 제어기 간의 데이터 전송을 CPU가 직접 책임지는 방식(ex. 폴링 방식)
   - **간접 I/O 방식**: CPU가 직접 입출력을 담당하지 않고 **인터럽트**를 사용하여 전용 입출력 프로세서인 **DMA**나 채널을 이용하는 방식

3. **DMA 구조**

   - 장치 제어기는 데이터 블록을 CPU의 관여 없이 직접 주기억 장치로 이동하며, 인터럽트는 바이트 단위가 아닌 블록 단위로 발생한다.
   - 입출력 명령을 만나면 CPU는 DMA에게 입출력 명령을 내린 후 다른 프로그램을 수행.
   - DMA는 자동으로 입출력 처리하고 완료시 CPU에게 인터럽트로 완료 사실을 보고.

### 저장 장치의 구조

- 주기억 장치와 보조기억 장치로 구분
- 주기억 장치 용도
  - 프로그램 실행 용도
- 보조기억 장치:
  - 파일 시스템
  - 메모리 연장 공간인 스왑용

1. 저장 장치의 계층 구조
   - ![저장 장치의 계층 구조](https://raw.githubusercontent.com/Crazy0416/Study_Summery/master/OS/resource/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202018-11-03%20%EC%98%A4%ED%9B%84%204.22.58.png){:width="50%"}
2. 캐싱
   - CPU가 데이터를 필요하면 먼저 캐시에 그 데이터가 있는 지 검사한다. 만약 있으면 캐시에서 바로 사용하고 없으면 메인 메모리에 있는 데이터를 사용하지만 이 데이터의 복사본을 캐시에 보관한다. 이것은 이 데이터를 곧 또 다시 사용할 확률이 높기 때문이다. 



### 하드웨어 보호

- 다중 프로그래밍 환경에서는 하나의 프로세스의 오류가 다른 프로세스에게도 영향을 줄 수 있다. 
- 따라서 운영체제는 이런 오류가 다른 프로세스에 영향을 주지 않도록 해야 한다.
- 보통, 오류가 발생하면 하드웨어는 트랩을 발생하며, 운영체제는 트랩을 발생시킨 프로세스를 강제로 종료시키고 적절한 오류 메세지를 출력한다.

1. **이중모드 동작**
   - 여러 오류로부터 프로세스를 보호하기 위해 두 가지 동작 모드를 제공한다. 현재 모드를 나타내기 위해 하드웨어에 이것을 나타내는 모드 비트(mode bit)가 있다.
     - **사용자 모드**: 사용자 프로세스는 이 모드에서 수행되다가 인터럽트나 트랩이 발생하면 모니터 모드로 전환된다.
     - **모니터 모드**: 다른 말로 슈퍼바이저(supervisor) 모드, 시스템 모드, 특권(privileged) 모드라 한다.
   - 문제를 일으킬 소지가 있는 명령어는 특권 명령으로 분류하고 이 명령은 **모니터 모드(특권 모드, 슈퍼바이저 모드)**에서만 수행되도록 하여 프로세스를 보호한다.
   - 사용자는 운영체제만이 수행할 수 있는 특권 명령의 수행을 부탁하여 운영체제와 상호작용한다. 이런 요청을 보통 **시스템 콜(system call)**이라 하며, 하드웨어는 이런 시스템 콜을 **소프트웨어 인터럽트(트랩)**로 간주한다.
2. **입출력 보호**
   - 사용자가 불법적인 입출력 요청을 할 수 없도록 모든 입출력 명령은 특권 명령으로 분류한다.
3. **주기억장치 보호**
   - 주기억 장치 영역은 사용자 프로그램으로부터 보호되어야 하며, 사용자 프로그램이 사용하는 주기억장치 영역은 다른 사용자 프로그램으로부터 보호되어야 한다.
   - 주기억장치를 보호하기 위해서는 특정 프로그램이 접근할 수 있는 주기억장치 영역을 결저할 수 있어야 한다. 보통 기준 레지스터(base register)와 한계 레지스터(limit register)를 이용하여 영역을 나타낸다. 
   - 사용자 프로그램은 기준 레지스터에 있는 주소 ~ 한계 레지스터 값 사이의 주소 영역만 접근 가능
4. **CPU 보호**
   - 운영체제가 항상 제어권을 확보할 수 있도록 해야 한다. 사용자 프로그램이 무한루프에 빠져 제어권을 다시 운영체제에 넘기지 않을 수 있다.
   - 이 문제를 해결하기 위해 타이머를 사용한다. 일정 시간이 경과되면 타이머는 인터럽트를 발생하여 운영체제에 제어권을 넘긴다.

