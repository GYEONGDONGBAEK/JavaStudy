# 객체지향 프로그래밍(2)

# 7. 객체지향 프로그래밍II

---

## 1.상속

### 상속

- 기존의 클래스로 새로운 클래스를 작성하는 것(코드의 재사용)
- 두 클래스를 부모와 자식으로 관계를 맺어주는 것.
- 자손은 조상의 모든 멤버를 상속받는다( 생성자, 초기화블럭 제외)
- 자손의 멤버 개수는 조상보다 적을 수 없다.(같거나 많다.)
- 자손의 변경은 조상에 영향을 미치지 않는다.
- Java는 다중상속을 허용하지 않는다. 단일상속만 가능하다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/bb081e46-a04d-4486-87a3-a1eb62ebedf3">

### 다중상속을 허용하지 않는 이유

부모 클래스가 2개인데, 각 클래스에 메소드의 이름이 겹치는 상황을 생각해보자.

그러면 누구의 메소드를 상속받을 것인지 정해야 한다.

이러한 다중상속의 문제점으로 단일 상속만을 허용한다. (그런데 C++에서는 다중상속을 허용한다.)

---

## 포함관계, 상속관계

### 포함관계

"has a" 를 넣어서 문장이 성립하면 포함관계이다.

ex) Circle has a point. (원은 점을 가지고 있다.)

```
class Point {
	int x;
    int y;
}
class Circle {
	Point c = new Point(); // 원점
    int r; // 반지름
}
```

### 상속 관계

"is a" 를 넣어서 문장이 성립하면 상속관계이다.

ex) Circle is a shape. (원은 도형이다.)

```
class Shape {
	String color = "black";
}
class Circle extends Shape {
	...
}
```

JAVA에서 다중상속처럼 하는 방법 ⇒ 비중이 높은 클래스 하나만 상속관계, 나머지는 포함으로 한다.

---

## Overriding

"~위에 덮어쓰다." 라는 뜻이다.

말 그대로 조상 클래스로부터 상속받은 **기존의 메소드**의 내용을 변경하는 것을 말한다.

### 조건

조상 클래스의 메소드와

1. 이름이 같아야 한다.
2. 매개변수가 같아야 한다.
3. 반환타입이 같아야 한다.

  => 즉 선언부가 서로 일치해야 한다.

<aside>
💡 **오버로딩/ 오버라이딩/ 메서드 정의**

Class Parent{
void parentMethod(){}
}

class Child extends Parent{
void parentMethod() {} // 오버라이딩
void parentMethod(int i){} // 오버로딩

void childMethod(){} // 메서드 정의

void childMethod(int i){} // 오버로딩

void childMethod(){} // 중복정의

}

</aside>

---

## super

자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조변수이다.

```
class Parent {
	int x = 10;
}

class Child extends Parent{
	int x = 20;
    void method() {
    	System.out.println(super.x);  // 10
        System.out.println(this.x);   // 20
    }
}
```

만약 `super()` 이렇게 사용한다면 조상 클래스의 생성자를 부른다는 뜻이다.

**Object 클래스를 제외한 클래스의 생성자 첫 줄에는 `super();`가 붙어있다. 안 붙이면 컴파일러가 알아서 붙여준다.**

그런데 만일 부모 클래스에 **기본 생성자가 아닌 생성자**가 들어가있다면 자식 클래스에 부모 클래스의 생성자를 붙여줘야 한다.

```
class Parent {
    int x = 10;

    public Parent(int x) {
        this.x = x;
    }
}

class Child extends Parent {
    int x = 20;

    public Child(int x) {
        // super(10); 없으면 컴파일 에러!
        this.x = x;
    }
    public void method() {
        System.out.println(this.x);
        System.out.println(super.x);
    }
}
public class Test {
    public static void main(String[] args) {
        Child c = new Child(20);
        c.method();
    }
}
```

**조상 클래스의 멤버변수는 이처럼 조상의 생성자에 의해 초기화되도록 해야 하는 것이다.**

---

## 패키지(package)

- 서로 관련된 클래스의 묶음
- 클래스는 클래스 파일(*.class), 패키지는 폴더. 하위 패키지는 하위 폴더
- 클래스의 실제 이름(full name)은 패키지를 포함. (ex . java.lang.String)

### 패키지의 선언

- 패키지는 소스파일의 첫 번째 문장으로 단 한번 선언
- 같은 소스 파일의 클래스들은 모두 같은 패키지에 속하게 된다.
- 패키지 선언이 없으면 이름없는(unnamed) 패키지(default package)에 속하게 된다.

---

### Import

<aside>
💡 import 패키지명.클래스명;
  또는
import 패키지명.*;

</aside>

- import 문의 역할은 컴파일러에게 소스파일에 사용된 클래스의 패키지에 대한 정보를 제공하는 것이다.
- import 문은 프로그램의 성능에 전혀 영향을 미치지 않고 컴파일 시간이 아주 조금 더 소요된다.

📍 **static import 문**

- static import 문을 사용하면 static멤버를 호출할 때 클래스 이름 생략 가능

<aside>
💡 import static java.lang.System.out;

class StaticImport {
  public static void main(String[] args) {
    out.println("Hello World!");
  }
}

</aside>

---

## 제어자(modifier)

- 제어자는 클래스 변수 또는 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여
- 제어자의 종류
    - 접근 제어자 : `public`, `protected`, `default`, `private`
    - 그 외 : `static`, `final`, `abstract`, `native`, `transient`, `synchronized`, `volatile`, `strictfp`

### `static` -클래스의, 공통적인

- `static`멤버 변수는 하나의 변수를 모든 인스턴스가 공유하기 때문에 인스턴스에 관계없이 같은 값을 갖는다.
- `static`은 멤버 변수, 메서드, 초기화 블럭에서 사용될 수 있다.

### `final` -마지막의, 변경될 수 없는

- 변수에 사용되면 상수, 메서드에 사용되면 오버라이딩 불가능하고, 클래스에 사용되면 상속이 불가능하다.
- `final`은 클래스, 메서드, 멤버 변수, 지역 변수에서 사용될 수 있다.

**생성자를 이용한 `final`멤버 변수의 초기화**

- 인스턴스 변수의 경우 생성자에서 초기화가 가능
- 이 기능을 활용하여 각 인스턴스마다 `final`멤버 변수가 다른 값을 갖도록 하는 것이 가능

### `abstract` - 추상의, 미완성의

- 메서드의 선언부만 작성하고 실제 수행내용은 구현하지 않은 추상 메서드를 선언하는데 사용
- `abstract`는 클래스, 메서드에서 사용될 수 있다.

### 접근 제어자

- 멤버 또는 클래스에 사용되어, 해당하는 멤버 또는 클래스를 외부에서 접근하지 못하도록 제한하는 역할
- 접근 제어자가 사용될 수 있는 곳 - 클래스, 멤버 변수, 메서드, 생성자
    - `private` : 같은 클래스 내에서만 접근 가능
    - `default` : 같은 패키지 내에서만 접근 가능
    - `protected` : 같은 패키지 내에서, 그리고 다른 패키지의 자손 클래스에서 접근 가능
    - `public` : 접근 제한 x

**접근 범위**

```
public > protected > (default) > private
```

**접근 제어자를 이용한 캡슐화**

- 클래스의 내부에 선언된 데이터를 보호하기 위해서 클래스나, 멤버에 접근 제어자를 사용
- 외부로부터의 접근을 제한하는 것을 데이터 감추기(data hiding)라고 하며, 객체지향개념의 캡슐화(encapsulation)에 해당하는 내용이다.

**접근 제어자를 사용하는 이유**

- 외부로부터 데이터를 보호하기 위해서
- 외부에는 불필요한, 내부적으로만 사용되는, 부분을 감추기 위해서

**생성자의 접근 제어자**

- 생성자에 접근 제어자를 사용함으로써 인스턴의 생성을 제한할 수 있음
- 생성자의 접근 제어자를 `private`로 지정하면,외부에서 생성자에 접근할 수 없으므로 클래스 내부에서 인스턴스를 생성해 반환해주는 `public` 메서드를 제공함으로써 외부에서 인스턴스를 사용할 수 있게 할 수 있음
- 생성자가 `private`인 클래스는 자손클래스에서 조상클래스 생성자 호출이 불가능하기 때문에 다른 클래스의 조상이 될 수 없음

### 제어자(modifier)의 조합

제어자를 조합해서 사용할 때 주의해야 할 사항

- 메서드에 `static`과 `abstract`를 함께 사용할 수 없다.
    - `static` 메서드는 몸통이 있는 메서드에만 사용할 수 있기 때문이다.
- 클래스에 `abstract`와 `final`을 동시에 사용할 수 없다.
    - 클래스에 사용되는 `final`은 클래스를 확장할 수 없다는 의미이고 `abstract`는 상속을 통해서 완성되어야 한다는 의미이므로 서로 모순되기 때문이다.
- `abstract` 메서드의 접근 제어자가 `private`일 수 없다.
    - `abstract` 메서드는 자손클래스에서 구현해주어야 하는데 접근 제어자가 `private`이면, 자손클래스에서 접근할 수 없기 때문이다.
- 메스드에 `private`과 `final`을 같이 사용할 필요는 없다.
    - 접근 제어자가 `private`인 메서드는 오버라이딩될 수 없기 때문이다.
    
    ---