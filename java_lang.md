# java.lang 패키지와 유용한 클래스

---

## Object 클래스

object 클래스는 모든 클래스의 최고 조상이기 때문에 Ojbect 클래스의 멤버들은 모든 클래스에서 사용 가능하다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/2b39acad-608b-461b-8b6f-c94cb7707d5f">

### Object 메소드

| 메소드 | 설명 |
| --- | --- |
| protected Object clone() | 해당 객체의 복제본을 생성하여 반환함. |
| boolean equals(Object obj) | 해당 객체와 전달받은 객체가 같은지 여부를 반환함. |
| protected void finalize() | 해당 객체를 더는 아무도 참조하지 않아 가비지 컬렉터가 객체의 리소스를 정리하기 위해 호출함. |
| Class<T> getClass() | 자신이 속한 클래스의 Class객체를 반환하는 메서드
Class객체는 클래스의 모든 정보를 담고 있으며, 클래스당 단 1개만 존재
클래스 파일(*. class)이 메모리에 로드될 때 생성된다. |
| int hashCode() | 해당 객체의 해시 코드값을 반환함. |
| void notify() | 해당 객체의 대기(wait)하고 있는 하나의 스레드를 다시 실행할 때 호출함. |
| void notifyAll() | 해당 객체의 대기(wait)하고 있는 모든 스레드를 다시 실행할 때 호출함. |
| String toString() | 해당 객체의 정보를 문자열로 반환함. |
| void wait() | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행할 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출함. |
| void wait(long timeout) | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행하거나 전달받은 시간이 지날 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출함. |
| void wait(long timeout, int nanos) | 해당 객체의 다른 스레드가 notify()나 notifyAll() 메소드를 실행하거나 전달받은 시간이 지나거나 다른 스레드가 현재 스레드를 인터럽트(interrupt) 할 때까지 현재 스레드를 일시적으로 대기(wait)시킬 때 호출함. |

### toString() 메소드

toString() 메소드는 해당 인스턴스에 대한 정보를 문자열로 반환한다.

이때 반환되는 문자열은 클래스 이름과 함께 구분자로 '@'가 사용되며, 그 뒤로 16진수 해시 코드(hash code)가 추가된다.

16진수 해시 코드 값은 인스턴스의 주소를 가리키는 값으로, 인스턴스마다 모두 다르게 반환된다.

```java
Car car01 = new Car();

Car car02 = new Car();

System.out.println(car01.toString());

System.out.println(car02.toString());
-----------------------------------
결과

Car@15db9742

Car@6d06d69c
```

### equals() 메소드

equals() 메소드는 해당 인스턴스를 매개변수로 전달받는 참조 변수와 비교하여, 그 결과를 반환한다.

이때 참조 변수가 가리키는 값을 비교하므로, 서로 다른 두 객체는 언제나 false를 반환하게 된다.

```java
Car car01 = new Car();

Car car02 = new Car();

System.out.println(car01.equals(car02));

car01 = car02; // 두 참조 변수가 같은 주소를 가리킴.

System.out.println(car01.equals(car02));
------------------------------------------
결과
false

true
```

### clone() 메소드

clone() 메소드는 해당 인스턴스를 복제하여, 새로운 인스턴스를 생성해 반환한다.

하지만 Object 클래스의 clone() 메소드는 단지 필드의 값만을 복사하므로, 필드의 값이 배열이나 인스턴스면 제대로 복제할 수 없다. (얉은 복사)

따라서 이러한 경우에는 해당 클래스에서 clone() 메소드를 오버라이딩하여, 복제가 제대로 이루어지도록 재정의해야 한다.

이러한 clone() 메소드는 데이터의 보호를 이유로 Cloneable 인터페이스를 구현한 클래스의 인스턴스만이 사용할 수 있다.

```java
import java.util.*;

class Car implements Cloneable {
   private String modelName;
①  private ArrayList<String> owners = new ArrayList<String>();

   public String getModelName() { 
		return this.modelName; 
	 }  // modelName의 값을 반환함

   public void setModelName(String modelName) { 
				this.modelName = modelName; 
	 } // modelName의 값을 설정함

    public ArrayList getOwners() { 
				return this.owners; 
	  }// owners의 값을 반환함

    public void setOwners(String ownerName) { 
				this.owners.add(ownerName); 
		}// owners의 값을 추가함

    public Object clone() {

        try {

					② Car clonedCar = (Car)super.clone();

					③ // clonedCar.owners = (ArrayList)owners.clone();

            return clonedCar;

				 ④} catch (CloneNotSupportedException ex) {
            ex.printStackTrace();
            return null;
        }
    }
}

public class Object03 {
    public static void main(String[] args) {
			⑤ Car car01 = new Car();
        car01.setModelName("아반떼");

        car01.setOwners("홍길동");
			⑥ System.out.println("Car01 : " + car01.getModelName() + ", " + car01.getOwners() + "\n");

      ⑦ Car car02 = (Car)car01.clone();

      ⑧ car02.setOwners("이순신");

      ⑨ System.out.println("Car01 : " + car01.getModelName() + ", " + car01.getOwners());

      ⑩ System.out.println("Car02 : " + car02.getModelName() + ", " + car02.getOwners());

    }

}
-----------------------------------
결과
Car01 : 아반떼, [홍길동]
Car02 : 아반떼, [홍길동, 이순신]
Car02 : 아반떼, [홍길동, 이순신]
③번 줄 주석을 해제한 결과
Car01 : 아반떼, [홍길동] 
Car02 : 아반떼, [홍길동]
Car02 : 아반떼, [홍길동, 이순신]
```

---

## **String 클래스**

String 인스턴스는 한 번 생성되면 그 값을 읽기만 할 수 있고, 변경할 수는 없다.

이러한 객체를 자바에서는 불변 객체(immutable object)라고 한다.

즉, 자바에서 덧셈(+) 연산자를 이용하여 문자열 결합을 수행하면, 기존 문자열의 내용이 변경되는 것이 아니라 내용이 합쳐진 새로운 String 인스턴스가 생성되는 것이다. (**String Interning**)

### **String 메소드**

| 메소드 | 설명 |
| --- | --- |
| char charAt(int index) | 해당 문자열의 특정 인덱스에 해당하는 문자를 반환함. |
| int compareTo(String str) | 해당 문자열을 인수로 전달된 문자열과 사전 편찬 순으로 비교함. |
| int compareToIgnoreCase(String str) | 해당 문자열을 인수로 전달된 문자열과 대소문자를 구분하지 않고 사전 편찬 순으로 비교함. |
| String concat(String str) | 해당 문자열의 뒤에 인수로 전달된 문자열을 추가한 새로운 문자열을 반환함. |
| int indexOf(int ch)int indexOf(String str) | 해당 문자열에서 특정 문자나 문자열이 처음으로 등장하는 위치의 인덱스를 반환함. |
| int indexOf(int ch, int fromIndex)
int indexOf(String str, int fromIndex) | 해당 문자열에서 특정 문자나 문자열이 전달된 인덱스 이후에 처음으로 등장하는 위치의 인덱스를 반환함. |
| int lastIndexOf(int ch) | 해당 문자열에서 특정 문자가 마지막으로 등장하는 위치의 인덱스를 반환함. |
| int lastIndexOf(int ch, int fromIndex) | 해당 문자열에서 특정 문자가 전달된 인덱스 이후에 마지막으로 등장하는 위치의 인덱스를 반환함. |
| String[] split(String regex) | 해당 문자열을 전달된 정규 표현식(regular expression)에 따라 나눠서 반환함. |
| String substring(int beginIndex) | 해당 문자열의 전달된 인덱스부터 끝까지를 새로운 문자열로 반환함. |
| String substring(int begin, int end) | 해당 문자열의 전달된 시작 인덱스부터 마지막 인덱스까지를 새로운 문자열로 반환함. |
| String toLowerCase() | 해당 문자열의 모든 문자를 소문자로 변환함. |
| String toUpperCase() | 해당 문자열의 모든 문자를 대문자로 변환함. |
| String trim() | 해당 문자열의 맨 앞과 맨 뒤에 포함된 모든 공백 문자를 제거함. |
| length() | 해당 문자열의 길이를 반환함. |
| isEmpty() | 해당 문자열의 길이가 0이면 true를 반환하고, 아니면 false를 반환함. |

### StringBuffer 클래스

String 클래스의 인스턴스는 한 번 생성되면 그 값을 읽기만 할 수 있고, 변경할 수는 없다.

하지만 StringBuffer 클래스의 인스턴스는 그 값을 변경할 수도 있고, 추가할 수도 있다.

이를 위해 StringBuffer 클래스는 내부적으로 버퍼(buffer)라고 하는 독립적인 공간을 가진다.

버퍼 크기의 기본값은 16개의 문자를 저장할 수 있는 크기이며, 생성자를 통해 그 크기를 별도로 설정할 수도 있다.

하지만 인스턴스 생성 시 사용자가 설정한 크기보다 언제나 16개의 문자를 더 저장할 수 있도록 여유 있는 크기로 생성된다.

StringBuffer 인스턴스를 사용하면 문자열을 바로 추가할 수 있으며, 공간의 낭비도 없으며 속도도 매우 빨라진다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/8b23f887-662f-4825-8754-f3aca3f23eeb">

### **StringBuffer 메소드**

| 메소드  | 설명 |
| --- | --- |
| StringBuffer append(boolean b)
StringBuffer append(char c)
StringBuffer append(char[] str)
StringBuffer append(CharSequence s)
StringBuffer append(double d)
StringBuffer append(float f)
StringBuffer append(int i)
StringBuffer append(long lng)
StringBuffer append(Object obj)
StringBuffer append(String str)
StringBuffer append(StringBuffer sb) | 인수로 전달된 값을 문자열로 변환한 후, 해당 문자열의 마지막에 추가함. |
| int capacity() | 현재 버퍼 크기를 반환함. |
| StringBuffer delete(int start, int end) | 전달된 인덱스에 해당하는 부분 문자열을 해당 문자열에서 제거함. |
| StringBuffer deleteCharAt(int index) | 전달된 인덱스에 해당하는 문자를 해당 문자열에서 제거함. |
| StringBuffer insert(int offset, boolean b)
StringBuffer insert(int offset, char c)
StringBuffer insert(int offset, char[] str)
StringBuffer insert(int offset, CharSequence s)
StringBuffer insert(int offset, double d)
StringBuffer insert(int offset, float f)
StringBuffer insert(int offset, int i)
StringBuffer insert(int offset, long lng)
StringBuffer insert(int offset, Object obj)
StringBuffer insert(int offset, String str) | 인수로 전달된 값을 문자열로 변환한 후, 해당 문자열의 지정된 인덱스 위치에 추가함. |
| StringBuffer reverse() | 해당 문자열의 인덱스를 역순으로 재배열함. |

### StringBuilder

StringBuffer는 멀티쓰레드에 Thread safe 하도록 동기화 되어있다. 동기화가 StringBuffer의 성능을 떨어뜨리는데, 만약 멀티쓰레드로 작성된 프로그램이 아닌경우, StringBuffer의 동기화는 불필요한 성능저하를 야기한다. 그래서 StringBuffer에서 쓰레드의 동기화를 제외한 StringBuilder가 새로 추가되었다. 두 클래스는 완전히 똑같은 기능으로 동작한다.

하지만 StringBuffer도 충분히 성능이 좋기 때문에 성능향상이 반드시 필요하지 않는 경우라면 StringBuffer를 사용해도 무방하다.

---

## Math 클래스

Math클래스는 기본적인 수학계산에 유용한 메서드로 구성되어 있으며, 클래스 내에 인스턴스변수가 하나도 없으므로 Math클래스의 메서드는 모두 static다.

### Math 메소드

| 메소드 | 설명 |
| --- | --- |
| static double random() | 0.0 이상 1.0 미만의 범위에서 임의의 double형 값을 하나 생성하여 반환함. |
| static double abs(double a)
static double abs(float a)
static double abs(int a)
static double abs(long a) | 전달된 값이 음수이면 그 값의 절댓값을 반환하며, 전달된 값이 양수이면 인수를 그대로 반환함. |
| static double ceil(double a) | 전달된 double형 값의 소수 부분이 존재하면 소수 부분을 무조건 올리고 반환함. |
| static double floor(double a) | 전달된 double형 값의 소수 부분이 존재하면 소수 부분을 무조건 버리고 반환함. |
| static long round(double a)
static int round(float a) | 전달된 값을 소수점 첫째 자리에서 반올림한 정수를 반환함. |
| static double max(double a, double b)
static float max(float a, float b)
static long max(long a, long b)
static int max(int a, int b) | 전달된 두 값을 비교하여 큰 값을 반환함. |
| static double min(double a, double b)
static float min(float a, float b)
static long min(long a, long b)
static int min(int a, int b) | 전달된 두 값을 비교하여 작은 값을 반환함. |
| static double pow(double a, double b) | 전달된 두 개의 double형 값을 가지고 제곱 연산을 수행하여, ab을 반환함. |
| static double sqrt(double a) | 전달된 double형 값의 제곱근 값을 반환함. |

---

### 래퍼 클래스(Wrapper class)

프로그램에 따라 기본 타입의 데이터를 객체로 취급해야 하는 경우가 있다.

예를 들어, 메소드의 인수로 객체 타입만이 요구되면, 기본 타입의 데이터를 그대로 사용할 수는 없다.

이때에는 기본 타입의 데이터를 먼저 객체로 변환한 후 작업을 수행해야 한다.

이렇게 8개의 기본 타입에 해당하는 데이터를 객체로 포장해 주는 클래스를 래퍼 클래스(Wrapper class)라고 한다.

래퍼 클래스는 각각의 타입에 해당하는 데이터를 인수로 전달받아, 해당 값을 가지는 객체로 만들어 준다.

| 기본 타입 | 래퍼 클래스 |
| --- | --- |
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
| char | Character |
| boolean | Boolean |

### **박싱(Boxing)과 언박싱(UnBoxing)**

래퍼 클래스(Wrapper class)는 산술 연산을 위해 정의된 클래스가 아니므로, 인스턴스에 저장된 값을 변경할 수 없다.

단지, 값을 참조하기 위해 새로운 인스턴스를 생성하고, 생성된 인스턴스의 값만을 참조할 수 있다.

<img src="https://github.com/GYEONGDONGBAEK/JavaStudy/assets/122242439/7776e369-911d-49dd-837d-8f6cd51e5c88">

기본 타입의 데이터를 래퍼 클래스의 인스턴스로 변환하는 과정을 박싱(Boxing)이라고 한다.

반면 래퍼 클래스의 인스턴스에 저장된 값을 다시 기본 타입의 데이터로 꺼내는 과정을 언박싱(UnBoxing)이라고 한다.

### 오토 박싱(AutoBoxing)과 오토 언박싱(AutoUnBoxing)

JDK 1.5부터는 박싱과 언박싱이 필요한 상황에서 자바 컴파일러가 이를 자동으로 처리해 준다.

이렇게 자동화된 박싱과 언박싱을 오토 박싱(AutoBoxing)과 오토 언박싱(AutoUnBoxing)이라고 부다.

---

## 정규식(regex)

Pattern 클래스는 정규식을 정의하는데 사용되고 Matcher 클래스는 정규식을 데이터와 비교하는 역할을 한다.

| 정규식 패턴 | 설명 |
| --- | --- |
| c[a-z]* | c로 시작하는 a~z로 이루어진 문자열 |
| c[a-z] | c와 a~z로 시작하는 두 자리 문자열 |
| c[a-zA-Z] | c와 a~z또는 A~Z로 시작하는 두 자리 문자열 |
| c[a-zA-Z0-9]c\w | c로 시작하고 숫자와 영어로 조합된 두 자리 문자열 |
| .* | 모든 문자열 |
| c. | c로 시작하는 두 자리 문자열 |
| c.* | c로 시작하는 모든 문자열 |
| c\. | 문자열 "c." |
| c\dc[0-9] | c와 숫자로 구성된 두 자리 문자열 |
| c.*t | c로 시작하고 t로 끝나는 문자열 |
| [b|c].*[bc].*[b-c].* | b또는 c로 시작하는 문자열 |
| [^b|c].*[^bc].*[^b-c].* | b또는 c로 시작하지 않는 문자열 |
| .*a.* | a를 포함하는 모든 문자열 |
| .*a.+ | a를 포함하지만 a하나만으로 끝나지 않는 모든 문자열 |
| [b|c].{2} | b또는 c로 시작하는 세 자리 문자열 |
| \\d{3,4} | 3~4자리 숫자 |