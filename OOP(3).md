# 객체지향 프로그래밍(2)

## **7. 객체지향 프로그래밍II-(2)**

---

## 다형성(Polymorphism)

객체지향개념에서 다형성이란 '여러 가지 형태를 가질 수 있는 능력'을 의미하며, 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다형성을 프로그램적으로 구현하였다.

- **조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하였다.**

<aside>
💡 class Tv {
  ...
}

class CationTv extends Tv {
  ...
}

Tv t = new CationTv();
CationTv c = new CationTv();

</aside>

실제 인스턴스가 CationTv타입이라 할지라도, 참조 변수 t로는 CationTv인스턴스의 모든 멤버를 사용할 수 없다. **둘 다 같은 타입의 인스턴스지만 참조변수의 타입에 따라 사용할 수 있는 멤버의 개수가 달라진다.**

`CationTv c = new Tv();` 와 같은 코드는 컴파일 에러가 발생한다. 그 이유는 실제 인스턴스인 Tv의 멤버 개수보다 참조변수 c가 사용할 수 있는 멤버 개수가 더 많기 때문이다.

**참조변수가 사용할 수 있는 멤버의 개수는 인스턴스의 멤버 개수보다 같거나 적어야 한다.**

---

### 참조 변수의 형변환

### 참조변수의 형변환 하는 이유

 ⇒참조변수를 변경함으로써 사용할 수 있는 멤버의 개수를 조절하기 위해서

---

자바에서는 참조 변수도 다음과 같은 조건에 따라 형변환을 할 수 있다.

1. 서로 상속 관계에 있는 클래스 사이에만 형변환을 할 수 있다.

2. 자식 클래스 타입에서 부모 클래스 타입으로의 형변환은 생략할 수 있다.

3. 하지만 부모 클래스 타입에서 자식 클래스 타입으로의 형변환은 반드시 명시해야 한다.

참조 변수의 형변환도 기본 타입의 형변환과 마찬가지로 타입 캐스트 연산자(())를 사용한다.

### 문법

(변환할클래스이름) 변환할 참조변수

다음 예제는 참조 변수의 형변환을 보여주는 예제입니다.

<aside>
💡 **class** Parent { ... }

**class** Child **extends** *Parent* { ... }

**class** Brother **extends** *Parent* { ... }

...

**Parent** pa01 **=** **null**;

**Child** ch **=** **new** **Child**();

**Parent** pa02 **=** **new** **Parent**();

**Brother** br **=** **null**;

pa01 **=** ch;          *// pa01 = (Parent)ch; 와 같으며, 타입 변환을 생략할 수 있음.*

br **=** (**Brother**)pa02; *// 타입 변환을 생략할 수 없음.*

br **=** (**Brother**)ch;   *// 직접적인 상속 관계가 아니므로, 오류 발생.*

</aside>

---

### instanceof 연산자

이러한 다형성으로 인해 런타임에 참조 변수가 실제로 참조하고 있는 인스턴스의 타입을 확인할 필요성이 생긴다.

자바에서는 instanceof 연산자를 제공하여, 참조 변수가 참조하고 있는 인스턴스의 실제 타입을 확인할 수 있도록 해준다.

자바에서 instanceof 연산자는 다음과 같이 사용한다.

### 문법

<aside>
💡 참조변수 **instanceof** 클래스이름

</aside>

왼쪽에 전달된 참조 변수가 실제로 참조하고 있는 인스턴스의 타입이 오른쪽에 전달된 클래스 타입이면 true를 반환하고, 아니면 false를 반환한다.

만약에 참조 변수가 null을 가리키고 있으면 false를 반환한다.

<aside>
💡 **class** Parent { }

**class** Child **extends** *Parent* { }

**class** Brother **extends** *Parent* { }

**public** **class** Polymorphism01 {

**public** **static** **void** **main**(**String**[] *args*) {

**Parent** p **=** **new** **Parent**();

**System.**out**.**println(p **instanceof** **Object**); *// true*

**System.**out**.**println(p **instanceof** **Parent**); *// true*

**System.**out**.**println(p **instanceof** **Child**);  *// false*

---

**Parent** c **=** **new** **Child**();

**System.**out**.**println(c **instanceof** **Object**); *// true*

**System.**out**.**println(c **instanceof** **Parent**); *// true*

**System.**out**.**println(c **instanceof** **Child**);  *// true*

****}

}

</aside>

---

매개변수의 다형성

- 참조형 매개변수는 메서드 호출시, 자신과 같은타입 또는 자손타입의 인스턴스를 넘겨줄 수 있다.

<aside>
💡 Class Product{
int price;
int bonusPoint;
}
class Tv extends Product {}
class Computer extends Product{}

Class Buyer{
int money= 1000;
int bonusPoint= 0;
}

---

만약 다형성을 안 쓴다면.

void buy(Tv t){
money-=t.price;
bonusPoint+=t.bonusPoint;
}
void buy(Computer c){
money-=c.price;
bonusPoint+=c.bonusPoint;
}

---

다형성을 사용 한다면
void buy(Product p){
money-=p.price;
bonusPoint+=bonusPoint;
}
Product p=new Tv();
Product p1=new Computer();

메서드를 중복선언 하지 않아도 된다.

</aside>

---

## 추상 클래스(abstract class)

추상 클래스는 클래스로서의 역할을 다 못하지만, 새로운 클래스를 작성하는데 있어서 바탕이 되는 조상 클래스로서 중요한 의미를 갖는다. 추상 클래스는 키워드 `abstract` 를 붙인다.

추상 클래스는 추상 메서드를 포함하고 있다는 것을 제외하고는 일반 클래스와 전혀 다르지 않다.

**추상화**

- 클래스간의 공통점을 찾아내서 공통의 조상을 만드는 작업

**구체화**

- 상속을 통해 클래스를 구현, 확장하는 작업

### 추상 메서드(abstract method)

추상 메서드란 선언부만 작성하고 구현부는 작성하지 않은 채로 남겨 둔 것이다.

추상 클래스로부터 상속받는 자손 클래스는 오버라이딩을 통해 조상인 추상 클래스의 추상 메서드를 모두 구현해주어야 한다. 만일 조상으로부터 상속받은 추상 메서드 중 하나라도 구현하지 않는다면, 자손 클래스 역시 추상 클래스로 지정해 주어야 한다.

---

## 추상클래스

추상클래스는 미완성 설계도에 비유할 수 있다.

추상클래스 자체로는 클래스로서의 역할을 다 못하지만, 새로운 클래스를 작성하는데 있어서 바탕이 되는 조상 클래스로서 중요한 의미를 갖는다.

그러니깐 "자식클래스들은 이 메소드를 써야해!" 하고 틀을 만들어주는 것이다.

추상클래스에도 생성자가 있고, 멤버변수와 메소드를 가질 수 있다.

**기존 클래스의 공통부분을 뽑아 조상클래스로 만드는 개념이다.**

### 미완성 상태로 남겨놓는 이유

상속받는 클래스에 따라 메소드의 내용이 달라질 수 있다.

그렇기 때문에 선언부만을 작성해서 해당 기능의 목적을 알려주는 것이다.

자식클래스들은 해당 메소드를 받아 적절히 구현하는 것이다.

### 구현방법

```
abstract class Player {
	abstract void play(int post);
    void stop();
}
```

메소드에 `abstract` 를 붙이면 자식 클래스에서 해당 메소드를 구현하도록 강제할 수 있다.

## 인터페이스

- 인터페이스는 일종의 추상클래스이다.
- 추상클래스처럼 추상메소드를 갖지만 추상화 정도가 더 높다.
- 추상메소드와 상수만을 멤버로 가질 수 있다.
- 일반 메소드, 멤버변수를 가질 수 없다.

구현된 것은 아무것도 없고 밑그림만 그려져 있는 기본 설계도와 같다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/fbca977c-a4d8-4259-b807-cc36f66905b9">

### 구현방법

```
interface 인터페이스이름 {
	public static final 타입 상수이름 = 값;
    public abstract 메소드이름(매개변수목록);
}
```

### 주의 사항

- 모든 멤버변수는 `public static final` 이어야 하며, 이를 생략할 수 있다.
- 모든 메소드는 `public abstract`이어야 하며, 이를 생략할 수 있다.

생략하면 컴파일러가 자동으로 추가해준다.

### 인터페이스의 상속

```
interface Movable {
	void move(int x, int y);
}
interface Attackable {
	void attack(Unit u);
}
interface Fightable extends Movable, Attackable {}
```

클래스와 달리 다중상속이 가능하다.

> interface는 Object클래스와 같은 최고 조상이 없다.
> 

### 인터페이스의 구현

```
class 클래스이름 implements 인터페이스이름 {
	...
}
```

`extends`가 아닌 `implements`를 사용한다.

- 만일 구현하는 인터페이스 메소드 중에 일부만 구현한다면 abstract를 붙여 추상클래스로 선언해야한다.
- 구현하는 클래스에서는 `public`을 꼭 붙여야 한다. 접근 제어자의 범위를 같거나 좁게해야하기 때문이다.

### 인터페이스를 이용한 다형성

1. 인터페이스의 타입의 참조로 구현한 클래스의 인스턴스를 참조할 수 있다.

```
class Fighter extends Unit implements Fightable {
	...
}

Fightable f = new Fighter();
```

1. 인터페이스는 다음과 같이 메소드의 매개변수의 타입으로 사용될 수 있다.

```
void attack(Fightable f) {
	...
}
```

그러면 1번에 의해서 다음과 같이 할 수 있다.

`attack(new Fighter())`

1. 메소드의 리턴타입으로 인터페이스의 타입을 지정할 수 있다.

```
Fightable method() {
	return new Fighter();
}
```

- **리턴타입이 인터페이스라는 것은 메소드가 해당 인터페이스를 구현한 클래스의 인스턴스를 반환하다는 것을 의미한다.**이 문장은 극도로 중요하다고 나와있다. 위의 코드를 보면 알 수 있다.

### 인터페이스의 장점

- 개발시간을 단축할 수 있다.
- 표준화가 가능하다.
- 서로 관계없는 클래스들에게 관계를 맺어줄 수 있다.
- 독립적인 프로그래밍이 가능하다.

### 인터페이스의 이해

- 클래스를 사용하는 쪽과 클래스를 제공하는 쪽이 있다.
- 메소드를 사용하는 쪽에서는 사용하려는 메소드의 선언부만 알면 된다. (내부는 몰라도 된다.)