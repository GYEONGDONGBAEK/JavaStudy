# [Java] JVM 구조-(1)



## VM (****Virtual Machine) 이란?****

JVM 을 알아보기 전에 VM에 대해 알아보겠다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/700c6198-3f8f-4e2c-8a69-844e369615f8">

VM은 물리 컴퓨터의 가상 표현이다. VM을 게스트 머신이라고 부르고, 그것이 실행되는 물리 컴퓨터를 호스트 머신이라고 부른다.

하나의 물리 머신은 각각 자체 운영 체제와 응용 프로그램을 갖춘 여러 개의 VM을 실행할 수 있으며, 이러한 VM은 서로 격리된다.

---

# JVM(****Java Virtual Machine)****

C와 C++과 같은 프로그래밍 언어에서 코드는 먼저 플랫폼별 기계 코드로 컴파일된다. 이러한 언어를 컴파일 언어라고 한다.

반면에 JavaScript와 Python과 같은 언어에서는 컴퓨터가 컴파일할 필요 없이 명령어를 직접 실행한다. 이러한 언어를 인터프리터 언어라고 한다.

Java는 두 기술의 조합을 사용한다. Java 코드는 먼저 바이트 코드로 컴파일되어 클래스 파일을 생성한다. 이 클래스 파일은 기본 플랫폼에서 Java Virtual Machine에 의해 해석된다. 동일한 클래스 파일은 기계의 플랫폼 및 운영 체제와 관계없이 모든 버전의 JVM에서 실행할 수 있다.

가상 머신과 유사하게, JVM은 호스트 기계에서 격리된 공간을 만든다. 이 공간은 기계의 플랫폼이나 운영 체제와 관계없이 Java 프로그램을 실행하는 데 사용할 수 있다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/11051f90-74e6-4a42-978e-b1d4b1e50208">

### JVM의 동작 방식

1. 자바 프로그램을 실행하면 JVM은 OS로부터 메모리를 할당받는다.
2. 자바 컴파일러(javac)가 자바 소스코드(.java)를 자바 바이트 코드(.class)로 컴파일 한다.
3. **Class Loader**는 동적 로딩을 통해 필요한 클래스들을 로딩 및 링크 하여 **Runtime Data Area(실질적인 메모리를 할당 받아 관리하는 영역)**에 올린다.
4. **Runtime Data Area**에 로딩 된 바이트 코드는 **Execution Engine**을 통해 해석된다.
5. 이 과정에서 **Execution Engine**에 의해 **Garbage Collector**의 작동과 **Thread** 동기화가 이루어진다.

---

# JVM의 구조

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/77e76417-aaf2-43d0-9f27-89a9bd3739ce">

JVM은 세 개의 서로 다른 구성 요소로 구성된다.

- 클래스 로더(Class Loader)
- 런타임 데이터 영역(Runtime Data Area)
- 실행 엔진(Execution Engine)

---

## 클래스 로더(Class Loader)

**클래스 로더**는 JVM 내로 클래스 파일(*.class)을 동적으로 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈이다.

즉, 로드된 **바이트 코드(.class)들을 엮어서 JVM의 메모리 영역인 Runtime Data Areas에 배치**한다.

클래스를 메모리에 올리는 로딩 기능은 한번에 메모리에 올리지 않고, 어플리케이션에서 필요한 경우 동적으로 메모리에 적재하게 된다.

클래스 파일의 로드 프로세스는 다음과 같이 3단계로 구성된다. (Loading → Linking → Initialization)

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/cdae2de9-d0c7-4f6a-819a-2f10e070cf0f">

### **로딩(Loading)**

특정 이름의 클래스나 인터페이스의 이진 표현(바이트 코드)을 가져와서 원래의 클래스나 인터페이스를 생성하는 과정

### **링킹(Linking)**

클래스가 메모리에 로딩된 후, 링킹 과정을 거친다. 클래스나 인터페이스를 링크하는 것은 프로그램의 다른 요소와 의존성을 함께 결합하는 것을 포함한다.

- **검증(Verification)**: .class 파일의 구조적 올바름을 제약 조건 또는 규칙을 통해 검사한다. 검증이 어떤 이유로 실패하면 VerifyException이 발생한다.
- **준비(Preparation)**:  JVM은 클래스나 인터페이스의 정적 필드에 대한 메모리를 할당하고, 그것들을 기본값으로 초기화한다.
- **해석(Resolution)**: 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경한다.

### 초기화(Initialization)

클래스나 인터페이스의 초기화 메서드를 실행하는 것을 포함한다. 클래스의 생성자를 호출하고 정적 블록을 실행하며, 모든 정적 변수에 값을 할당하는 것을 포함할 수 있다.