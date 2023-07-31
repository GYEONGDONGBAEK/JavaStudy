# [Java] JVM 구조-(2)

---

## ****런타임 데이터 영역 (Runtime Data Area)****

JVM의 메모리 영역으로 자바 애플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역이다.

Method, Heap , Stack, PC Register, Native Method Stack 영역으로 나뉜다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/7a8a83c4-2f5e-4f95-9015-2acc49644fc7">

이때 Method , Heap Area 는 모든 쓰레드(Thread)가 공유하는 영역이고, Stack, PC Register, Native Method Stack은 각 쓰레드 마다 생성되는 개별 영역이다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/5d749e59-fbf1-43c5-b86d-b00698de7557">

---

## 메서드 영역 (Method Area)

- **메서드 영역**은 JVM이 시작될 때 생성되는 공간으로 **바이트 코드(.class)**를 처음 메모리 공간에 올릴 때 **초기화되는 대상을 저장**하기 위한 메모리 공간이다.
- JVM이 동작하고 클래스가 로드될 때 적재되서 **프로그램이 종료될 때까지 저장** 된다.
- Class Area 나 Static Area 로도 불린다.
- 모든 쓰레드가 공유하는 영역이라 다음과 같이 초기화 코드 정보들이 저장되게 된다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/7ce40cd3-9fc9-4f53-aa45-6d33d1e85e22">

- Type information
    - Type은 클래스와 인터페이스를 통칭하는 것으로 이해하면 된다
    - 클래스와 관련한 모든 정보
- Constant Pool
    - 문자열 상수와 같은 리터럴 상수
    - 메서드와 필드에 대한 모든 Reference를 담고 있음 (Symbolic Reference) 즉, 어떤 메서드나 필드를 참조할 때, JVM은 런타임 상수 풀을 통해 메서드나 필드의 실제 메모리 상 주소를 참조하여 중복을 막는 역할
- Field Information
    - Class 멤버 변수의 이름 및 데이터 타입, 접근 제어자에 대한 정보를 저장
- Method Information
    - Class 멤버 메서드의 이름, 리턴 타입, 매개변수, 접근제어자에 대한 정보
- Class Variable
    - static으로 선언되는 모든 클래스 변수
    - 이 변수는 모든 Instance에서 접근 가능하기 때문에 동기화 이슈가 발생할 수 있음Class Variable을 final로 선언할 경우에는 Constant Pool에 저장
- Reference to ClassLoader & class Class
    - 특정 클래스를 로드한 클래스로더의 정보를 관리
    - Class object와 서로 양방향 접근을 하기 대문에 Class Object에 대한 참조 주소 값을 가진다
- Method Table
    - Class의 Method에 대한 Direct Reference를 가진다고 보면 된다
    - Method Table을 이용해 Super Class에서 상속된 Method의 Reference까지 확인이 가능

---

### 힙 영역 (**Heap Area)**

- JVM이 관리하는 프로그램 상에서 데이터를 저장하기 위해 런타임 시 동적으로 할당하여 사용하는 영역
- new 연산자로 생성된 객체 또는 인스턴스와 배열을 저장
- 힙 영역에서 생성된 객체와 배열은 스택 영역의 변수나 다른 객체의 필드에서 참조
- 참조하는 변수나 필드가 없다면 의미 없는 객체가 되어 GC의 대상이 된다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/46fe2efa-c875-48be-b114-97fae967ca19">

힙 영역은 다시 물리적으로 **Young Generation** 과 **Old Generation** 영역으로 구분되게 되는데 다음과 같다.

- **Young Generation** : 생명 주기가 짧은 객체를 GC 대상으로 하는 영역.
    - **Eden** : new를 통해 새로 생성된 객체가 위치. 정기적인 쓰레기 수집 후 살아남은 객체들은 Survivor로 이동
    - **Survivor 0 / Survivor 1** : 각 영역이 채워지게 되면, 살아남은 객체는 비워진 Survivor로 순차적으로 이동
- **Old Generation** : 생명 주기가 긴 객체를 GC 대상으로 하는 영역. Youn Generation에서 마지막까지 살아남은 객체가 이동

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/31dec059-10a3-4a5e-acbd-f3499be759b8">

위에 존재하던 Permanet가 Java8 부터 Metaspace로 바뀌었다.

- Permanent Generation
    - Permanent Generation은 Class 혹은 Method Code가 저장되는 영역
    - PermGen은 Heap 영역에 속함
    - Default로 제한된 크기를 가지고 있음
- Metaspace
    - Metaspace는 Java 클래스 로더가 현재까지 로드한 Class들의 메타데이터가 저장되는 공간
    - JVM에 의해 관리되는 Heap 영역이 아니라 OS 레벨에서 관리되는 Native 메모리 영역에 위치
    - Default로 제한된 크기를 가지고 있지 않고, 필요한 만큼 늘어남.

---

### **스택 영역 (Stack Area)**

스택 영역은 int, long, boolean 등 기본 자료형을 생성할 때 저장하는 공간으로, **임시적으로 사용되는 변수나 정보들이 저장되는 영역**이다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/5a40fd37-5b6d-4305-a526-624ce9c71604">

Stack은 마지막에 들어온 값이 먼저 나가는 LIFO  구조로 push와 pop 기능 사용방식으로 동작한다.

메서드 호출 시마다 각각의 **스택 프레임(그 메서드만을 위한 공간)**이 생성되고 메서드 안에서 사용되는 값들을 저장하고, 호출된 메서드의 매개변수, 지역변수, 리턴 값 및 연산 시 일어나는 값들을 임시로 저장한다.

그리고 메서드 수행이 끝나면 프레임별로 삭제된다.