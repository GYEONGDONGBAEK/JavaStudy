# Exception

# 예외처리

---

# 프로그램 오류

- 컴파일 에러 : 컴파일 할 때 발생하는 에러
- 런타임 에러 : 실행 할 때 발생하는 에러
- 논리적 에러 : 작성 의도와 다르게 동작

## Java의 런타임 에러

- 에러(error) : 코드에 의해 수습될 수 없는 심각한 오류(out of Memory error)
- 예외(exception) : 코드에 의해 수습될 수 있는 다소 미약한 오류-> 에러는 어쩔 수 없지만, 예외는 처리하자.

## 예외처리의 정의와 목적

- 정의: 프로그램 실행 시 발생할 수 있는 예외의 발생에 대비한 코드를 작성하는 것
- 목적: 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하는 것

---

# 예외 처리하기. try-catch문

```java
💡 
try {
    예외를 처리하길 원하는 실행 코드;
} catch (e1) {
    e1 예외가 발생할 경우에 실행될 코드;
} catch (e2) {
    e2 예외가 발생할 경우에 실행될 코드;
}
...
finally {
    예외 발생 여부와 상관없이 무조건 실행될 코드;
}
```

1. try 블록 : 기본적으로 맨 먼저 실행되는 코드로 여기에서 발생한 예외는 catch 블록에서 처리된다.
2. catch 블록 : try 블록에서 발생한 예외 코드나 예외 객체를 인수로 전달받아 그 처리를 담당한다.
3. finally 블록 : 이 블록은 try 블록에서 예외가 발생하건 안 하건 맨 마지막에 무조건 실행된다.

catch 블록과 finally 블록은 선택적인 옵션으로 반드시 사용할 필요는 없다. 따라서 사용할 수 있는 모든 적합한 try 구문은 다음과 같다.

```java
💡 
적합한 try 구문
1. try / catch

2. try / finally

3. try / catch / ... / finally
```

### 예외 처리 메커니즘

자바에서 예외 처리는 다음과 같은 순서로 진행된다.

1. try 블록에 도달한 프로그램의 제어는 try 블록 내의 코드를 실행한다.

이때 만약 예외가 발생(throw)하지 않고, finally 블록이 존재하면 프로그램의 제어는 바로 finally 블록으로 이동한다.

1. try 블록에서 예외가 발생하면 catch 핸들러는 다음과 같은 순서로 적절한 catch 블록을 찾게 된다.

2-1. 스택에서 try 블록과 가장 가까운 catch 블록부터 차례대로 검사한다.

2-2. 만약 적절한 catch 블록을 찾지 못하면, 바로 다음 바깥쪽 try 블록 다음에 위치한 catch 블록을 차례대로 검사한다.

2-3. 이러한 과정을 가장 바깥쪽 try 블록까지 계속 검사하게 된다.

2-4. 그래도 적절한 catch 블록을 찾지 못하면, 예외는 처리되지 못한다.

1. 만약 적절한 catch 블록을 찾게 되면, throw 문의 피연산자는 예외 객체의 형식 매개변수로 전달된다.
2. 모든 예외 처리가 끝나면 프로그램의 제어는 finally 블록으로 이동한다.
3. finally 블록이 모두 처리되면, 프로그램의 제어는 예외 처리문 바로 다음으로 이동한다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/31bf98cb-52e4-4b26-bff2-b6234c8c94a2">

---

# Exception과 RuntimeException

- Exception클래스와 그 자손: 사용자의 실수와 같은 외적인 요인에 의해 발생하는 예외
- RuntimeException과 그 자손: 프로그래머의 실수로 발생하는 예외

## 

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/12a19937-9d0e-4de7-b299-d3d218d09933">

## 예외 처리의 계층 관계

자바에서는 예외가 발생하면, try 블록과 가장 가까운 catch 블록부터 순서대로 검사한다.

따라서 여러 개의 catch 블록을 사용할 때는 Exception 클래스의 계층 관계에도 주의를 기울여야만 한다.

```java
💡
try{

    System.out.write(list);

} catch (Exception e) {

    e.printStackTrace();

} catch (IOException e) {

    e.printStackTrace();
}
```

위의 예제에서 IOException이 발생하면, 자바는 첫 번째 catch 블록부터 순서대로 해당 예외를 처리할 수 있는지를 검사한다.

그런데 IOException은 Exception의 자식 클래스이므로, 첫 번째 catch 블록에서도 IOException을 처리할 수 있다.

따라서 IOException을 비롯한 Exception 클래스의 자식 클래스에 해당하는 예외가 발생하면, 언제나 첫 번째 catch 블록에서만 처리될 것이다.

즉, catch 블록의 순서를 위의 예제처럼 작성하면, 두 번째 catch 블록은 영원히 실행되지 못할 것이다.

따라서 IOException만을 따로 처리하고자 한다면, 다음 예제처럼 catch 블록의 순서를 변경해야 한다.

```java
💡

try {

    System.out.write(list);

} catch (IOException e) {

    e.printStackTrace();

} catch (Exception e) {

    e.printStackTrace();

}
```

---

### Throwable 클래스

자바에서 Throwable 클래스는 모든 예외의 조상이 되는 Exception 클래스와 모든 오류의 조상이 되는 Error 클래스의 부모 클래스다.

Throwable 타입과 이 클래스를 상속받은 서브 타입만이 자바 가상 머신(JVM)이나 throw 키워드에 의해 던져질 수 있다.

이 클래스에는 예외나 오류에 관한 다양한 정보를 확인할 수 있는 다음과 같은 메소드가 포함되어 있다.

| 메소드 | 설명 |
| --- | --- |
| String getMessage() | 해당 throwable 객체에 대한 자세한 내용을 문자열로 반환함. |
| void printStackTrace() | 해당 throwable 객체와 표준 오류 스트림(standard error stream)에서 해당 객체의 스택 트레이스(stack trace)를 출력함. |
| String toString() | 해당 throwable 객체에 대한 간략한 내용을 문자열로 반환함. |

### 자주 사용되는 예외 클래스

자바에서 자주 사용되는 예외 클래스는 다음과 같다.

| 클래스 | 설명 |
| --- | --- |
| ClassCastException | 수행할 수 없는 타입 변환이 진행될 경우 |
| ArrayIndexOutOfBoundsException | 배열에 잘못된 인덱스를 사용하여 접근할 경우 |
| NullPointerException | null 객체의 인스턴스 메소드를 호출하는 등의 경우 |
| ArithmeticException | 산술 연산에서 정수를 0으로 나누는 등 연산을 수행할 수 없는 경우 |

---

# 예외 던지기

## 예외 발생시키기

자바에서 강제로 예외를 발생시키기 위해서는 throw를 사용하면 된다. 아래 예시에서는 강제로 Exception을 발생시키면 catch문에서 예외를 잡고 Exception에 대한 메시지를 출력한다.

```java
try {
    // throw로 강제 예외 발생
    throw new Exception("예외 발생시키기");
} catch (Exception e)    {
    System.out.println("err_msg : " + e.getMessage());
    e.printStackTrace();
}
```

## **예외 떠넘기기 (throws)**

예외가 발생할 수 있는 코드를 작성할 때 try - catch 블록으로 처리하는 것이 기본이지만, 경우에 따라서는 다른 곳에서 예외를 처리하도록 호출한 곳으로 예외를 떠넘길 수도 있다.

이때 사용하는 키워드가 throws이다. throws 는 메소드 선언부 끝에 작성되어 메소드에서 예외를 직접 처리(catch)하지 않은 예외를 호출한 곳으로 떠넘기는 역할을 한다.

```java
throws 로 떠넘기기 전

public class Main {
    public static void main(String[] args) {
        method1();
        method2();
    }

    public static void method1() {
        try {
            throw new ClassNotFoundException("에러1");
        } catch (ClassNotFoundException e) {
            System.out.println(e.getMessage());
        }
    }

    public static void method2() {
        try {
            throw new ArithmeticException("에러2");
        } catch (ArithmeticException e) {
            System.out.println(e.getMessage());
        }
    }
}
---------------------------------------------------------
throws 로 떠넘긴 후

public class Main {
    public static void main(String[] args) {
        try {
            method1();
            method2();
        } catch (ClassNotFoundException | ArithmeticException) {
            System.out.println(e.getMessage());
        }
    }

    public static void method1() throws ClassNotFoundException {
        throw new ClassNotFoundException("에러1");
    }

    public static void method2() throws ArithmeticException {
        throw new ArithmeticException("에러2");
    }
}
```

---

## 예외와 트랜잭션

트랜잭션(Transaction)은 하나의 작업 단위를 뜻한다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/f1653a9b-d57c-4710-a10a-4bf3431f2515">

즉, 자바 코드에서 메서드 블럭내의 코드들이 예외가 발생해도 모두 실행되느냐 아니면 예외가 발생하면 그상태로 중지하느냐의 작업 단위를 개발자가 어떤 형태의 예외 처리 방법을 사용하느냐에 따라 달라지게 된다.

예를들어 각 메서드에서 일일히 try - catch 하면, 메인 메소드에 있는 메서드 실행 코드 부분은 모두 실행 자체는 된다.

왜냐하면 예외처리를 각 메서드에서 하기 때문에 상위의 메인 메서드의 코드들은 모두 실행되게 된다.

```java
상품발송() {
    포장();
    영수증발행();
    발송();
}

포장(){
    try {
       ...
    }catch(예외) {
       포장취소();
    }
}

영수증발행() {
    try {
       ...
    }catch(예외) {
       영수증발행취소();
    }
}

발송() {
    try {
       ...
    }catch(예외) {
       발송취소();
    }
}
```

만약 포장 단계에서 예외가 발생하더라도, 영수증발행과 발송은 별도로 진행되기때문에 문제가 발생한다.

```java
상품발송() {
    try {
        포장();
        영수증발행();
        발송();
    }catch(예외) {
        모두취소();  // 하나라도 실패하면 모두 취소한다.
    }
}

포장() throws 예외 {
   ...
}

영수증발행() throws 예외 {
   ...
}

발송() throws 예외 {
   ...
}
```

이렇게 작성하게 되면 포장단계에서 문제가 생긴다면 상품발송 단계에서 모두 취소하기때문에 영수증발행과 발송은 진행되지 않는다.