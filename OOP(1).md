# 객체지향 프로그래밍(1)

---

# 6. 객체지향 프로그래밍Ⅰ

---

## 1. 객체지향언어

### 주요 특징

1. 코드의 재사용성이 높다.
2. 코드의 관리가 용이하다.
3. 신뢰성이 높은 프로그래밍을 가능하게 한다.

---

객체 지향의 핵심적인 4가지 특징

1. 캡슐화
2. 상속화
3. 추상화
4. 다형성

---

## 2. 클래스와 객체

클래스란 '객체를 정의해 놓은 것', 또는 '객체의 설계도 또는 틀'이라고 정의할 수 있다.

> 클래스의 정의 :객체(실제로 존재하는 것, 사물 or 개념)를 정의해 놓은 것이다.
> 
> 
> 클래스의 용도 **:** 객체를 생성하는데 사용된다.
> 

프로그래밍에서 객체는 클래스에 정의된 내용대로 메모리에 생성된 것을 뜻한다.

> 객체의 정의 실제로 존재하는 것. 사물 또는 개념
> 
> 
> **객체의 용도** 객체가 가지고 있는 기능과 속성에 따라 다름.
> 
> **유형의 객체** 책상, 의자, 자동차, TV와 같은 사물
> 

<aside>
💡 클래스 -제품 설계도
객체 - 제품

설계도를 만드는 이유 : 제품을 쉽게 만들기 위해.
제품을 만드는 이유 : 제품이 가지고 있는 특성을 사용하기 위해

</aside>

객체: 모든 인스턴스를 대표하는 일반적 용어

인스턴스:특정 클래스로부터 생성된 객체(예:TV인스턴스)

```
               인스턴스화
클래스-----------------------------> 인스턴스(객체)
```

-인스턴스의 생성과 사용

<aside>
💡 class Tv {
  String color;
  boolean power;
  int channel;

  void power() { power != power; }
  void channelUp() { channel += 1; }
  void channelDown() { channel -= 1; }
}

class Tvtest {
  public static void main(String args[]) {
    Tv t; // Tv 클래스 타입의 참조변수 t 선언
    t = new Tv(); // Tv클래스의 인스턴스가 메모리의 빈 공간에 생성됨
    t.channel = 7; // 인스턴스의 멤버 변수 channel에 7을 저장
    t.channelDown(); // Tv인스턴스의 channelDown 메서드 호출
    System.out.println("현재 채널은 " + t.channel + " 입니다");
  }
}

</aside>

인스턴스는 참조 변수를 통해서만 다룰 수 있으며, 참조 변수의 타입은 인스턴스의 타입과 일치해야 한다.

---

## 3. 변수

| 변수의 종류 | 선언위치 | 생성시기 |
| --- | --- | --- |
| 클래스 변수 | 클래스 영역 | 클래스가 메모리에 올라갈 때 |
| 인스턴스 변수 | 클래스 영역 | 인스턴스가 생성되었을 때 |
| 지역 변수 | 매서드, 생성자, 초기화 블럭 내부 | 변수 선언문이 수행되었을 때 |

(1) 인스턴스 변수 - 클래스 영역에 선언되며, 클래스의 인스턴스를 생성할 때 만들어짐. 독립적인 저장공간을 가진다.

(2) 클래스 변수 - 인스턴스 변수 앞에 static을 붙임. 모든 인스턴스가 공통된 저장공간을 공유한다. 인스턴스 생성 없이 언제라도 바로 사용할 수 있음. '클래스이름.클래스변수'의 형식으로 사용. 메모리에 로딩될 때 생성되어 프로그램 종료까지 유지되며 전역변수의 성격을 갖는다.

(3) 지역 변수 - 블럭 내에 선언된 지역변수는 블럭을 벗어나면 소멸되어 사용할 수 없음.

## 메서드

메서드(method)는 특정 작업을 수행하는 일련의 문장들을 하나로 묶인 것이다.

메서드를 사용하는 이유

1. 높은 재사용성(reusability)
2. 중복된 코드의 제거
3. 프로그램의 구조화

메서드의 선언과 구현

```cpp
반환 타입 메서드 이름 (타입 변수명, ...) {
  // 수행될 코드
}

int add(int a, int b) {
  return a + b;
}
```

메서드 호출

```
메서드이름(arg1, arg2, ...);

int res = add(1, 3);
```

---

## JVM의 메모리 구조

JVM은 시스템으로부터 프로그램을 수행하는데 필요한 메모리를 할당받고 JVM은 이 메모리를 용도에 따라 여려 영역으로 나누어 관리한다.

1. 메서드 영역(method area)
    - 프로그램 실행 중 어떤 클래스가 사용되면, JVM은 해당 클래스의 클래스 파일을 읽어서 분석하여 클래스에 대한 정보를 이곳에 저장한다. 이때, 그 클래스의 클래스 변수도 이 역역에 생성된다.
2. 힙(heap)
    - 인스턴스가 생성되는 공간
3. 호출 스택(call stack or excution stack)
    - 메서드의 작업에 필요한 메모리 공간을 제공

---

## **기본형 매개변수와 참조형 매개변수**

기본형 매개변수

- 기본형 값 복사
- 변수의 값을 읽기만 가능

참조형 매개변수

- 인스턴스의 주소 복사
- 변수의 값을 읽고 변경 가능

---

## 클래스 메서드와 인스턴스 메서드

변수와 마찬가지로 `static`이 붙어 있으면 클래스 메서드, 붙어 있지 않으면 인스턴스 메서드다.

인스턴스 메서드는 인스턴스 변수와 관련된 작업을 하는, 즉 메서드의 작업을 수행하는데 인스턴스 변수를 필요로 하는 메서드이다. 반면에 인스턴스와 관계없는 메서드를 클래스 메서드로 정의한다.

📌 정리

1. 클래스를 설계할 때, 멤버 변수 중 모든 인스턴스에 공통으로 사용하는 것에 `static`을 붙인다.
2. 클래스 변수는 인스턴스를 생성하지 않아도 사용할 수 있다.
3. 클래스 메서드는 인스턴스 변수를 사용할 수 없다.
4. 메서드 내에서 인스턴스 변수를 사용하지 않는다면, `static`을 붙이는 것을 고려한다.

```
class Math {
  long a, b;
  public Math(int a, int b) {
    this.a = a;
    this.b = b;
  }
  // 인스턴스 메서드long add() { return a + b; }
  long substract() { return a - b; }
  long multiply() { return a * b; }
  double devide() { return a / b; }
  // 클래스 메서드static long add(int a, int b) { return a + b; }
  static long substract(int a, int b) { return a - b; }
  static long multiply(int a, int b) { return a * b; }
  static double devide(int a, int b) { return a / b; }
}

class MathTest {
  public static void main(String[] args)  {
    // 클래스 메서드는 인스턴스 생성없이 호출 가능
    Math.add(200, 100);
    Math.substract(200, 100);
    Math.multiply(200, 100);
    Math.devide(200, 100);

    Math math = new Math(200, 100);
    // 인스턴스 메서드는 인스턴스 생성 후 호출 가능
    math.add();
    math.substract();
    math.multiply();
    math.devide();
  }
}
```

## 클래스 멤버와 인스턴스 멤버간 참조, 호출

같은 클래스에 속한 멤버들 간에는 별도의 인스턴스를 생성하지 않고도 서로 참조 또는 호출이 가능하다. 단, 클래스 멤버가 인스턴스 멤버를 참조 또는 호출하고자 하는 경우에는 인스턴스를 생성해야 한다. 그 이유는 클래스 멤버가 존재하는 시점에 인스턴스 멤버가 존재하지 않을 수도 있기 때문이다.

```cpp
class Test {
  int iv;
  static int cv;
  void instanceMethod() { }
  static void staticMethod() { }

  void instanceMethod2() {
    instanceMethod();
    staticMethod();
  }

  static void staticMethod2() {
    // int a = iv; // Errorint a = new Test().iv;
    int b = cv;
    // instanceMethod(); // Errornew Test().instanceMethod();
    staticMethod();
  }
}
```

## 오버 로딩(Overloading)

한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 '메서드 오버 로딩' 또는 '오버 로딩'이라 한다.

### 오버 로딩의 조건

오버 로딩이 성립하기 위해서는 다음과 같은 조건을 만족해야 한다.

1. 메서드 이름이 같아야 한다.
2. 매개변수 개수 또는 타입이 달라야 한다.
3. 반환 타입은 영향이 없다.

오버 로딩의 몇 가지 예

- 보기 1

```cpp
// 매개변수만 다를 경우int add(int a, int b) {
  return a + b;
}
int add(int x, int y) {
  return x + y;
}
```

위 코드는 오버 로딩이 성립하지 않는다.

- 보기 2

```cpp
// 반환 타입만 다를 경우int add(int a, int b) {
  return a + b;
}
long add(int a, int b) {
  return a + b;
}
```

위 코드도 오버로딩이 성립하지 않는다.

- 보기 3

```cpp
// 매개변수 타입의 순서가 다른 경우long add(int a, long b) {
  return a + b;
}
long add(long a, int b) {
  return a + b;
}
```

위 코드는 오버 로딩으로 간주한다. 하지만 `add(3, 3)`과 같이 호출한다면 두 메서드 중 어느 메서드 호출된 것인지 알 수 없기 때문에 컴파일 에러가 발생한다.

- 보기 4

```cpp
int add(int a, int b) {
  return a + b;
}
long add(int a, long b) {
  return a + b;
}
long add(int[] a) {
  int ret = 0;
  for (int i : a) {
    ret += i;
  }
  return ret;
}
```

위 코드는 바르게 오버 로딩되어 있다.

### 오버 로딩의 장점

- 오버 로딩을 통해 여러 메서드들이 하나의 이름으로 정의할 수 있다.
- 메서드의 이름을 절약할 수 있다.

---

## 생성자

생성자는 인스턴스가 생성될 때 호출되는 '인스턴스 초기화 메서드'다.

생성자의 조건

- 생성자의 이름은 클래스의 이름과 같아야 한다.
- 생성자는 리턴 값이 없다.

```
class Class_name {
  Class_name() {
    ...
  }
  Class_name(String k, int num) {
    ...
  }
}
```

참고❗️

- **연산자 `new`가 인스턴스를 생성하는 것이지 생성자가 인스턴스를 생성하는 것이 아니다.**

### 기본 생성자

모든 클래스에는 반드시 하나 이상의 생성자가 정의되어 있어야 하지만 컴파일러에서 `기본 생성자`를 제공하기 때문에 생성자를 정의하지 않아도 인스턴스를 생성할 수 있었다.

> 기본 생성자가 컴파일러에 추가되는 경우는 클래스에 정의된 생성자가 하나도 없을 때뿐이다.
> 

### 매개변수가 있는 생성자

생성자에 매개변수를 선언하여 인스턴스의 초기화 작업에 사용할 수 있다.

```arduino
class Math {
  long a, b;
  Math(long a, long b) {
    this.a = a;
    this.b = b;
  }

  public static void main(String[] args) {
    Math math = new Math(1, 2);
  }
}
```

### 생성자에서 다른 생성자 호출하기

- 생성자의 이름으로 클래스 이름 대신 this를 사용한다.
- 한 생성자에서 다른 생성자를 호출할 때는 반드시 첫 줄에서만 호출이 가능하다.

```tsx
class Math {
  long a, b;

  Math() {
    this(-1, -1);
  }

  Math(long a, long b) {
    this.a = a;
    this.b = b;
  }

  public static void main(String[] args) {
    Math dMath = new Math(); // -1, -1로 초기화Math math = new Math(1, 2); // 1, 2로 초기화
  }
}
```

`this`는 참조 변수로 인스턴스 자신을 가리킨다. 그리고 인스턴스 멤버만 사용할 수 있으며, `static`메서드에서는 사용할 수 없다.

> this 인스턴스 자신을 가리키는 참조 변수, 인스턴스의 주소가 저장되어 있다.
> 
> 
> 모든 인스턴스 메서드에 지역변수로 숨겨진 채로 존재한다.
> 
> `this(), this(arguments)` 생성자, 같은 클래스의 다른 생성자를 호출할 때 사용한다.
> 

---

# 변수의 초기화

**멤버 변수와 배열의 초기화는 선택적이지만, 지역변수의 초기화는 필수적이다.**

📍 각 타입의 기본값

| 자료형 | 기본값 |
| --- | --- |
| boolean | false |
| char | '\u000' |
| byte, short, int | 0 |
| long | 0L |
| float | 0.0f |
| double | 0.0d or 0.0 |
| 참조형 변수 | null |

📍 멤버 변수의 초기화 방법

- 명시적 초기화 (explicit intialization)
- 생성자 (Constructor)
- 초기화 블록 (initialization block)
    - 인스턴스 초기화 블록 : 인스턴스 변수를 초기화 하는데 사용
    - 클래스 초기화 블럭 : 클래스 변수를 초기화 하는데 사용

### 명시적 초기화

변수를 선언과 동시에 초기화하는 것을 명시적 초기화라고 한다.

### 초기화 블럭

- 클래스 초기화 블럭
    - 클래스 변수의 복잡한 초기화에 사용
    - 클래스가 메모리에 처음 로딩될 때 한 번만 수행
- 인스턴스 초기화 블록
    - 인스턴스 변수의 복잡한 초기화에 사용
    - 생성자와 같이 인스턴스를 생성할 때마다 수행
    - 생성자보다 먼저 수행됨
    - 공통으로 수행돼야 하는 코드를 넣는 데 사용

```
class InitBlock {
  static { ... } // 클래스 초기화 블럭
  { ... } // 인스턴스 초기화 블럭
}
```

```
Car() {
  count++;
  serialNo = count;
  ...
}

Car(String color, String gearType) {
  count++;
  serialNo = count;
  ...
}
```

위 코드를 아래와 같이 바꾸면 코드가 보다 간결해진다.

```
{
  count++;
  serialNo = count;
}

Car () {
  ...
}
Car (String color, String gearType) {
  ...
}
```

코드의 중복을 제거하는 것은 코드의 신뢰성을 높여 주고, 오류의 발생 가능성을 줄여준다. 즉, 재사용성을 높이고 중복을 제거하는 것이 객체지향 프로그래밍이 추구하는 궁극적인 목표다.

```arduino
class BlockTest {
  static {
    System.out.println("static { }");
  }

  {
    System.out.println("{ }");
  }

  BlockTest() {
    System.out.println("생성자");
  }

  public static void main(String[] args) {
    System.out.println("BlockTest bt = new BlockTest()");
    BlockTest bt = new BlockTest;
  }
  /* 출력 결과
    static { }
    BlockTest bt = new BlockTset()
    { }
    생성자
  */
}
```

### 멤버변수의 초기화 순서와 시점

- 클래스 변수
    - 초기화 시점
        - 클래스가 처음 로딩될 때 단 한번 초기화된다.
    - 초기화 순서
        - 기본값 -> 명시적 초기화 -> 클래스 초기화 블록
- 인스턴스 변수
    - 초기화 시점
        - 인스턴스가 생성될 때마다 각 인스턴스 별로 초기화가 이루어진다.
    - 초기화 순서
        - 기본값 -> 명시적 초기화 -> 인스턴스 초기화 블록 -> 생성자